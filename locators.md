!SLIDE

# CSS Locators
<http://bit.ly/cssxpath>

Santiago Suarez Ordoñez

[@santiycr](http://twitter.com/santiycr)

[Sauce Labs](http://saucelabs.com)

!SLIDE

## What are locators?

locators are a way to tell selenium which specific element we want it to act on

!SLIDE


## Agenda

* Why you should use CSS locators
* Understanding CSS locators
* When not to use CSS locators
* Useful tools

!SLIDE

## Why to use CSS locators?

!SLIDE

* Because they are faster
* Because they are more readable
* Because CSS is jQuery's locating strategy
* Because no one else uses XPATH anyways!

!SLIDE

#### Faster?

Only on IE. Check the results from a small measuring script I made: <https://gist.github.com/963821>

<br />

**Highlights**:

* Firefox, Chrome, Opera, Safari: times are fairly similar (generally bellow 0.05 seconds, which is acceptable within Selenium tests)
* IE, not so much :,(

!SLIDE

<small>
@@@ js

browser         |     IE6    |     IE7    |     IE8    |     IE9    |
----------------|------------|------------|------------|------------|
locator:        | CSS  | XPT | CSS  | XPT | CSS  | XPT | CSS  | XPT |
----------------|------|-----|------|-----|------|-----|------|-----|
Relative ID     | 0.09 | 17  | 0.08 | 15  | 0.10 | 17  | 0.09 | 30  |
Relative Class  | 12   | 16  | 13   | 15  | 13   | 17  | 22   | 30  |
Relative Content| 13   | 17  | 14   | 17  | 16   | 18  | 27   | 32  |
Relative Name   | 0.1  | 16  | 0.11 | 15  | 0.11 | 17  | 0.09 | 29  |

@@@

<br />

Absolute versions are an order of magnitude faster (0.1 vs 1)

<br />

Want to see the difference in action? <https://saucelabs.com/jobs/8eca38f844ffbc91336eddefad84177e>
</small>

!SLIDE

#### More readable?

@@@ css

//input[@id="myId"] vs input#myId

//input[@class="myClass"] vs input.myClass

//input[@name="myName"] vs input[name=myName]

//*[@id="myId"] vs #myId

//table[@id="myId"]//tr[@class="myClass"]//td[3]
vs
table#myId tr.myClass td:nth(3)

@@@

!SLIDE

#### Because jQuery uses CSS (Sizzle)

![jquery marketshare](http://farm3.static.flickr.com/2790/4465177118_bfa8845239_o.png)

<small>jQuery usage graph from [BuiltWith.](http://trends.builtwith.com/javascript/JQuery)</small>

!SLIDE

#### Because no one uses XPATH anyways

!SLIDE

## Understanding CSS

!SLIDE

#### The Basics

@@@ css
  div /\* This is selecting a node \*/
  ""   /\* No tag for "any tag" \*/
  table > tr /\* Direct child \*/
  table td /\* Child or Subchild \*/
  #myId /\* ID \*/
  .myClass /\* Class \*/
  [name=myName] /\* Attribute \*/
  tr:nth(5) /\* nth element \*/
  a.myClass#myId[name=myName] /\* Chain them! \*/
@@@

!SLIDE

#### The Powerful

@@@ css
  a[id^='id_prefix_']
  a[id$='_id_sufix']
  a[id*='id_pattern'] /\* Attribute Sub-patterns \*/
  a:contains('Log Out') /\* Inner text \*/
  div:not(.hidden) /\* Filter out \*/
  :header /\* All types of headers \*/
  :input /\* All inputs (textareas, selects, buttons) \*/
@@@

!SLIDE

## When not to use CSS locators?

!SLIDE

#### Bottom up navigation

<small>
@@@ css

id("user1")/../../td[@class="actions"]/a[@class="delete-user"]

@@@
</small>

<br/>

<table style="margin-left:20px;font-size:18px" border="1">
<tr><th>Users</th><th>Random content</th><th>Actions</th></tr>
<tr><td style="padding:5px">user1</td><td style="padding:5px">askdf asdlkfjasldfj asdf</td><td style="padding:5px"><a href="#">Delete</a> <a href="#">Update</a></td></tr>
<tr><td style="padding:5px">user2</td><td style="padding:5px">alskdfjaskdfjaskdfj</td><td style="padding:5px"><a href="#">Delete</a> <a href="#">Update</a></td></tr>
<tr><td style="padding:5px">user3</td><td style="padding:5px">asdfkajsdf asldfkj asdfklj</td><td style="padding:5px"><a href="#">Delete</a> <a href="#">Update</a></td></tr>
<tr><td style="padding:5px">user4</td><td style="padding:5px">asdkfj lkjocixvjzoxicvu i</td><td style="padding:5px"><a href="#">Delete</a> <a href="#">Update</a></td></tr>
</table>

!SLIDE

#### Selenium 2

@@@ java
  // Selenium 1
  browser.type("#menu [name=search]", "Hello, WebDriver");
  browser.click("#menu a:contains(Home)");
  
  // Selenium 2
  WebElement menu = driver.findElement(By.id("menu"));
  WebElement search = menu.findElement(By.name("search"));
  search.sendKeys("Hello, WebDriver");
  WebElement home = menu.findElement(By.linkText("Home"));
  home.click();
@@@

!SLIDE

## References

* [Start Improving your locators](http://saucelabs.com/blog/index.php/2009/10/selenium-tip-of-the-week-start-improving-your-locators/)
* [Sizzle and special locators](http://saucelabs.com/blog/index.php/2011/01/why-jquery-in-selenium-css-locators-is-the-way-to-go/)
* [CSS locators demystified](http://saucelabs.com/blog/index.php/2010/01/selenium-totw-css-selectors-in-selenium-demystified/)
* [CSS Quick Reference](http://saucelabs.com/downloads/documentation/css-selector-quickreference.pdf)

!SLIDE

## Useful Tools

* [Selenium IDE](http://seleniumhq.org/download/)
* [cssify](https://github.com/santiycr/cssify)
* [Firebug](http://getfirebug.com/)
* [Selector Gadget](http://www.selectorgadget.com/)

!SLIDE

# Questions?

!SLIDE

# Thank you!

<http://bit.ly/cssxpath>

[@santiycr](http://twitter.com/santiycr)
