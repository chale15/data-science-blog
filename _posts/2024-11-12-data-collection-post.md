---
layout: post
title:  "Diving into Data Collection"
date: 2024-11-12
description: Turn the internet into YOUR personal dataset with Web Scraping!  
image: 
display_image: false
---

<p class="intro"><span class="dropcap">L</span>earn how to access any data you want with two easy to use Python Packages.</p>

### Introduction

<p class="tip-description">What is Web Scraping, and why do we use it?
</p>

So you're ready to trade your kiddie pool of curated datasets for the ocean of information available through the Internet! It's exciting and intimidating at the same time. And while mastering the art of data collection takes years, you can learn the basics in just a few short minutes with the help of two easy-to-use Python Packages: Beautiful Soup and Selenium. 

But first, what is web scraping? Generally speaking, web scraping is a technique you can use to extract information from a website. If you've ever copy and pasted information from online, you've webscraped without realizing it! For our purposes however, we'll use webscraping to refer to a more methodical, structured, and most importantly, automated approach do data collection. Let's say you want to use a table on Wikipedia for further analysis. With web scraping, you can obtain that information in an ready-to-use format almost instantaneously. What if you want to try out a new recipe, but don't want to worry about scrolling past pop-up ads and personal anecdotes? With web scraping, you can cut out the fluff and jump straight to the data. And how about when you have a question you want to answer through research, but a quick Google search doesn't come up with any relevant datasets? Now you don't have to leave your question unanswered; you can curate a dataset specifically to the topic at hand!

Throughout this post, I'll take you with me through a question I had, and introduce you to basic techniques that you can apply to answer questions of your own!

------------------------------------------------------------------------

### Motivating Question

<p class="tip-description">

In American Football, does a Quarterbacks' ability to run with the ball negatively affect Reciever performance?

</p>

Before we dive into the question at hand, I'll preface that this article _will_ include football terms, and a basic understanding of the sport will likely come in handy. I've attached a quick guide below. 

<a href="https://usasports.co.uk/blogs/blog/a-beginners-guide-to-american-football-and-the-nfl?srsltid=AfmBOopndDwlgsvt01xaVEIIp0gPuECjvfRV_hSA737oPLnDQ9wtoX0i" target="_blank">Guide</a>

Anyways, as I was watching football one evening, and lamenting the decline of the once-great Patriots dynasty, the announcer made an interesting comment about how the performance of one of the top recievers in the NFL had suffered on a new team because of his mobile quarterback. Looking past the logical fallacy of correlation equalling causation, I decided to collect my own data to either confirm or deny the announcer's opinion. 

------------------------------------------------------------------------

### Finding Your Data

In order to collect data, you first have to find it. Fortunately for me and my question I didn't have to search too hard, as the NFL tracks and makes player, team, and many other statistics available on their website, <a href="https://www.nfl.com/stats/player-stats/" target="_blank">NFL.com/stats</a>. Specifically, I decided that I wanted to use the 'Stat Leaders' table, as well as statistics located on individual player pages to answer my question. 

<img src="{{site.url}}/{{site.baseurl}}/assets/img/nfl_home_page.png" alt="NFL Home Page" />

As you can see, this page has a lot going on, but with the handy inspect element tool, I was able to find the information I needed buried within more HTML tags and divisions than they could possibly need. For an introduction to HTML and inspect element, check out this <a href="https://www.youtube.com/watch?v=TUpsyv9A9vU" target="_blank">video!</a>

------------------------------------------------------------------------

### Should You Use Your Data?

Once you've found your data, it's easy to get excited and skip straight to scraping. One of the most important steps in the process however, and one that often gets forgotten, is to decide whether your data can be obtained ethically. Typically, websites will have a 'robots.txt' file that outlines permitted use of data on that site. Sometimes sites don't want individual users to use their information, and it's important to respect their wishes, and find a different source to collect your data. The site might also ask that you build a delay into your web scraping code to not overwhelm their servers, and if you ignore this request, they can prohibit you from collecting data. The very first website I tried to scrape had a limiting feature built in, and because I didn't know about ethical use or the importance of checking the 'robots.txt' file, I ended up getting banned from the site and had to find my data elsewhere. For more information about the ethics governing web scraping and the 'robots.txt' file, <a href="https://brightdata.com/blog/how-tos/robots-txt-for-web-scraping-guide" target="_blank">this blog</a> explains it well.

Fortunately for us, the NFL gives us almost universal access to scrape, as seen in their 'robots.txt' file below.

<img src="{{site.url}}/{{site.baseurl}}/assets/img/nfl_robots.png" alt="NFL robots.txt" />

The only thing that affects us is the very last line, which prohibits users from scraping information about former players who are now involved in League Operations in a media, analyst, or management capacity, such as Tom Brady or Matt Ryan. Fortunately, this only prevents us from accessing a small amount of information, and now that we've determined that we **should** use this data, we need to figure out **how** to obtain it. 

------------------------------------------------------------------------

### Choosing the Right Tool

Well, we've officially made it to the hardest part of the whole process: getting our data into a form we can use. I'll be using a Jupyter Notebook to work through the process, and you can access my code and final results at the github link below. 

<div style="display: flex; justify-content: center; align-items: center;">
  <a href="https://github.com/chale15/NFL_Data/" style="text-decoration:none;">
    <button style="background-color:#2dba4e; color:white; padding:10px 20px; border:none; border-radius:5px; font-size:16px;">
      GitHub Repository
    </button>
  </a>
</div>
\


We also have to figure out which package will be the best for our purposes. The two major packages for web scraping in Python are *Beautiful Soup* and *Selenium*. Beautiful Soup is a much more lightweight, easy to use package, making it ideal for simpler web scraping tasks, although it is more limited in scope and features than Selenium. Beautiful Soup works in tandem with the Requests package, allowing you to collect the entirety of a website as text in JSON or HTML form, and from there, filter down that text object within your coding environment to obtain the information you want without having to interact further with the website. Generally speaking, you want to use Beautiful Soup and Requests to obtain data as often as you possible. A good rule of thumb is if there's nothing that forces you to use Selenium, use Beautiful Soup. 

Selenium, on the other hand, is much more powerful, much less intuitive, and much more demanding on your machine. It functions by imitating your browser, but is fully automated, allowing you to click on links, select search filters from a dropdown menu, and do anything else you would normally do manually, all without lifting a finger. Generally speaking, Selenium is the right choice if you have to interact with the website in some way to access your data, such as if you have to click a button to view the second page of a table.

For further reading on these libraries, check out the guides below:

<a href="https://realpython.com/python-requests/" target="_blank">Requests</a>\t<a href="https://realpython.com/beautiful-soup-web-scraper-python/" target="_blank">BeautifulSoup</a>\t<a href="https://www.simplilearn.com/tutorials/python-tutorial/selenium-with-python" target="_blank">Selenium</a>


For our data, there's some good news and bad news. The bad news is that interacting with the website as we scrape will make our lives considerably easier, so we have to use Selenium. The good news is that we don't need Selenium for everything, so we get to use a mix of the two packages to collect our data! Let's jump into the code!

------------------------------------------------------------------------

### The Code

As is good practice, we start by loading in the everything we need. For this project, I ended up using pandas, requests, BeautifulSoup, time, and re, but every project is slightly different and might require different tools. I also loaded in some Selenium specific functions, most of which I didn't end up needing, but that are good to have just in case. In order to use Selenium, you have to specify which browswer the tool will work through, and load the appropriate webdriver. I use Safari but you can easily modify the code to use whichever browser you prefer. 

#### Import General Packages

{%- highlight python -%} 
    ## Import General Packages

    import pandas as pd
    import numpy as np
    import requests
    from bs4 import BeautifulSoup
    import time
    import re


    ## Import Selenium Specific Functions

    from selenium import webdriver
    from selenium.webdriver.common.by import By
    from selenium.webdriver.safari.service import Service as SafariService
    from selenium.webdriver.support.ui import WebDriverWait
    from selenium.webdriver.support import expected_conditions as EC 
{%- endhighlight -%}


After importing my packages, I had to figure out how I wanted to assemble my dataset. Like most programming tasks, there's many different ways to arrive at the same solution, so use whatever approach makes sense for you. My method might not have been the most effecient or the prettiest, but it gave me usable data, which is the most important part.

I wanted to collect data spanning several years, so all of my code is nestled within loops. I also decided pretty early on that I didn't want to have all my data in one dataset, and although this may be a controversial approach, I believe it makes sense in the context of the question. To include everything together, I would have had to pivot the dataframe on key features, transforming it into a form averse to analysis. By storing my data for Quarterbacks and Recievers separately, I was able to avoid this issue altogether, and the data can easily be joined together, or filtered, depending on the demands of the analysis. Because I chose to keep my data separate, the process for building each dataset is very similar, so I'll just walk through the creation of the Quarterback stats dataset. 


#### Initialize Selenium

{%- highlight python -%} 
    try:
    driver.quit()
except:
    print("No Driver")

link = 'https://www.nfl.com/stats/player-stats/category/passing/' +str(2024 - i) +'/reg/all/passingyards/desc'
driver = webdriver.Safari(service=SafariService())
driver.get(link) 
{%- endhighlight -%}

While simple, these few lines of code are among the most important, because this is where I initialize Selenium. Once these lines have been run the automated browser is active, and will interact with your website however you tell it to. From here, my code tells the automated browser to search through the HTML until it finds what we want. In this case, we want the table with all the Quarterback information on it. 


#### Scrape Data with Selenium

{%- highlight python -%} 
    while True:
    try:
        container = driver.find_element(By.CLASS_NAME, 'nfl-c-player-directory')
        all_qbs = container.find_elements(By.XPATH, ".//tbody/tr")
    except:
        break

    for player in all_qbs:
        stats = player.find_elements(By.XPATH, "./td")
        #years1.append(2024-i)
        qbs.append(stats[0].text.strip())
        names1.append(stats[0].text.strip())
        qb_yards.append(stats[1].text.strip())
        qb_att.append(stats[3].text.strip())
        qb_ypa.append(stats[2].text.strip())
        qb_cmp.append(stats[4].text.strip())
        qb_td.append(stats[6].text.strip())
        qb_int.append(stats[7].text.strip())
        qb_rate.append(stats[8].text.strip())
        qb_sack.append(stats[14].text.strip())

    try:
        next_button = container.find_element(By.XPATH, './/a[@class="nfl-o-table-pagination__next"]')
        next_button.click()
        time.sleep(2)

    except:
        break 
{%- endhighlight -%}

Once it has found the table, it locates the individual rows, each of which represent a different player, and adds that player's data for each of the key stats into a list. Essentially, we're building the columns of our dataframe simultaneously. Once we have all the information we want, we'll combine them into one big dataset, but we're not there yet. 

Unfortunately, the table only shows 25 players at a time, which is why we have to use Selenium. Once we've gathered everything from the first 25 players, our browser clicks a button to move to the next page of results. We scrape this data, and the process repeats until there's no more buttons to push, and we know that we've scraped the entire table. 

Now that we've gotten everything we want from this main table, we need to get some data from individual player sites. To do this, we find the specific url for each player by transforming their name into the proper format using regular expressions. Now, we get to use our requests library and Beautiful Soup!


#### Scrape Data with Beautiful Soup

{%- highlight python -%} 
    for qb in qbs:
    qb_name = re.sub('[^a-zA-Z]+','-', qb)
    url = 'https://www.nfl.com/players/' + qb_name + '/stats/career'
    #print(url.replace('-/','/'))
    r = requests.get(url.replace('-/','/'))
    bs = BeautifulSoup(r.text)
    try:
        rush = bs.find_all('div', {'class':'nfl-o-roster'})[1].find('tbody').find_all('tr')
        stats = yearMatch(str(2024-i), rush)
    except:
        continue
    names.append(qb)
    years.append(stats[0].text.strip())
    teams.append(stats[1].text.strip())
    games.append(stats[2].text.strip())
    r_atts.append(stats[3].text.strip())
    r_yds.append(stats[4].text.strip())
    ypc.append(stats[5].text.strip())
    r_tds.append(stats[7].text.strip())
{%- endhighlight -%}

For each player in our original list of names, we send a request to their personal information page and use Beautiful soup to extract the information we want, in this case their team, the number of games they played, and their rushing statistics.

Once we have everything we want, we save it away, wipe the lists we're using as temporary storage, and the process repeats for the next year we want to get information from. 


#### Compile Dataset

{%- highlight python -%} 
    i += 1

pass_df = pd.DataFrame({'QB':names1, 'YDS':qb_yards, 'ATT':qb_att, 'YPA':qb_ypa, 'CMP':qb_cmp, 'TDs':qb_td, 'INTs':qb_int, 'QBR':qb_rate, 'SCK':qb_sack})
rush_df = pd.DataFrame({'QB':names, 'Team':teams, 'GP':games, 'Year':years, 'ATT(R)':r_atts, 'YDS(R)':r_yds, 'YPC':ypc, 'TDs(R)':r_tds})
qb_df = pd.merge(rush_df, pass_df, on='QB')
df = pd.concat([df, qb_df], ignore_index=True)

names1 = []
names = []
teams = []
games = []
years = []
r_atts = []
r_yds = []
ypc = []
r_tds = []
qbs = []
qb_yards = []
qb_att = []
qb_ypa = []
qb_cmp = []
qb_td = []
qb_int = []
qb_rate = []
qb_sack = []
{%- endhighlight -%}

After all of our loops have finished running, all that's left to do is to quit Selenium, fix a quick error, and write our data to a csv file. Because of how I created my code, some data ends up duplicating. Normally, this would mean I would have to completely rewrite my code, and approach this task a different way. Since web scraping is (mostly) all about the result and not about the product, however, a simple pd.drop_duplicates function gets us our desired final dataset with considerably less stress. Is it good coding practice? Maybe not, but it works for us!


#### Save Dataset
{%- highlight python -%} 
    driver.quit()
df = df.drop_duplicates(ignore_index=True)
df.to_csv('./qb_data.csv')
{%- endhighlight -%}

And there we have it! A successfully scraped quarterback stats dataset!

(As previously mentioned, the process for scraping wide reciever data is nearly identical, and is included in the <a href="https://github.com/chale15/NFL_Data/blob/main/nfl_data.ipynb" target="_blank">'nfl_data.ipynb'</a> file on GitHub)

------------------------------------------------------------------------

### EDA (Exploring Da Associations)

Great! Now the hard part is done, and we have some new data to explore! Let's take a look at our datasets

First, the Quarterback data:

<img src="{{site.url}}/{{site.baseurl}}/assets/img/qb_df.png" alt="QB DataFrame" />


And the Recievers:

<img src="{{site.url}}/{{site.baseurl}}/assets/img/wr_df.png" alt="Reciever DataFrame" />


After cleaning the data by removing rows with missing values, our Quarterback data ended with 16 features, out of which 14 could be quantitative, and 375 observations, which should be more than enough for our analysis. More importantly, we ended with 9 features (7 potential quantitative) and 1444 observations in our Reciever dataset. So even though writing and running code to web scrape might feel like a lot of work, it's definitely worth it for the amount of data you can get in a short amount of time. 


Using the 'pd.describe()' function shows us summary statistics, let's dive a little deeper into some of our more important features in the Reciever data. 

<img src="{{site.url}}/{{site.baseurl}}/assets/img/wr_df_describe.png" alt="Reciever DataFrame Describe" />

This function is super helpful because it can help us to get a feel for the distribution of our quantitative variables. From our output, we can see that over the 4 year period, an individual reciever was targeted a median 21 times, but caught the ball just 14 times. And even though the mean number of recieving touchdowns for a reciever was just 1.54, one reciever caught 16 recieving touchdowns in a single season. Maybe it's the same player who had 1,947 recieving yards in a season, while the league average was just 252.6. 

We can even break this down further, and compare statistics by season. 

<img src="{{site.url}}/{{site.baseurl}}/assets/img/wr_df_years.png" alt="Reciever DataFrame Years" />

If we look at these same summary statistics for 2022 and 2023, we can see that for the most part, performance between these seasons was about the same. Many median and mean values were slightly higher in 2022 however, but this could be because the maximum values were higher as well. This highlights a shortcoming of the describe function, which is that it only gives you so much. Much like Beautiful Soup, it's great when you need something simple, but not the best tool if you need deeper insights. For that, we turn to graphics. 


<img src="{{site.url}}/{{site.baseurl}}/assets/img/wr_by_year.png" alt="Yards by Year" />

In this graphic, we see that overall, the recieving yards each season is mostly consistent, with the exception of the 2024 season. While this could be for many reasons, the most likely cause is that the 2024 season is still ongoing, with several weeks of games left to be played. If we account for this by standardizing by the number of games, we see a much more consistent trend below. 

<img src="{{site.url}}/{{site.baseurl}}/assets/img/wr_by_year_standard.png" alt="Yards by Year Standardized" />

------------------------------------------------------------------------

### Conclusion

Well? That wasn't too bad, was it? And you've got some new skills to show for your time! 

As you can see, web scraping provides an efficient way to gather data directly from the internet, and with the help of tools like Beautiful Soup and Selenium, you can easily turn raw online content into structured data for analysis. And even though the process seems technical at first, it becomes manageable with a clear strategy and a step-by-step approach. From identifying the right tools to scraping and cleaning data, these skills will help you unlock a wealth of insights from even the most complex websites. 

Now that you've mastered the basics, it's time to dive in and start scraping your own data! Don't forget to check out the GitHub repository for the full code and data, and leave a comment to tell me what data you scraped!








------------------------------------------------------------------------
