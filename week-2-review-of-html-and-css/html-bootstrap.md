# HTML Bootstrap

Assignment

Folder: Create this assignment in the “myFinalProject” folder

1. Break the index.html file from the basewebSite folder into several smaller files. The file can be broken up based on it’s logical components (i.e. the navigation bar, the header, the genre nav etc.)
2. Do any customizations you wish to the page such as color, shading, simple formatting etc. You do not need to go overboard but make the page your own in a small way.

## Introduction

The first thing we are going to do this class is a review of HTML and CSS which will also serve an introduction to the Bootstrap CSS library. We are also going to learn our first ColdFusion command which is in the “tag” format which is \<cfinclude>.

As I’m sure you know, since it’s a pre-requisite for the class, HTML and CSS are two “languages” which serve as the foundation of web design. HTML provides the structure for the site as a series of rectangular shapes which act as an outline for your page. CSS describes what each of those rectangular shapes look like including layout (height, width, and spatial relationship), formatting (color, border, text attributes and background images) and some programmatic issues (counting, insertion of other special elements) and more.

There are several pre-built libraries of CSS and JavaScript which are available for free on the internet for use by designers and developers in their web pages. One of these is the Bootstrap library located at[http://getbootstrap.com](http://getbootstrap.com). First developed by Twitter throughout the 2010s and made into an open source project in 2011, Bootstrap was completely overhauled with its release of v.3. The version was significant because the entire library was re-written as “mobile first” meaning that it accommodates all screen sizes such as tablets, smart phones, laptops, monitors, and mobile apps with responsive design which can render the page differently based on the available space. We will be using version 5.3.

Your assignment this week is to create the foundation of the index page of the bookstore web site which we are going to use the rest of the semester. In doing so, we’ll get a review of HTML, CSS and provide a way to learn how to incorporate the Bootstrap library into our projects. The key components we are going to explore are:

* The Bootstrap grid system consisting of rows and columns
* Side and Main Navigations
* Thumbnails
* Tables

Check out the week 2 documents in the “Codebase” section of the class website.

## Before You Start

* Make sure that you have completed setting up your work environment and the Connecting to Class Servers process. Each of you has your own space on the server at [comweb.uml.edu](http://comweb.uml.edu).
* Copy and paste the index.html file from basewebSite into your myFinalProject folder. **Rename it index.cfm**. We’re going to cut sections of the site out of this file and paste those sections into other files.

## Start Your Site

Note: Because of a difference in the folder structure on the class server and on the local development environment we set up, it is recommended that you make all link relative to the index page in your folder.

**Remember** – If you have never used a CSS library before, you have probably written your HTML and then written your CSS to stylize it. When you are using a library, the CSS is mostly written (except for the tweaks you do later). This means that you need to make your HTML classes and IDs match the rules that are already written in the library.

We are going to be end up with 6 pages for this exercise. index.cfm, header.cfm, horizontalnav.cfm, genrenav.cfm, carousel.cfm and footer.cfm. The reason for this is a development concept of keeping “chunks” of code as small as possible and as reusable as possible. We’ll get more into that but the big picture is that index.cfm is going to be a wrapper for the other 5 files. That will make more sense as we go.

.

## Using Built In developer Tools

Most of the modern browsers have built in tools that make inspecting what is happening with your page much easier. I use Chrome’s Developer Tools which you can access by pressing CTRL+SHIFT+i when the page is open in Chrome. This allows you to inspect the page’s HTML (or DOM), view the applied CSS rules, start and stop JavaScript scripts and see what elements or files loaded or failed to load. I’ll reference the developer tools throughout the class but there is no requirement to use Chrome. However, whichever you choose, become familiar with them and what tools and resources are available to you.

## Understanding the Site’s Basic Format

Bootstrap’s layout is based on a layout of rows and columns. Each row is meant to contain up to 12 columns in it. We can control how wide our columns are by using the built in CSS classes. For more detailed description of the grid system refer to the Bootstrap documentation here ([https://getbootstrap.com/docs/5.1/layout/grid/](https://getbootstrap.com/docs/5.1/layout/grid/)).

Because of the semantic tags in HTML5 we can break down the page into sections simply.

**Header**: this is bounded by the \<header>\</header> tag. Cut and paste this into header.cfm. In its place in index.cfm type \<cfinclude template=”header.cfm” />. Try opening index.cfm in a browser. Don’t forget you’ll need to have your CommandBox server started.

**Navigation**: this is bounded by the \<nav>\</nav> tag. Put this in horizontalnav.cfm. In its place leave \<cfinclude template=”horizontalnav.cfm” />. Try opening it in the browser.

**Main area**: this is bounded by the \<main>\</main> tag Leave this tag in index.cfm. Try opening it in the browser.

**Carousel**: this is the first \<section>\</section> tag. Put this into carousel.cfm. In its place leave \<cfinclude template=”carousel.cfm” />. Try opening it in the browser.

**Genre Nav**: this is the second \<section>\</section> tag. Put this in genrenav.cfm. In its place leave \<cfinclude template=”genrenav.cfm” />. Try opening it in the browser.

**Footer**: This is the \<footer>\</footer>. Put this in footer.cfm. In its place leave \<cfinclude template=”footer.cfm” />. Try opening it in the browser.

## Conclusion

This page is the start of the site we are going to build this semester. By the end of the 10 week course we will have used databases to autopopulate this page, created the other pages and their navigation systems, created a login and password system, used data from the databases to create the front carousel, have a detail page for more information about the books and more. For now, get the layout complete, check and make sure that the navigation collapses on smaller screens, the carousel works, and customize the page more to your liking.

Have fun!
