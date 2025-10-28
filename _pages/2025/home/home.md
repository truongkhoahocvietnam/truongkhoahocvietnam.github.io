---
layout: page
title: "Home"
permalink: /vsss2025/home/
author_profile: true
---

<style>
  .home-container {
    text-align: center;
    font-family: sans-serif;
  }
  .main-heading {
    font-size: 2.5em;
    text-align: center;
    margin-top: 0.5em;
    margin-bottom: 0.2em;
  }
  .sub-heading {
    font-size: 1.2em;
    margin-bottom: 0.5em;
  }
  .date-location {
    margin-bottom: 1.5em;
  }
  .nav-button {
    display: inline-block;
    padding: 10px 20px;
    margin: 0 10px 20px 10px;
    background-color: #007bff;
    color: white;
    text-decoration: none;
    border-radius: 5px;
    border: none;
    cursor: pointer;
    font-size: 1em;
  }
  .nav-button:hover {
    background-color: #0056b3;
  }
  .home-image {
    max-width: 100%;
    height: auto;
    border-radius: 8px;
    margin-bottom: 2em;
  }
  .section {
    margin: 2em 0;
    text-align: justify;
  }
  .section img {
     max-width: 100%;
     height: auto;
     border-radius: 8px;
  }
  .section-button {
     margin-top: 1em;
  }
  .section ul {
     list-style-position: inside;
     text-align: justify;
     margin-bottom: 1.5em;
  }
  .section li {
     margin-bottom: 0.75em;
  }
  .numbered-list {
     list-style: none;          /* Remove default numbering */
     counter-reset: my-counter; /* Initialize a counter */
  }
  .numbered-list li::before {
     counter-increment: my-counter; /* Increment the counter for each list item */
     content: "(" counter(my-counter) ") "; /* Display the counter with parentheses */
     margin-right: 5px;      /* Add some space after the number */
     margin-bottom: 1.5em;
  }
</style>

<div class="home-container">

  <p class="sub-heading">
     12th Vietnam Summer School of Science
  </p>
  <h1 class="main-heading">
     Embrace the Unknown
  </h1>
  <p class="date-location">
     ICISE, Quy Nhon, Binh Dinh<br>August 5-8, 2025
  </p>

  <div>
    <a href="/vsss2025/about-us/VSSS/" class="nav-button">About VSSS</a>
    <a href="/vsss2025/others/faqs/" class="nav-button">FAQs</a>
  </div>

  <img src="/_pages/2025/home/home.jpg" alt="12th Vietnam Summer School of Science" class="home-image">

  <div class="section">
    <h2>
         Our Journey
    </h2>
    <p>
         The Vietnam Summer School of Science was established by a network of Vietnamese scientists working overseas to share the magic of science and inspire young students in their home country.
    </p>
    <img src="/_pages/2025/home/ourjourney.jpeg" alt="Students and lecturers at a past VSSS event">
    <div class="section-button">
        <a href="/vsss2025/about-us/VSSS/" class="nav-button">More About VSSS</a>
    </div>
  </div>
</div>
