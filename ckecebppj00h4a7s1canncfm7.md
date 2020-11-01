## How to make using Github tools easy?

Are you `committing` mistakes on Git? Mixing up the branches? Don't know how to revert correctly? `Git` being a command-line tool might be a little tough to get along with. There are other tools from **Github** that can make life easy. 

I have just started as Software Engineer at a startup after completing my CS degree. I haven't come across Github being taught in the university courses. But it is a necessity in the corporate world.

Here are some ways which I think are mostly used in all companies, you need to get thorough with. 

It is seen that `ssh keys` are used, so that you wouldn't need to do authentication every time you have to push changes. Once you start using it, you'll realise it saves time. And if you are over a zoom call with your boss breathing down your neck for you to push changes, you wouldn't want to exasperate them.

Add `ssh key` to your Github account and start using it!


- **First step is:**
```
git clone "repo-url"
```
This is pretty basic step. Though there are n-branches for that repository, only the `default` one gets cloned.

At work, you would be told to create your own branch to start working. 

- **To check your current branch use:**
```
git branch 
```


- **It is better to use Github web to create origin branch.** It's really easy to create and you understand from where should your branch originate. 

![Click here](https://dev-to-uploads.s3.amazonaws.com/i/o9qi8dhlig9hyc9wgmep.png)


Select branch from which you wish to create and then enter the name of the branch. The naming conventions might differ but if you are developing a new feature start with `feature/feature-name` or `development/`. If you are teaming up with someone `team/feature-name`. For bug fixes, don't forget to include `bug` or `fix` in the branch-name. For rest you can use your name `your-name/task-name`. 

- **Now, you create the same branch on your machine (local branch)**. It is better to name the branch the same as the origin. 
```
git checkout -b "branch-name"
```

You need to track the origin branch for any commits and code pushes. Setting upstream allows you to track the origin branch. You could use just `git pull` and `git push` without mentioning the remote.

- **Set upstream using this command.**
```
git branch --set-upstream-to=origin/<branch-name> <branch-name>
```

- **It is always safe to rebase whenever you are taking a pull from the origin.** A basic `git pull` might merge your commits on your local into one commit. A rebase will apply your commits on top of the working tree, so you know if you want those commits on the branch or not.
```
git pull --rebase
```


- **Github desktop is really handy**. It eliminates the effort of staging the changes using `git add` before committing. You can see all your changes in various different files and choose what files to commit by checking the checkbox.
Right clicking on commit gives you many options like `Revert this Commit`, `Create Tag`, `Copy commit hash`. 

![Click here](https://dev-to-uploads.s3.amazonaws.com/i/ij3sak5hmr2pmqk8nney.png)

The easiest way that I found to revert commit is using Github Desktop. 

You can see your current branch and switch branches. Take a rebase whenever you are switching branches. This will apply commits on top of the working tree. You can view this in the history tab of Github desktop. 

- **To remove unwanted commits at the top you can use:**
```
git reset --hard "commit-hash"
```
to start anew!

OR

- **To retain the changes and choose what to commit again, use:**
```
git reset --soft "commit-hash"
```



- Alternative to reseting `^HEAD`, will be creating a branch from a specific commit, if you think you have messed up after some commit and wish to redo. 
```
git checkout -b "branch-name" "commit-hash"
```

- And suppose you want a specific commit from another branch, you can `cherry-pick` that commit into your branch. This commit will sit on top of your working tree.
```
git cherry-pick "commit-hash"
```
I would recommend you use this only when the other branch is going to remain un-merged. Otherwise, merge would create duplicate commits in the working tree. 


- Use github web to merge branches. Create a pull request. When you do this, you can compare and see if the branch is `Able to merge`. 
![Click here](https://dev-to-uploads.s3.amazonaws.com/i/4o5s5dq5738323rr6hh9.png)
Go ahead and merge, choose a reviewer if needs code review.

And if you see this, `Can't automatically merge`
![Click here](https://dev-to-uploads.s3.amazonaws.com/i/gxxl117kvsgnmkv9jqyd.png)

You need to do it locally and resolve merge conflicts. In this case, if you wish to merge `branch B` into `branch A`. You need to checkout to `branch A` and use: 
```
git merge "branch B"
```
And now you when you come to Github desktop, it will prompt you to resolve conflicts. If you are resolving conflicts, sit with your team and do it. This way you avoid overwriting anybody else's precious code.

- **To visualize your repository branches as a graph**:
On Github web, go to **Insights** tab and select **Network** from the side bar. Which will look something like this,
![Click here](https://res.cloudinary.com/practicaldev/image/fetch/s--4T-xm85i--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://thepracticaldev.s3.amazonaws.com/i/gcqluv5zi95chw3igk8o.png)

- **To remove all your local branches except the master branch:**

```
git branch | grep -v "master" | xargs git branch -D
```

I think this was all pretty basic stuff, which you might have come across. But in corporate, you must be extra careful before making any changes. Your code is valuable and affects the company value in the market.

Keep coding!


### Other Blogposts you might like to checkout!

- **[Twitter: Automate updating follower count in your name](https://divyajyotiuk.hashnode.dev/twitter-automate-updating-follower-count-in-your-name-ckeh597ez02z8p2s1fkdkg1su
)**
- **[Header tags and how they boost SEO](https://divyajyotiuk.hashnode.dev/header-tags-and-how-they-boost-seo-ckemx9ynn04kg99s1hwat4t1m)**
- **[setTimeout() - an edge case](https://divyajyotiuk.hashnode.dev/settimeout-an-edge-case-ckepxig6z031kjss19ohx17l2)**
- **[Clojure and Leiningen to manage Clojure projects](https://divyajyotiuk.hashnode.dev/clojure-and-leiningen-to-manage-clojure-projects-ckesb05t1005qs6s1gvcy7nfj)**
- **[How to create React App with Flask backend?](https://divyajyotiuk.hashnode.dev/how-to-create-react-app-with-flask-backend-ckfl971az02si5ds1h7qnabk9)**
- **[Exporting your Twitter bookmarks in markdown file](https://divyajyotiuk.hashnode.dev/exporting-your-twitter-bookmarks-in-markdown-file)**


 