# wdio-webcomponents

wdio-webcomponents is a webdriver.io plugin which makes webdriver compatible with Open Shadow Roots. 

With the rise of Shadow DOM in webcomponent applications, we need a solution to test the components using Webdriver(Selenium). 


This is meant as a temporary solution until the people behind the WebDriver standard and the browser implementations can decide on a solution (discussion has been going on since 2014, untill this day, with no clear solution in sight).

## Installation
Install the npm lib:

`npm install wdio-webcomponents --save-dev`

Then add the plugin to your `wdio.conf` under plugins.

```javascript
{
    plugins: {
        'wdio-webcomponents': {}
    }
}
```

## Internal workings
The plugin works by replacing the `browser.element` and `browser.elements` command with another implementation. All other webdriver commands use these two functions, so overriding fixes it for all other commands.

It uses a Javascript function, sent to the browser, to find the correct element/elements in or outside of a Shadow DOM. The implementation is based on ChadKillingsworth's code, that can be found here: https://gist.github.com/ChadKillingsworth/d4cb3d30b9d7fbc3fd0af93c2a133a53

The code in this plugin has been modified to support more use cases, non-shadowroots and multiple element selection. You can find it in `src/finders/findElement.js`. 

## How to use
You can use it just like you normally use webdriver. However, it should be noted that the CSS selector should contain every element with a Shadow Root on the way, or it will not be able to find it.  