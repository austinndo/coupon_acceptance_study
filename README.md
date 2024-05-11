# Will the Customer Accept the Coupon?
I investigate a dataset from UCI Machine Learning repository collected from a survey on Amazon Mechanical Turk. Several fields are captured including the recipient's destination, age, current weather, education level, how often they frequent certain establishments (bars), etc.

If a driver accepts a coupon, either right away or to be used at a later date before the coupon expires, the field "Y" is assigned a value of 1. On the other hand, recipients that deny the coupon have an assigned value of 0.

The full analysis can be found [here](austin_do_assignment_5_1.ipynb)



## Read and clean the data

I use pandas to first read the [csv file](data/coupons.csv) and take a quick look using the methods `.head()` and `.info()` 
![data_head](/assets/data_head.png)

![data_info](/assets//data_info.png)

I found that the car column was missing a lot of values, and did not prove to be helpful in the later analysis. I utilize `dropna()` to get rid of any other null values after removing the 'car' column from my dataframe. I assign a new variable 'cleaned' to this cleaned data

![cleaned](/assets/cleaned_df_info.png)


## Begin visualizations

After cleaning the data, I created a bar chart of the counts of the different coupon types. There are five different groups of coupons, with the most belonging to 'Coffee House'

![coupon_bar](/assets/coupon_bar.png)

Later on, I focus on just the carry out and take away coupons. Within this subset I compare the acceptances between various fields.

![carry_pie](/assets/carry_pie.png)

![carry_weather](/assets/carry_weather_hist.png)

![carry_education](/assets/carry_education_hist.png)


## Bar Coupons 

The first task is to investigate the bar coupons. I would be required to determine the proportion of coupons that were accepted several times in this analysis. As a result, I created a custom function that accepts a dataframe and returns the proportions

```
def getProportionAccepted(df):
    return df['Y'].value_counts(normalize=True)
```

Of all the bar coupons, 41.19% were accepted. Drivers that go to bars more than three (3) times a month accepted the coupon 62.7% of the time, indicating that those drivers that often go to bars will make use of the coupon if offered. 

Those under the legal drinking age are not making use of bar coupons, as an additional filter for drivers that go to bars more than once a month and are over the age of 25 had an acceptance rate of 69.0%.

Continuing with this investigation, drivers with a passenger that is not labeled as a kid and did not have an occuption in farming, fishing, or forestry also often chose to use the bar coupons. (At a 71.4% acceptance rate)



## Carry Out and Take Away Coupons

Following the bar coupon study, I chose to look at the carry out/take away coupons that consisted of a total of 2280 entries in my cleaned dataset.

Looking at the previous weather comparison chart, I noticed that many drivers chose to accept carry out coupons when the weather was "Sunny". In fact, 76.4% of coupons were accepted when the weather was "Sunny" compared to when it was "Rainy" at 61.1%.

I continued this investigation and found that across income levels, ages, and despite the destination direction (whether it was in the same direction or out of their way), drivers often chose to use the carry out coupons in "Sunny" weather. 

One feature of note was that between education levels, no one with an education of "Some High School" appeared to deny the coupon. There was some variation of coupon acceptance between those with a Bachelors degree or higher vs those without a Bachelors degree. The difference being a 71.8% acceptance rate for a Bachelors or greater vs. an 80.8% rate otherwise.

To summarize, drivers often use carry out and take away coupons in general. 73.8% of these coupons were accepted. When the weather is "Sunny", most drivers decided to accept the coupon for immediate use, or at a later date before it would expire. Drivers that held no degree, or at least some education below a Bachelors, were only slightly more likely to use these coupons compared to their peers who hold a Bachelors degree or greater.



