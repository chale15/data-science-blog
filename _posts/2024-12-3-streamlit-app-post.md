---
layout: post
title:  "Sharing your Data"
date: 2024-12-3
description: Help others benefit from your data, because sharing is caring! 
image: 
display_image: false
---

<p class="intro"><span class="dropcap">U</span>ncovering NFL Trends with Interactive Data: A Dive into NFL Data with Streamlit</p>

### Introduction

Football season brings excitement not only to fans watching the games but also to data enthusiasts who want to explore how teams and players perform over time. In this blog post, I'll take you through a project where we explore key insights from the NFL dataset we created last time (<a href="https://chale15.github.io/data-science-blog/blog/data-collection-post/" target = "_blank">Link</a>) using a Streamlit app. 

The app allows users to interact with NFL data in meaningful ways, revealing trends and patterns that are often hidden in raw numbers. Whether you're a sports fan or a data science enthusiast, this app provides a simple and unique way to dive deeper into the world of professional football and easily visualize trends. 

---

### Motivating Question

<p class="tip-description">How have offensive player stats changed over the last few seasons?</p>

As an avid football watcher, I've noticed that in the last couple seasons, quarterback play has been much more inconsistent than in the past, and I wanted to find a good way further examine this percieved trend through data visualization. 

To do this, I decided to create a Streamlit app, which can be found at the link below. 


<div style="display: flex; justify-content: center; align-items: center;">
  <a href="https://nfl-data-chale15.streamlit.app" target = "_blank" style="text-decoration:none;">
    <button style="background-color:#079ED9; color:white; padding:10px 20px; border:none; border-radius:5px; font-size:16px;">
      Streamlit App
    </button>
  </a>
</div>


Additionally, all code used to create this app can be found <a href="https://github.com/chale15/NFL_Data_App" target = "_blank">here</a>.

---

### Introducing the Streamlit App: Your Interactive Guide to NFL Data

The purpose of this Streamlit app is to give users an intuitive and interactive way to explore the NFL dataset. It offers various visualizations that allow users to dive deep into statistics, league performance, and individual player metrics. Whether you're a sports analyst, a fan, or a data scientist, this app can provide a wealth of insights.

---

### Key App Features:

**Interactive Visualizations**: Users can interact with different charts, filtering by teams, players, and seasons. This makes it easy to see how a particular team's or player's performance changes over time. Additionally, as the majority of plots are created using plotly express, hovering over elements of a chart can provided more detailed data. 
   
**Player Comparison**: The app allows users to compare players' stats over multiple seasons, helping to identify top performers and trends. For example, comparing quarterbacks based on passing yards, touchdowns, and interceptions across multiple seasons.

**Dynamic Filters**: The app offers dynamic filters where users can select specific metrics or seasons to narrow down their analysis. This allows users to explore the data in a variety of ways, depending on their questions or interests.

**Intuitive Navigation**: Easily navigate this app using the sidebar menu to change pages and tabs to explore different visualizations!

<p align="center">
    <img src="{{site.url}}/{{site.baseurl}}/assets/img/app.png" alt="App" width="90%">
</p>

---

#### How Users Can Explore the Data:
  
**Explore League Trends**: Pick a statistic to visualize how overall league performance in that metric has changed over time, or display the best players in regard to that statistic for desired seasons
  
**Compare Players**: Compare players based on key performance metrics to see which ones have been most successful, including visualizing that comparison over multiple seasons

---

### Key Insights: Player Performance Trends Over Time

A fascinating insight through this app comes from analyzing individual player statistics over multiple seasons. Despite still having a few elite quarterbacks, over the last couple seasons there has been a consistant decline in the overall number of and quality of play by the quarterbacks who are just *good*. 

<p align="center">
    <img src="{{site.url}}/{{site.baseurl}}/assets/img/qbr.png" alt="QBR" width="90%">
</p>

Despit showing a slight negative trend in average (mean and median) quarterback ratings from the 2020 season to the 2024 season, there was a jump in the max ratings, indicating a greater spread in our data, with more poor quarterbacks balancing out the improved play of a few elite players. 

Backup quarterbacks are also playing more than ever before, as teams seem more willing to bench a quarterback after one or two poor performances than they have in the past, leading to a less clear divide between classifications of quarterbacks. 

<p align="center">
  <img src="{{site.url}}/{{site.baseurl}}/assets/img/2020_yards.png" alt="2020 Yards" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img src="{{site.url}}/{{site.baseurl}}/assets/img/2024_yards.png" alt="2024 Yards" width="45%">
</p>

From these graphs, we can clearly see several drops in our 2020 data, indicative of natural boundaries in quarterback skills. These drops become less pronounced in the 2024 data however, and as a whole, the data reflects a much smoother linear trend. 

---

### Conclusion: Dive Deeper into NFL Data with the Streamlit App

In this blog post, we've explored several key relationships, such as changes in league trends over time and the distributions of stat leaders. We've barely scratched the surface however, and the true beauty of this dataset lies in how much more you can discover by exploring the data interactively through the Streamlit app.

I encourage you to dive into the app yourself and see what you can uncover. Whether you're interested in league dynamics, player trends, or game statistics, the app offers a powerful tool for exploring NFL data in ways that go beyond simple box scores.

Once again, you can access the Streamlit app <a href="https://nfl-data-chale15.streamlit.app" target = "_blank">here</a>, and for the full code and further exploration, check out the GitHub repository <a href="https://github.com/chale15/NFL_Data_App" target = "_blank">here</a>.

What insights did you discover when exploring the data? Feel free to leave a comment and share your findings! Let’s keep the conversation going!

---