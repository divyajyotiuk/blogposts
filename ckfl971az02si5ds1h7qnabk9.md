## How to create React App with Flask backend?

Do you want use Python as backend for your React project? You can write the frontend logic in Javascript and use Python for the backend. Flask makes this integration into one single project really easy.

We'll be covering,
- **Creating Flask API**
- **Creating React App**
- **Integration**

## Creating Flask API

First we start by creating a Flask project. I would recommend to make a separate folder to run the backend server code.

```
$ mkdir flask-api
$ cd flask-api
```

I always setup a virtual environment. A virtual environment manages dependencies of the project and remain particular for the single project. It does not affect the system packages. The following commands are for Unix-based systems. They create virtual environment and activates it. 

```
$ python3 -m venv venv
$ source venv/bin/activate
(venv) $ 
```

Python versions `<3.4` do not have virtual environments inbuilt. You need to install a third-party package `virtualenv`  and run `virtualenv venv`

Now you start installing flask and python's dotenv package. And flask-cors for handling Cross Origin Resource Sharing for making cross-origin http calls.

```
(venv) $ pip install flask python-dotenv
(venv) $ pip install -U flask-cors
```
Create a file `app.py` in the `flask-api` directory and initialise the flask environment. 

```
from flask import Flask
from flask_cors import CORS

app = Flask(__name__)
CORS(app)
```

The next step is to create a `.env` file which contains the following data. 
```
FLASK_APP=app.py
FLASK_ENV=development
```
Flask automatically imports the project from the `FLASK_APP` environment variable. And reads the environment from `FLASK_ENV` variable.

Let's start with writing a simple API that responds with  **"Hello World"**. In recent versions, Flask supports returning dictionary rather than calling `jsonify()` as Flask implicitly JSONifies the dictionary.

```
from flask import Flask
from flask_cors import CORS

app = Flask(__name__)
CORS(app)

@app.route('/hello')
def say_hello_world():
    return {'result': "Hello World"}
```

Start the Flask server using `flask run`. You should see something like this:
```
* Serving Flask app "app.py" (lazy loading)
* Environment: development
* Debug mode: on
* Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
* Restarting with fsevents reloader
* Debugger is active!
* Debugger PIN: 306-333-596
```

## Creating React App

```
$ npx create-react-app react-flask-app
$ cd react-flask-app
```
In `package.json`, add this particular line. It tells the development server to proxy the request to API server.
```
"proxy": "http://localhost:5000"
```

## Integration

In React's `App.js` file
```
import React, { useState, useEffect } from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  const [placeholder, setPlaceholder] = useState('Hi');

  useEffect(() => {
    fetch('/hello').then(res => res.json()).then(data => {
      setPlaceholder(data.result);
    });
  }, []);

  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
        <p>Flask says {placeholder}</p>
      </header>
    </div>
  );
}

export default App;
```
![Screenshot 2020-09-27 at 8.04.04 PM.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1601217268600/YXIVXq_eR.png)

Hurrah! We did it! It automatically makes a request to Flask backend and updates the DOM. There is no language barrier for client server communication.

### Other Blogposts you might like to checkout!

- **[How to make using Github tools easy?](https://divyajyotiuk.hashnode.dev/how-to-make-using-github-tools-easy-ckecebppj00h4a7s1canncfm7)**
- **[Twitter: Automate updating follower count in your name](https://divyajyotiuk.hashnode.dev/twitter-automate-updating-follower-count-in-your-name-ckeh597ez02z8p2s1fkdkg1su
)**
- **[Header tags and how they boost SEO](https://divyajyotiuk.hashnode.dev/header-tags-and-how-they-boost-seo-ckemx9ynn04kg99s1hwat4t1m)**
- **[setTimeout() - an edge case](https://divyajyotiuk.hashnode.dev/settimeout-an-edge-case-ckepxig6z031kjss19ohx17l2)**
- **[Clojure and Leiningen to manage Clojure projects](https://divyajyotiuk.hashnode.dev/clojure-and-leiningen-to-manage-clojure-projects-ckesb05t1005qs6s1gvcy7nfj)**
- **[Exporting your Twitter bookmarks in markdown file](https://divyajyotiuk.hashnode.dev/exporting-your-twitter-bookmarks-in-markdown-file)**
















