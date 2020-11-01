## Clojure and Leiningen to manage Clojure projects

I would like to introduce you to Clojure. I am fascinated by how it works and it is also known to sharpen your thinking as a programmer. In this article, we'll do a basic setup and start programming in Clojure!

## What is Clojure ?
**Daniel Higginbotham** in his book *Clojure for the Brave and True* has humorously defined Clojure as 
> 
an alloy of Lisp, functional programming and a lock of Rich Hickey's own epic hair

It combines Lisp dialect, powerful and expressive features of functional programming. Clojure is a *hosted language* meaning Clojure programs run on platforms like Java, Javascript and .NET and use their underlying features.  

## Leiningen
`Leiningen` is a useful tool to automate and manage your Clojure projects. Leiningen and Clojure require Java. Since, we are focusing on the JVM implementation of Clojure, OpenJDK will be required. You must have `> 1.6` java version installed.

Follow the steps on https://leiningen.org/ to download Leiningen. It will automatically download Clojure compiler, `clojure.jar`

### Creating a new project 
```
lein new app clojure-project
```

After installing you would find the following files in the directory.

- `project.clj` (like package.json of npm) contains project dependencies. 
- `resources` folder to save assets (like images). 
- `src/clojure-project/core.clj` will be where you write your code.

### Running the project

```
(ns clojure-project.core
  (:gen-class))

(defn -main
  "I don't do a whole lot...yet."
  [& args]
    (println "Hello, World!"))
```

This code will be already present in the `src/clojure-project/core.clj` file. If you have ever used C, C++ you would know namespace and the main function. Well, the `defn -main` is the starting point of your program. 

To run, `cd` into the clojure-project and run:
```
lein run
```
You should see `Hello, World!` as the output!

## Building the project

Clojure works even with environment change. It is not necessary that Leiningen is required to run the project elsewhere. To allow code shareability, we can create a stand-alone file that works where Java is installed. 

```
lein uberjar
```

After running this command a stand-alone file would be created in a *target/uberjar/* folder (same directory level as src). This jar file can be distributed on any platform.

## Using REPL

**REPL** - **r**ead, **e**valuate and **p**rint **l**oop. It is a tool that takes single line and executes the code as soon as it evaluates (just like Console in web developer tools or python prompt). 

To start Clojure repl
```
lein repl
```

The prompt would look something like this:
```
nREPL server started on port 56969 on host 127.0.0.1 - nrepl://127.0.0.1:56969
REPL-y 0.4.4, nREPL 0.7.0
Clojure 1.10.1
OpenJDK 64-Bit Server VM 1.8.0_242-b08
    Docs: (doc function-name-here)
          (find-doc "part-of-name-here")
  Source: (source function-name-here)
 Javadoc: (javadoc java-object-or-class-here)
    Exit: Control+D or (exit) or (quit)
 Results: Stored in vars *1, *2, *3, an exception in *e

clojure-project.core=> 
```

Clojure follows prefix notation and everything resides in matching parentheses. 

Samples to try out: 

- `(+ 1 2 3 4 5)` should add up all numbers and return 15
- `( str "hello world" )` should print `"hello world"`
- `( str "Hi! " "John " "Doe" )` should concatenate all the strings
- `( * 1 2 3 4 5 )` should return multiplied value 120


### Other Blogposts you would like to checkout!

- **[How to make using Github tools easy?](https://divyajyotiuk.hashnode.dev/how-to-make-using-github-tools-easy-ckecebppj00h4a7s1canncfm7)**
- **[Twitter: Automate updating follower count in your name](https://divyajyotiuk.hashnode.dev/twitter-automate-updating-follower-count-in-your-name-ckeh597ez02z8p2s1fkdkg1su
)**
- **[Header tags and how they boost SEO](https://divyajyotiuk.hashnode.dev/header-tags-and-how-they-boost-seo-ckemx9ynn04kg99s1hwat4t1m)**
- **[setTimeout() - an edge case](https://divyajyotiuk.hashnode.dev/settimeout-an-edge-case-ckepxig6z031kjss19ohx17l2)**
- **[How to create React App with Flask backend?](https://divyajyotiuk.hashnode.dev/how-to-create-react-app-with-flask-backend-ckfl971az02si5ds1h7qnabk9)**
- **[Exporting your Twitter bookmarks in markdown file](https://divyajyotiuk.hashnode.dev/exporting-your-twitter-bookmarks-in-markdown-file)**








