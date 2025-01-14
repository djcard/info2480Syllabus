---
description: >-
  Goal: By the end of this document, you'll have transformed a static index.html
  into several BoxLang template (.bxm) pages
---

# Making a Static Website Dynamic

Folder: Create this assignment in the “myFinalProject” folder

1. Break the index.html file from the basewebSite folder into several smaller files. The file can be broken up based on it’s logical components (i.e. the navigation bar, the header, the genre nav etc.)
2. Do any customizations you wish to the page such as color, shading, simple formatting etc. You do not need to go overboard but make the page your own in a small way.

## Introduction

The first thing we are going to do this class is a review of HTML and CSS which will also serve an introduction to the Bootstrap CSS library. We are also going to learn our first BoxLang command which is in the “tag” format which is \<bx:include>.

As I’m sure you know, since it’s a pre-requisite for the class, HTML and CSS are two “languages” which serve as the foundation of web design. HTML provides the structure for the site as a series of rectangular shapes which act as an outline for your page. CSS describes what each of those rectangular shapes look like including layout (height, width, and spatial relationship), formatting (color, border, text attributes and background images) and some programmatic issues (counting, insertion of other special elements) and more.

There are several pre-built libraries of CSS and JavaScript which are available for free on the internet for use by designers and developers in their web pages. One of these is the Bootstrap library located at [http://getbootstrap.com](http://getbootstrap.com). First developed by Twitter ( now x )  throughout the 2010s and made into an open source project in 2011, Bootstrap was completely overhauled with its release of v.3. The version was significant because the entire library was re-written as “mobile first” meaning that it accommodates all screen sizes such as tablets, smart phones, laptops, monitors, and mobile apps with responsive design which can render the page differently based on the available space. We will be using version 5.3.

Your assignment this week is to create the foundation of the index page of the bookstore web site which we are going to use the rest of the semester. In doing so, we’ll get a review of HTML, CSS and provide a way to learn how to incorporate the Bootstrap library into our projects. The key components we are going to explore are:

* The Bootstrap grid system consisting of rows and columns
* Side and Main Navigations
* Thumbnails
* Tables

## Before You Start

* Make sure that you have created the Week2 branch according to [Making Point In Time and Working Branches](making-point-of-time-and-working-branches.md).&#x20;

## Start Your Site

**Remember** – If you have never used a CSS library before, you have probably written your HTML and then written your CSS to stylize it. When you are using a library, the CSS is mostly written (except for the tweaks you do later). This means that you need to make your HTML classes and IDs match the rules that are already written in the library.

We are going to be end up with 6 pages for this exercise. `index.bxm`, `header.bxm`, `horizontalnav.bxm`, `genrenav.bxm`, `carousel.bxm` and `footer.bxm`. The reason for this is a development concept of keeping “chunks” of code as small as possible and as reusable as possible. We’ll get more into that but the big picture is that `index.bxm` is going to be a wrapper for the other 5 files. That will make more sense as we go..

## Using Built In developer Tools

Most of the modern browsers have built in tools that make inspecting what is happening with your page much easier. I use Chrome’s Developer Tools which you can access by pressing CTRL+SHIFT+i when the page is open in Chrome. This allows you to inspect the page’s HTML (or DOM), view the applied CSS rules, start and stop JavaScript scripts and see what elements or files loaded or failed to load. I’ll reference the developer tools throughout the class but there is no requirement to use Chrome. However, whichever you choose, become familiar with them and what tools and resources are available to you.

## Understanding the Site’s Basic Format

Bootstrap’s layout is based on a layout of rows and columns. Each row is meant to contain up to 12 columns in it. We can control how wide our columns are by using the built in CSS classes. For more detailed description of the grid system refer to the Bootstrap documentation here ([https://getbootstrap.com/docs/5.3/layout/grid/](https://getbootstrap.com/docs/5.3/layout/grid/)).

Because of the semantic tags in HTML5 we can break down the page into sections simply.

**Header**: this is bounded by the \<header>\</header> tag. Cut and paste this into header.bxm. In its place in index.bxm type \<bx:include template=”header.bxm” />. Try opening index.bxm in a browser. Don’t forget you’ll need to have your CommandBox server started.

**Navigation**: this is bounded by the \<nav>\</nav> tag. Put this in horizontalnav.bxm. In its place leave \<bx:include template=”horizontalnav.bxm” />. Try opening it in the browser.

**Main area**: this is bounded by the \<main>\</main> tag Leave this tag in index.bxm. Try opening it in the browser.

**Carousel**: this is inside the first \<section>\</section> tag. Put this into carousel.bxm. In its place leave \<bx:include template=”carousel.bxm” />. Try opening it in the browser.

**Genre Nav**: this is the second \<section>\</section> tag. Put this in genrenav.bxm. In its place leave \<bx:include template=”genrenav.bxm” />. Try opening it in the browser.

**Footer**: This is the \<footer>\</footer>. Put this in footer.bxm. In its place leave \<bx:include template=”footer.bxm” />. Try opening it in the browser.

## Conclusion

This page is the start of the site we are going to build this semester. By the end of the 10 week course we will have used databases to autopopulate this page, created the other pages and their navigation systems, created a login and password system, used data from the databases to create the front carousel, have a detail page for more information about the books and more. For now, get the layout complete, check and make sure that the navigation collapses on smaller screens, the carousel works, and customize the page more to your liking.

Have fun!
