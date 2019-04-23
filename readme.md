# X - Components and Forms

The Master branch of this repo is where we left off in session 8. The Master branch is being deployed to Netlify.

## Exercise continued - Site Redesign

Here is where we left off in session 10 - https://session10.netlify.com

Log in to Github ** _Download the zip file_ ** 
Create a new empty repo.

`cd` into `component-inclass-master` and initialize a repository:

```sh
$ git init
$ git add .
$ git commit -m 'initial commit'
$ git remote add origin <your-github-repo>
$ git push -u origin master
```

Install dependencies and run the application.

```sh
npm i
npm start
```

## Deployment

We'll use [Netlify](https://www.netlify.com/). 

Log in to [app.netlify.com](https://app.netlify.com), click "New site from Git" and create a new site.

Set up Netlify to allow continuous deployment on the Master branch of your Github repo.

* use the terminal to create and checkout a new branch

```sh
$ git status 
$ git branch dev
$ git checkout dev
```

In the future you will be able to merge your dev branch into the master branch to have your site deployed.

E.g. from the dev branch:

```sh
$ git status 
$ git add .
$ git commit -m 'commit message'
$ git checkout master
$ git merge dev
$ git push -u origin master
```

Be sure to run `git status` before switching or merging branches.

## Refactoring Components

Review the interdependencies between content (the pages folder) and layouts.

## Forms

Use the following in the `contact.html` component:

```html
<form name="contact" method="POST" action="/" autocomplete="true">
<fieldset>
  
  <input type="text" name="name" id="name" required autocomplete = "off" />
  <label for="name">Your name</label>
 
  <input type="email" name="email" id="email" required autocomplete = "off"   />
   <label for="email">Email address</label>

  
  <textarea name="message" id="message" placeholder="Your message" rows="7"></textarea>
  <label for="message">Your message</label>
  <button type="submit" name="submit">Send Message</button>
  </fieldset>
</form>
```

Bring the form into the layout via `contact.md`:

```yml
---
layout: layouts/contact.html
pageTitle: Contact Us
navTitle: Contact
date: 2019-04-01
---
```

and `layouts/video.html`:

```yml
---
layout: layouts/layout.html
---

{% include components/video-article.html %}

{{ content }}
```


`form`:

* action - Specifies where to send the form-data when a form is submitted
* autocomplete - Specifies whether a form should have autocomplete on or off
* method - Specifies the HTTP method to use when sending form-data
* name - Specifies the name of a form
* novalidate - turns validation off, typically used when you provide your own custom validations routines

`fieldset`: not really needed here. Allows the form to be split into multiple sections (e.g. shipping, billing)

`label`: The for attribute of the `<label>` tag should be equal to the id attribute of the related element to bind them together

`input`: Specifies an input field where the user can enter data. Is empty and consists of attributes only.

* can accept autocomplete and autofocus
* name - Specifies the name of an <input> element used to reference elements in a JavaScript, or to reference form data after a form is submitted
* type - the [most complex](https://www.w3schools.com/tags/att_input_type.asp) attribute, determines the nature of the input
* required - works with native HTML5 validation
* placeholder - the text the user sees before typing
* pattern - Specify a [regular expression](https://www.w3schools.com/TAGS/att_input_pattern.asp) that the `<input>` element's value is checked against on form submission
* title - use with pattern to specify extra information about an element, not form specific, often shown as a tooltip text, here - describes the pattern to help the user

Initial CSS:

```css
form {
  display: grid;
  padding: 2em 0;
}

form label {
  display: none;
}

input,
textarea,
button {
  width: 100%;
  padding: 1em;
  margin-bottom: 1em;
  font-size: 1rem;
}

input,
textarea {
  border: 1px solid #666;
}

button {
  border: 1px solid $link;
  background-color: $link;
  color: #fff;
  cursor: pointer;
}
```

Ender:

```html
<form name="contact" method="POST" data-netlify="true" action="/">
<fieldset>
  
  <input type="text" name="name" id="name" autocomplete="name" title="Please enter your name" required />
  <label for="name">Name</label>

  <input type="email" name="email" id="email" autocomplete="email" title="The domain portion of the email address is invalid (the portion after the @)." pattern="^([^\x00-\x20\x22\x28\x29\x2c\x2e\x3a-\x3c\x3e\x40\x5b-\x5d\x7f-\xff]+|\x22([^\x0d\x22\x5c\x80-\xff]|\x5c[\x00-\x7f])*\x22)(\x2e([^\x00-\x20\x22\x28\x29\x2c\x2e\x3a-\x3c\x3e\x40\x5b-\x5d\x7f-\xff]+|\x22([^\x0d\x22\x5c\x80-\xff]|\x5c[\x00-\x7f])*\x22))*\x40([^\x00-\x20\x22\x28\x29\x2c\x2e\x3a-\x3c\x3e\x40\x5b-\x5d\x7f-\xff]+|\x5b([^\x0d\x5b-\x5d\x80-\xff]|\x5c[\x00-\x7f])*\x5d)(\x2e([^\x00-\x20\x22\x28\x29\x2c\x2e\x3a-\x3c\x3e\x40\x5b-\x5d\x7f-\xff]+|\x5b([^\x0d\x5b-\x5d\x80-\xff]|\x5c[\x00-\x7f])*\x5d))*(\.\w{2,})+$" required />
    <label for="email">Email</label>

  <textarea name="message" id="message" placeholder="Write your message here" rows="7" required></textarea>
  <label for="message">Message</label>
  
  <button type="submit" name="submit">Send Message</button>
  </fieldset>
</form>
```

Try:

`autocomplete="off"`

Label effect:

```css
form {
  display: grid;
  padding: 2em 0;
  display: block;
  position: relative;
}

form label {
  display: block;
  position: relative;
  top: -42px;
  left: 16px;
  font-size: 16px;
  z-index: 1;
  transition: all 0.3s ease-out;
}

input:focus + label, input:valid + label{
  top: -80px;
  font-size: 0.875rem;
  color: #00aced;
}

input,
textarea,
button {
  width: 100%;
  padding: 1em;
  margin-bottom: 1em;
  font-size: 1rem;
}

input {
  display: block;
  position: relative;
  background: none;
  border: none;
  border-bottom: 1px solid $link;
  font-weight: bold;
  font-size: 16px;
  z-index: 2;
}

textarea {
  border: 1px solid $link;
}
textarea + label {
  display: none;
}
textarea:focus {
  outline: none;
}

input:focus, input:valid{
  outline: none;
  border-bottom: 1px solid $link;
}

button {
  border: 1px solid $link;
  background-color: $link;
  color: #fff;
  cursor: pointer;
}
```

https://www.netlify.com/docs/form-handling/

`data-netlify="true"`

Component: `contact.html`

Page: `contact.md`

```md
---
layout: layouts/contact.html
pageTitle: Contact Us
navTitle: Contact
date: 2019-04-01
---

[Home](/)
```

Layout: `contact.html`

```html
---
layout: layouts/layout.html
---

{% include components/contact.html %}
```

## Content Management

[Headless CMS](https://en.wikipedia.org/wiki/Headless_content_management_system) - a back-end only content management system built from the ground up as a content repository that makes content accessible via a RESTful API for display on any device.

[Netlify CMS](https://www.netlifycms.org/)

https://www.netlifycms.org/docs/add-to-your-site/

https://templates.netlify.com/template/eleventy-netlify-boilerplate/#about-deploy-to-netlify
https://github.com/danurbanowicz/eleventy-netlify-boilerplate/blob/master/admin/preview-templates/index.js

## Notes

js ajax and localstorage

prefetching and rendering the data


