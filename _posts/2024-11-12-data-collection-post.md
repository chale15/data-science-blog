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

Ready to move beyond curated datasets? Web scraping lets you collect almost any online data, and you can get started quickly with two Python packages: Beautiful Soup and Selenium. 

In essence, web scraping automates the process of copying data from websites into a format you can analyze. For instance, you could grab data from a Wikipedia table for analysis or extract recipes without ads. If a dataset doesn’t exist, web scraping lets you create your own!

In this post, I’ll share how I approached a football question with web scraping and walk you through some basics you can use to answer questions of your own!

---

### Motivating Question

<p class="tip-description">Does a quarterback's ability to run impact receiver performance in American football?</p>

Inspired by an announcer's comment during a football game, I wanted to test the claim that a quarterback’s mobility can reduce receiver performance. While there are lots of pre-curated NFL datasets, I wanted to collect data tailored to my question, so I turned to the internet.


<a href="https://usasports.co.uk/blogs/blog/a-beginners-guide-to-american-football-and-the-nfl?srsltid=AfmBOopndDwlgsvt01xaVEIIp0gPuECjvfRV_hSA737oPLnDQ9wtoX0i" target="_blank">Beginner's Guide to American Football</a>

---

### Finding Your Data

In order to scrape data, you first have to find it. Fortunately I didn't have to search too hard, as the NFL tracks and makes player, team, and many other statistics available on their <a href="https://www.nfl.com/stats/player-stats/" target="_blank">website</a>. Specifically, I decided that I wanted to use the 'Stat Leaders' table, as well as statistics located on individual player pages to answer my question. 

<img src="{{site.url}}/{{site.baseurl}}/assets/img/nfl_home_page.png" alt="NFL Home Page" />

As you can see, this page has a lot going on, but with the inspect element tool, I was able to find the information I needed buried within HTML tags and divisions. For an introduction to HTML and inspect element, check out this <a href="https://www.youtube.com/watch?v=TUpsyv9A9vU" target="_blank">video!</a>

---

### Should You Use Your Data?

Once you've found your data, it's easy to get excited and skip straight to scraping. The most important step in the process however is to decide whether your data can be obtained ethically. Typically, websites will have a 'robots.txt' file that outlines permitted use of data on that site. Some sites restrict data usage or require a delay in requests, and ignoring these rules can get you banned (in addition to just being rude). 

For more information about web scraping ethics and the 'robots.txt' file, <a href="https://brightdata.com/blog/how-tos/robots-txt-for-web-scraping-guide" target="_blank">this blog</a> explains it well.

Fortunately for us, the NFL gives us almost universal access to scrape, as seen in their 'robots.txt' file below.

<img src="{{site.url}}/{{site.baseurl}}/assets/img/nfl_robots.png" alt="NFL robots.txt" />

Now that we've determined that we **should** use this data, we need to figure out **how** to obtain it. 

---

### Choosing the Right Tool

For this project, I wrote my code in a Jupyter Notebook. You can access my code and final results at the github link below. 

<div style="display: flex; justify-content: center; align-items: center;">
  <a href="https://github.com/chale15/NFL_Data/" style="text-decoration:none;">
    <button style="background-color:#2dba4e; color:white; padding:10px 20px; border:none; border-radius:5px; font-size:16px;">
      GitHub Repository
    </button>
  </a>
</div>

The two main web scraping libraries in Python are *Beautiful Soup* and *Selenium*:

- **Beautiful Soup**: Ideal for static pages. It works with the Requests library to parse HTML in Python.
- **Selenium**: A more powerful for dynamic content, allowing interactions like clicks and dropdowns.

<a href="https://realpython.com/python-requests/" target="_blank">Requests</a>, <a href="https://realpython.com/beautiful-soup-web-scraper-python/" target="_blank">Beautiful Soup</a>, <a href="https://www.simplilearn.com/tutorials/python-tutorial/selenium-with-python" target="_blank">Selenium</a>

Generally speaking, you want to use Beautiful Soup and Requests to obtain data whenever possible. A good rule of thumb is if there's nothing interactive that requires you to use Selenium, use Beautiful Soup. 

For this project, I used both packages: Selenium for interactive elements and Beautiful Soup for straightforward extraction.

---

### The Code

As is good practice, we start by loading in the everything we need. For this project, I ended up using pandas, requests, BeautifulSoup, time, and re, but every project is slightly different and might require different tools. I also loaded in some Selenium specific functions, most of which I didn't end up needing, but that are good to have just in case. In order to use Selenium, you have to specify which browswer the tool will work through, and load the appropriate webdriver. I use Safari but you can easily modify the code to use whichever browser you prefer. 


#### 1. Import Packages

```python
import pandas as pd, numpy as np, requests, time, re
from bs4 import BeautifulSoup
from selenium import webdriver
from selenium.webdriver.common.by import By
```

After importing my packages, I had to plan out my code. Like most programming tasks, there's many different ways to arrive at the same solution, so use the approach that makes the most sense for you

I wanted to collect data spanning several years, so my code is nestled within loops. I also decided that in the context of my problem, creating two separate datasets made the most sense. The process for building each dataset is very similar, so I'll just walk through the creation of the Quarterback stats dataset. 

#### 2. Initialize Selenium

```python 
try:
    driver.quit()
except:
    print("No Driver")

link = 'https://www.nfl.com/stats/player-stats/category/passing/' +str(2024 - i) +'/reg/all/passingyards/desc'

driver = webdriver.Safari(service=SafariService()) #Modify for your preferred browser
driver.get(link) 
```

Once these lines of code have been run our automated Selenium browser is active, and will interact with your website however we tell it. From here, my code tells the automated browser to search through the HTML until it finds what we want; in this case the table with Quarterback information. 


#### 3. Scrape Data with Selenium

```python
while True:
try:
    container = driver.find_element(By.CLASS_NAME, 'nfl-c-player-directory')
    all_qbs = container.find_elements(By.XPATH, ".//tbody/tr")
except:
    break

for player in all_qbs:
    stats = player.find_elements(By.XPATH, "./td")
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
```

Once it has found the table, it locates rows which represent individual players, and adds that player's data for each of the key stats into a list. Essentially, we're building the columns of our dataframe separately, and we'll combine them at the end.

Our table only shows 25 players at a time, which is why we have to use Selenium. After scraping data from the first 25 rows, our browser clicks a button to move to the next page of results. This process repeats until there are no more buttons to push, and we know that we've scraped the entire table. 


#### 4. Scrape Data with Beautiful Soup

```python 
for qb in qbs:
qb_name = re.sub('[^a-zA-Z]+','-', qb)
url = 'https://www.nfl.com/players/' + qb_name + '/stats/career'
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
```

Next, we need data from individual player sites. First we find the specific url for each player using regular expressions. 

For each player in our original list of names, we send a request to their page and use Beautiful soup to extract the information we want, in this case their team, the number of games they played, and their rushing statistics.


#### 5. Compile and Save Dataset

```python
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
```

Once we have the data we want, we save it away, wipe the lists we're using as temporary storage, and repeat the process for the next year.

```python
driver.quit()
df = df.drop_duplicates(ignore_index=True)
df.to_csv('./qb_data.csv')
```

After all of our loops have finished running, all that's left to do is to quit Selenium and write our data to a csv file.

And there we have it! A successfully scraped quarterback stats dataset!

(As previously mentioned, the process for scraping wide reciever data is nearly identical, and is included in the '<a href="https://github.com/chale15/NFL_Data/blob/main/nfl_data.ipynb" target="_blank">nfl_data.ipynb</a>' file on GitHub)

---

### EDA (Exploratory Data Analysis)

Now that the hard part is done let's take a look at our datasets

#### 1. Overview

First, the Quarterback data:

<img src="{{site.url}}/{{site.baseurl}}/assets/img/qb_df.png" alt="QB DataFrame" />


And the Recievers:

<img src="{{site.url}}/{{site.baseurl}}/assets/img/wr_df.png" alt="Reciever DataFrame" />


| Dataset      | # of Observations | # of Features | # of Quantitative Features |
|--------------|-------------------|---------------|----------------------------|
| qb_data.csv  | 375               | 16            | 14                         |
| wr_full.csv  | 1444              | 9             | 7                          |


#### 2. Summary Statistics

The 'pd.describe()' function shows summary statistics, let's dive a little deeper into some of our more important features in the Reciever data. 

<img src="{{site.url}}/{{site.baseurl}}/assets/img/wr_df_describe.png" alt="Reciever DataFrame Describe" />

This function helps us get a feel of the distribution of our quantitative variables.

We can even break this down further, and compare statistics by season. 

<img src="{{site.url}}/{{site.baseurl}}/assets/img/wr_df_describe_years.png" alt="Reciever DataFrame Years" />

#### 3. Visualization

Summary statistics can only get us so far, so lets look at some visuals. 

<img src="{{site.url}}/{{site.baseurl}}/assets/img/wr_by_year_standard.png" alt="Yards by Year Standardized" />

From this comparison of recieving yards per game by year, we can see that overall, this statistic is mostly unaffected over time. We do see a larger spread and more outliers for data from the 2024 season, however this is to be expected as the season is still going on, and consequently, there is less data than for previous (completed) seasons. 

<img src="{{site.url}}/{{site.baseurl}}/assets/img/wr_correlation.png" alt="Reciever Corrplot" />

We also see from a simple heat map that many of the player statistics are highly correlated. For many problems, this would be a cause of concern, however for our data, this relationship makes sense. Generally, the best players have high values across the board, and those who catch the ball the most are more likely to produce more yards or points than other players.

<img src="{{site.url}}/{{site.baseurl}}/assets/img/top_players_yds.png" alt="Top Players (Yards)" />

<img src="{{site.url}}/{{site.baseurl}}/assets/img/top_players_tds.png" alt="Top Players (Touchdowns)" />

Next, I wanted to quickly determine several top players in order to pick a candidate for further individual analysis. I selected Tyreek Hill, as he has shown to be consistently one of the best recievers in terms of production, yet he has played several games this year with a new quarterback, due to an injury early in the season. The graphic below can help us to visualize the effect of this change. 

<img src="{{site.url}}/{{site.baseurl}}/assets/img/hill_stats_time.png" alt="Tyreek Hill Stats by Season" />

While further statistical testing is needed to confirm our hypothesis, as well as cross validation with other players for a higher level of statistical rigor, we can see from the graph above that at least for this player, our hypothesis seems to have some validity. 


---

### Conclusion

As you can see, web scraping offers a powerful way to access and customize data for analysis. With Beautiful Soup and Selenium, you can transform raw online content into structured datasets for research and insights, and we were able to quickly obtain data curated to the question at hand.

And even though the process seems technical at first, it becomes manageable with a clear strategy and a step-by-step approach. From identifying the right tools, to scraping and cleaning data, working on these skills will help you unlock a wealth of insights from even the most complex websites.

Now that you've mastered the basics, it's time to dive in and start scraping your own data! Don't forget to check out the GitHub repository for the full code and data, and leave a comment to show me the data you scraped!

---
