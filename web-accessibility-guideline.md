# The Ultimate Web Accessibility Guideline

#### I strongly suggest you to read this guideline thoroughly before developing. This will help you implementing web accessbility features without too much effort!

---

*Table of Contents*
  

  - [Best Practices on HTML Tags](#best-practices-on-html-tags)
    - [Text Content](#text-content)
    - [Always Communicate Clearly!](#always-communicate-clearly)
    - [Page Layouts](#page-layouts)
    - [Images](#images)
    - [UI controls](#ui-controls)
  
  - [ARIA (Accessible Rich Internet Applications) Attributes](#aria-accessible-rich-internet-applications-attributes)
  - [Skip to Main Content](#skip-to-main-content)
  - [onmouseover vs onfocus](#onmouseover-vs-onfocus)
  - [Tab Index](#tab-index)
  - [onkeydown](#onkeydown)
  - [Color Contrast](#color-contrast)
  - [Form Validation](#form-validation)
  - [Resources](#resources)
  
---

## Best Practices on HTML Tags 


`<div>` vs `<button>`

The fastest way to improve web page accessibility is to use the right HTML tags for the right task. **This means using the correct HTML elements for their intended purpose as much as possible.**

<span style="color:red">Don't:
```html
<div>Play</div>
```

<span style="color:orange"> Do:
```html
<button>Play</button>
```
```<button>``` supports built-in keyboard accessibility. 
Users can navigate between buttons using the ```tab ``` key and activate their selection using ```Return``` or ```Enter```.

<span style="color:red">Don't:
```html
<div class="header">
    <!--div Elements-->
</div>
```
<span style="color:orange"> Do:
```html
<header>
    <!--Header Elements-->
</header>
```
```<header>``` tags are intended to contain navigation elements like logos, links, and other introductory information. 
Using the more semantically accurate elements like ```<header>``` creates a more accessbile web pages for people using technology such as screen readers. 

---

### Text Content

Here is an excellent semantic example for content structure with headings, paragpraphs, lists, and etc.

```html
<h1>My heading</h1>

<p>This is the first section of my document.</p>

<ol>
    <li>This is</li>
    <li>a list for</li>
    <li>you to read</li>
</ol>

<h2>My subheading</h2>

<p>this is the first subsection of my document.</p>

<h2>My second subheading</h2>

<p>This is the second subsection of my content.</p>
```

1. The screen reader reads each header out as you progress through the content and it notifies you what a heading is, what is a paragraph, etc
2. It stops after each element, letting you go at whatever pace is comfortable for you.
3. You can jump to the next/previous heading in many screen readers.

---

### Always Communicate Clearly! 
* Don't use dashes. Write 5 to 7 instead of writing 5-7
* Expand abbreviations. Write January instead of writing Jan.

---

### Page Layouts 

Instead of using nested ```<div>``` elements, use appropriate sectioning elements to wrap your main navigation(```<nav>```), footer(```<footer>```), repeating content units(```<article>```), etc. These provide extra semantics for screen readers to give user extra clues about the content they are navigating.

Here is a good example of page layouts.

```html
<header>
  <h1>Header</h1>
</header>

<nav>
  <!-- main navigation in here -->
</nav>

<!-- Here is our page's main content -->
<main>

  <!-- It contains an article -->
  <article>
    <h2>Article heading</h2>

    <!-- article content in here -->
  </article>

  <aside>
    <h2>Related</h2>

    <!-- aside content in here -->
  </aside>

</main>

<!-- And here is our main footer that is used across all the pages of our website -->

<footer>
  <!-- footer content in here -->
</footer>
```
---

### Images 

All image elements must be provided with an ```alt``` attribute to ensure that a text description is available to be announced by screen readers.

*<span style="color:red">! it should not be containing 'image of' or 'picture of' unless the attached image is an image of the object.*

```html
<img src="traffic_lights.png" alt="traffic light with red stop signal">
```

* for image links, ```alt``` should describe the destination of the link, not the image content.

e.g. Company logo linking back to the hompage

```html
<img src="kmart.jpg" alt="Home - Kmart USA">
```



---


### UI controls 

Most commonly buttons, links, and form controls require interaction with users. Many semantic HMTL tags have built-in users interaction. 

 * Form

```html
<form>
  <div>
    <label for="name">Fill in your name:</label>
    <input type="text" id="name" name="name">
  </div>
  <div>
    <label for="age">Enter your age:</label>
    <input type="text" id="age" name="age">
  </div>
  <div>
    <label for="mood">Choose your mood:</label>
    <select id="mood" name="mood">
      <option>Happy</option>
      <option>Sad</option>
      <option>Angry</option>
      <option>Worried</option>
    </select>
  </div>
</form>
```
1.  ```<select>``` element can have its options displayed and cycled between using the up and down arrow keys **(Be sure to test the funcionality using the keyboard as you write a new page!)**  
   
2. ```<label>``` is required for every form control  
   
3. each ```<label>``` ```for``` attribute value needs to match the form element ```id``` value
   
4. Keyboard users may use the ```Tab```, ```Shift```, and ```Enter``` keys to navigate through forms(```Shift```+```Tab``` for backwards)
  

5. All form function should be available on keyboards
---
## ARIA (Accessible Rich Internet Applications) Attributes

* It is always recommended to use built-in semantic HTML elements to save time and extra work. However, when you need to go offroad and build your own control, ARIA can help you add in the semantics your new custom control is missing.


```html
<label>
    <input type="checkbox">
    Receive promotional offers
</label>
```
The screen reader will read
```
Checkbox
name: "Receive promotional offers"
state: checked (if it is checked)
```

But for some reasons, you need to use ```<div>``` to make a checkbox functionality. 

```html
<!--custom checkbox-->
<div class="checkbox checked">
    Receive promotional offers
</div>
```
The screen reader will read 
```
Text
value:"Receive promotional offers"
```
You can see how little context is given for users with the screen reader for the code snippet for the custom checkbox.

So, how can we improve this custom checkbox? Here is another code snippet that uses ```aria``` attributes and it functions just like a regular checkbox.


```html
...
<div tabindex="0" class="checkbox" checked role="checkbox" aria-checked="true">Option 1
</div>
<div tabindex="0" class="checkbox" role="checkbox" aria-checked="false">Option 2
</div>
```

By simply adding ```role=checkbox``` and ```aria-checked```, now my checkbox works just like ```<label>``` 

* ARIA can add, modify semantics

* ARIA can add extra labels and descriptions
  
```html
<button class="glyph"
aria-label="Filter"
>
    <div class="menu-glyph">
    </div>
</button>
```
* ARIA can also express relationships between different (or complex) elelements

```html
<button aria-expanded="false"
aria-controls="advanced-settings">
    <h2>Advanced Settings</h2>
</button>
<div id="advanced-settings">
    <label>
        <input type="checkbox">
            Offer to translate content
    </label>
</div>
```
By adding ```aria-controls```, button element controls the ```<div id="advanced-settings">```element 

* ARIA can also give live updates using ```role="alert"```

  
---
## Skip to Main Content

"Skip to Main Content", "Skip Navigation" links are extremely useful for keyboard users. For example, A Web page includes a variety of navigation techniques on each page: a bread crumb trail, a search tool, a site map, and a list of related resources. In this case, the first link on the page should be titled **"Skip to Main Content" to activate the link to skip over the navigation tools.** 

e.g. Users can skip navigation link to login. 

```Javascript
goToLoginInput = () = > {
    document.getElementById('username-field').focus()
}
//it focuses on the username input field that users can start type in username to login. 
...

return(
<a 
    class='skip-main'      href='javascript:undefined;'
    onClick={this.goToLoginInput}
    >Skip to Main Content</a>
)
```

The example above is written in React JS. 
in regular HTML, you will not need ```onClick```. You can put the ```class``` name that you want the users to go in ```href```. 

```href='javascript:undefined;'``` disables the page to go to the link that has been clicked because the user is not trying to go to the different page but different element. It is supported by ```onClick``` function. 

---

## onmouseover vs onfocus 


"onmouseover" attribute can be used to activate JavaScript and other forms of activity. Users can activate "onmouseover" by hovering over the assigned "onclick" element, but <span style="color:red">**it is not operable using the keyboard**.

"onfocus" attribute equivalent functionality by activating the effect when the interactive element receives **keyboard** focus.

```javascript
return(
    <input
    ...
    onFocus={e => {
        document.getElementById('element-id')
    }}>
)
```
---

## Tab Index

The HTML ```tabindex``` attribute is used to manage keyboard focus. Some semantic HTML tags have focus by default but if not, it is important to include ```tabindex``` attribute manually. 

* ```tabindex=0```
  
  The element is inserted into the tab order bsaed on its location in the source code. (basically, making the element focusable manually) 

* ```tabindex=-1```
  
  The element is not in the tab order but it is programmatically focusable.
  
  
* ```tabindex=1+```
  
  The element is on top of the tab order.


```tabindex``` example 
```html
...
<body>
<div>Not in the tab order</div>
<div tabindex="0">In the tab order</div>
<div tabindex="-1">Not in the tab order (but is focusable)</div>
<div tabindex="5">Ahead of everything in the tab order</div>

<script>
document.querySelector('[tabindex="-1"]').focus()
</script>
</body>
```
---

## onkeydown

The ```onkeydown``` event occurs when the user is pressing a key on the keyboard. 

Here is a code snippet on ```onkeydown``` implementation in React JS

```javascript
const handleIncreaseSpeed = (e) => {
    //speed increases when users press "space bar" down
    if (e.key === ' '){
        console.log('increasing speed')
        increaseSpeed();
    }
}

....

return(
    <div
    ...
    tabIndex='0' 
    onKeyDown={handleIncreaseSpeed}>
    ...
    </div>
)
```

Make sure to include ```tabIndex='0'``` to make the element focusable! 

---

## Color Contrast

* Text must have a **minimum** color contrast of over 4.5 to 1 with its background. The ratio of 3 to 1 is acceptable for **large text(14pt bold or 18pt)**. 

* Test your color contrast here: [color contrast checker](https://webaim.org/resources/contrastchecker)

*foreground color: text color

---

## Form Validation

* Make sure to include descriptive form labels.
* Errors associated with fields are helpful for users. 
* Alert screen reader users. 
  

Good example: 

<img src="formvalidation.png"
alt="Form Validation Example"
style="float: left; margin-right: 10px;" >

---

## Resources

* [General Usage of HTML semantics](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Cross_browser_testing/Accessibility#Using_native_keyboard_accessibility)
* [onmouseover vs onfocus](https://accessibility.iu.edu/creating-content/web-content/keyboard.html#:~:text=Users%20can%20activate%20%E2%80%9Conmouseover%E2%80%9D%20by,interactive%20element%20receives%20keyboard%20focus.)
* [4 Web Accessibility Best Practices](https://blog.prototypr.io/4-web-accessibility-best-practices-a0e957948bc5)
* [Using the tabindex attribute](https://developer.paciellogroup.com/blog/2014/08/using-the-tabindex-attribute/)
* [Controlling focus with tabindex](youtube.com/watch?v=Pe0Ce1WtnUM)
* [Intro to ARIA](https://www.youtube.com/watch?v=g9Qff0b-lHk&t=8s)
* EVT Codebase

