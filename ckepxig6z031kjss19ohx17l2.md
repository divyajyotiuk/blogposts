## setTimeout() - an edge case

Recently, I had come across a bug that needed auto-refresh after a certain point of time. And `setTimeout()` had been used to count down to the time and reload the page. Little did I know that `setTimeout()` came with a price. 


As quoted on MDN Web Docs at the very _bottom_, **"Browsers including Internet Explorer, Chrome, Safari, and Firefox store the delay as a 32-bit signed integer internally. This causes an integer overflow when using delays larger than 2,147,483,647 ms (about 24.8 days), resulting in the timeout being executed immediately."**


Now, you'll understand what kept happening to the page! (The page kept reloading...)


It is very much true that there is hardly any process that would require this big a delay. You have other options, like reseting timer after certain duration or using `setInterval()`. 

I would prefer `setInterval()`, when there are simple operations in the callback function and when you know what is the maximum time that function is going to take to execute. If you aren't aware of the maximum time, the event queue will keep piling up forever as your code's activity lags behind the actual system time. 

Choose wise! Don't forget to clear the timers when your job is done!

### Other Blogposts you might like to checkout!

- **[How to make using Github tools easy?](https://divyajyotiuk.hashnode.dev/how-to-make-using-github-tools-easy-ckecebppj00h4a7s1canncfm7)**
- **[Twitter: Automate updating follower count in your name](https://divyajyotiuk.hashnode.dev/twitter-automate-updating-follower-count-in-your-name-ckeh597ez02z8p2s1fkdkg1su
)**
- **[Header tags and how they boost SEO](https://divyajyotiuk.hashnode.dev/header-tags-and-how-they-boost-seo-ckemx9ynn04kg99s1hwat4t1m)**
- **[Clojure and Leiningen to manage Clojure projects](https://divyajyotiuk.hashnode.dev/clojure-and-leiningen-to-manage-clojure-projects-ckesb05t1005qs6s1gvcy7nfj)**
- **[How to create React App with Flask backend?](https://divyajyotiuk.hashnode.dev/how-to-create-react-app-with-flask-backend-ckfl971az02si5ds1h7qnabk9)**
- **[Exporting your Twitter bookmarks in markdown file](https://divyajyotiuk.hashnode.dev/exporting-your-twitter-bookmarks-in-markdown-file)**
