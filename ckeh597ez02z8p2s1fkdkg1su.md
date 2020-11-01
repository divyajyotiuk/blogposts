## Twitter: Automate updating follower count in your name

I wanted something fun to do in the weekend! Since, many people on dev twitter are building bots, I started this as a starting point. 

This is how it looks - my name with follower count:
![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ujpi8or1qya7ganvssrf.png)

In this blogpost, I have listed one way of doing this. You'll find many other ways too!

**Tech stack for this pet project**

- Node.js
- [twitter-lite](https://www.npmjs.com/package/twitter-lite) (npm package)
- [Vercel](https://vercel.com/) (for hosting)
- [cron-job](https://console.cron-job.org/) (free cron service to automate the update)

**Pre-requisites**
- You must have an [approved twitter developer account](https://developer.twitter.com/en/apply-for-access), and have activated the [developer portal](https://developer.twitter.com/en/portal/dashboard) where you can create new app. 
- You get all your access tokens and API keys here and also a bearer token.

**Step 1**: 

To write the code first.

We will be using twitter-lite, there are other packages as well that wrap the twitter API. First step is to create a twitter client that would fetch and send twitter data. 

```js
const Twitter = require('twitter-lite');

const twitterClient = new Twitter({
    subdomain: "api", // we are using twitter api
    version: "1.1", // twitter api version 1.1
    consumer_key: process.env.API_KEY,
    consumer_secret: process.env.API_SECRET,
    access_token_key: process.env.ACCESS_TOKEN, 
    access_token_secret: process.env.ACCESS_TOKEN_SECRET
});

```
Don't forget to add these environment variable when deploying on vercel.

The logic comes here:

```js

const name  = 'Divyajyoti👩‍💻JS';

module.exports = (req, res) => {

    let httpResponse = res;
    twitterClient.get('account/verify_credentials')
            .then((res) => {

                if(!res){
                    httpResponse.status(500).send("Error fetching Twitter Client");
                }

                const followerCount = res.followers_count;

                const userName = `${name}|${followerCount}`;

                return userName;
            })
            .then((user_name) => {
                const response = twitterClient.post("account/update_profile", { name: user_name });

                response.then((res) => {

                    if(!res){
                        httpResponse.status(500).send("Update error");
                    }else{
                        httpResponse.status(200).send(`Update ${user_name} Success!`);
                    }
                })
                .catch((err) => {
                   httpResponse.status(500).send(err);
                });
            })
            .catch((err) => {
                httpResponse.status(500).send(err);
            });

};
``` 

It's my habit to add all these checks, you can avoid if you want but it helps in debugging. 

If you want the number emojis as well, just create an object mapping and append.

The reason I used 
```js
module.exports = (req, res) => {}
```
is because [Vercel Serverless functions](https://vercel.com/docs/serverless-functions/introduction) demand it. Keep the file in `/api` folder, for vercel to identify it as lambda function. 

So, it would look like we have created an API endpoint that will do the dynamic updating.

**Step 2:**

If you have done this correctly, rest all is easy job. I would suggest uploading your project on Github. Vercel is easy to use if you have Git integration. 

Import the project using github repo url, add the environment vars and deploy it! 

Open the url provided by vercel. If /api is not formed add /api/<name of file> if not index.js

Now go to Function logs and select the your function from dropdown. You'll see your api logs here. 

Visit the url and see what message comes in the body. If it's successful, you'll see the change in your twitter account as well.

**Step 3:**

Now to update it with cron service. You don't need to manually hit the api to update change, cron will do the job for you. 

Go to [cron-job](https://console.cron-job.org/) and create an account. 
Create your first cron job, give your Vercel api url, specify the time interval to make your requests that will automatically run the function and update your twitter name.

Your job is done here! 

You can comment if you get stuck or have any questions!


I referred these articles:
- https://dev.to/code_rams/twitter-dynamic-name-generator-3ka2 by [@code_rams](https://twitter.com/code_rams)
- https://dev.to/radnerus/twitter-api-is-followers-count-mda by [@radnerus93](https://twitter.com/radnerus93) 


### Other Blogposts you might like to checkout!

- **[How to make using Github tools easy?](https://divyajyotiuk.hashnode.dev/how-to-make-using-github-tools-easy-ckecebppj00h4a7s1canncfm7)**
- **[Header tags and how they boost SEO](https://divyajyotiuk.hashnode.dev/header-tags-and-how-they-boost-seo-ckemx9ynn04kg99s1hwat4t1m)**
- **[setTimeout() - an edge case](https://divyajyotiuk.hashnode.dev/settimeout-an-edge-case-ckepxig6z031kjss19ohx17l2)**
- **[Clojure and Leiningen to manage Clojure projects](https://divyajyotiuk.hashnode.dev/clojure-and-leiningen-to-manage-clojure-projects-ckesb05t1005qs6s1gvcy7nfj)**
- **[How to create React App with Flask backend?](https://divyajyotiuk.hashnode.dev/how-to-create-react-app-with-flask-backend-ckfl971az02si5ds1h7qnabk9)**
- **[Exporting your Twitter bookmarks in markdown file](https://divyajyotiuk.hashnode.dev/exporting-your-twitter-bookmarks-in-markdown-file)**



 







