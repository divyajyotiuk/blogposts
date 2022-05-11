## Redirect other domain requests to your Nextjs App

This is a mechanism to secure your web application from running on a different host. Running your application on a different host may lead to security issues like leaking of user information, requesting servers other than your server, and a lot more which is not in the scope of this article. Concisely speaking, this is to prevent website spoofing.

You can directly jump down to [Secure your Nextjs App](#secure-your-nextjs-app) section to see the code.

Let's try to simulate this scenario.

Open your terminal.
```
$ ping ecbiz312.inmotionhosting.com
```
Copy the IP address - 209.182.215.63

Go to your hosts file.
```
// in macOS
$ sudo vim /etc/hosts
```
And make changes as below
```
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1       localhost
209.182.215.63  mywebsite.xyz
255.255.255.255 broadcasthost
::1             localhost
~
~
```

Now open https://mywebsite.xyz on your browser. You should see the same content as ecbiz312.inmotionhosting.com site. If you look at the headers, it shows the same remote address.
<br>
<img width="1369" alt="Screenshot 2022-05-11 at 1 59 48 PM" src="https://user-images.githubusercontent.com/30872426/167828325-a0bd0043-bf18-46c6-8ae8-20fc11473ea5.png">
<br>
<img width="1369" alt="Screenshot 2022-05-11 at 1 59 54 PM" src="https://user-images.githubusercontent.com/30872426/167828354-08231e5f-765c-41b9-a4dc-3379f08f1b04.png">
<br>
<img width="694" alt="Screenshot 2022-05-11 at 2 00 55 PM" src="https://user-images.githubusercontent.com/30872426/167828396-ea0041ea-8898-4b13-abb9-12b7cfd6f450.png">
<br>
<img width="694" alt="Screenshot 2022-05-11 at 2 00 36 PM" src="https://user-images.githubusercontent.com/30872426/167828370-726c56be-097d-4b47-860d-5daae3e1aa9d.png">
<br>

It is completely fine if you are not able to simulate this on your machine. 

### Secure your Nextjs App
Now, let’s write a way to prevent this in our Nextjs App. We will write a code that will check the host from request headers and redirect to our application if the domain is not whitelisted. So, if mywebsite.xyz requests ecbiz312.inmotionhosting.com app, ecbiz312.inmotionhosting.com should not let mywebsite.xyz access.

In your _app.js file,

```
MyApp.getInitialProps = async ( appContext ) => {
  const appProps = await App.getInitialProps(appContext);
  const req = appContext.ctx.req;
  const res = appContext.ctx.res;
  if ( req ) {
    const headers = req.headers;
    const host = headers.host;
    const whiteList = [“your”,”whitelisted”, “domains”];
    let len = whiteList.length;
    let isInvalidHost = true;
    while( len-- ) {
      let thisWhiteListDomain = whiteList[ len ];
      thisWhiteListDomain = thisWhiteListDomain.replace("https://", "");
      if ( host === thisWhiteListDomain ) {
        isInvalidHost = false;
        break;
      }
    }

    if ( res && isInvalidHost ) {
      res.writeHead(301, {
        Location: `https://your-application-domain`
      });
      res.end();
    }
  }

  return appProps;
};

```
So, if another domain tries to request our application, we redirect the user with 301(permanent redirect - good for SEO).

