## Safari CSS hack

Browsers have their own way of interpreting code. There isn't any universal browser as such. Well, it depends on people's choice! 
A good web developer should always check the responsiveness and compatibility of their code on various devices and whether the website is working as expected. While developing website, I came across Safari behaving differently.

Well, on searching I did find that Safari does not support
```css
position: sticky;
```
but works with 
```css
position: -webkit-sticky;
```
since Webkit is the HTML/CSS rendering engine for Apple/Safari. 

Also Safari has some problem with
```css
overflow: hidden;
```
as well. When you search you'll find various people trying to provide solution for this.

Getting frustrated, I tried to find CSS hack for Safari and came across this on [stackoverflow](https://stackoverflow.com/questions/16348489/is-there-a-css-hack-for-safari-only-not-chrome).

```css
/* Only Safari 10.1+ */
@media not all and (min-resolution:.001dpcm)
{ @supports (-webkit-appearance:none) {

    .footer-text { 

        color:#0000FF; 
        background-color:#CCCCCC; 

    }
}}
```

I found this solution working for me. 

But this is **NOT** a _recommended_ solution. You should be able to write perfect code for all types of browsers and do extensive testing so that your website never breaks!