---
title: "Apartment_1"
date: 2020-08-31T20:50:09-04:00
draft: true
---

## Introduction
In this blog post I am going to walk through a recent project that I did where I used Python's BeautifulSoup library, Docker, Kubernetes, Python's StatsmodelsAPI library and the Googlemaps Python Api to get information about potential apartments to live in the Tokyo area and figure out where is the optimal price to be paying based on the apartment type and proximity to train stations and other important locations. 


## Web Scraping 
For web scraping I used Python's BeautifulSoup library as well as the requests library. I pulled my data from a Japanese Real Estate website that allowed you to select the apartments that you wanted to find based off of certain critiria- I mainly selected based off of location and size of apartment (1K or larger) - and the website lists all listings that meet that criteria with a bunch of other information. The information that I choose to scrape included: apartment square meterage, closest station, how old the apartment is, how much of a deposite is due and a few other variables that I think could prove valuable in my analysis. Since each page includes multiple listings I had to loop through both the listings and however many webpages I wanted to scrape through. So for that I used a nested for loop like this:
```python
pages = np.random.randint(1,1000,1)

for page in pages:
	page = requests.get(URL + str(pages) + "&ref_=adv_nxt", headers=headers)
	soup = BeautifulSoup(page.text, 'html.parser')
	apartment_container = soup.find_all('div', class_ = "cassetteitem")
	sleep(np.random.randint(2,20)) # 2-20 seconds between each page
	for container in apartment_container:
		sleep(np.random.randint(2,3)) # wait 2-5 seconds between each apartment container for testing 
		renty = container.tbody.ul.span.text
		rent_price.append(renty)


``` 
Since I wanted to make sure I didn't run into any issues with making too many requests at once and therefore run into issues of being flagged as a bot and being kicked out I made sure to use the `time` libraries sleep function to take a random 10-30 second break between each apartment for each page. 

## Using the Googlemaps API
Another important piece of information to consider when moving into a place is how far it actually is from your work location. For that I decided to use the `googlemaps` api. Which allows you to lookup the time it takes to commute to a location during anytime you set from your inputted address and your goal destination. Since I was scraping the address of each of the apartments in my code already I just had to loop through the each apartment address and use that address as the argument for my function to calculate how long it takes via transit to get to my work from the certain apartment location. I then added this as a function in my dataset....


## Docker/Kubernetes Architecture/Setup


## Data Visualization



## Analysis  