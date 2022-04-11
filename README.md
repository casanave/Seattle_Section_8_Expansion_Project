# Seattle_Section_8_Project

## Repo Navigation: 
|-Data
           -Fire_Stations.csv
           -Hospitals.csv
           -Housing_Project_Full
           -Housing_Project_No_Dummies
           -Housing_Project_With_Zipcodes
           -column_names.md
           -kc_house_data.csv
|-Visuals
           -Correlation.png
           -Renovation_Comparission.png
           -Schools_Map (html) 
           -Schools_Map.png
|-.gitignore
|-README.md
|-Seattle_Section_8_Project.ipynb


## Introduction
Premise:

Public/low income housing has become a somewhat controversial issue in Seattle. While many can agree there are two Seattles, or about the existence of a"homelessness issue," ideas about how to solve for this problem range from tax breaks for real estate investors, increased police budgets, to "defensive design" (IE spikes on buildings to stop people from sleeping there) to increasing unemployment budgets and back-to-work programs. In the city's political history, candidates have called the issue of class disparity and homelessness either larger or smaller, depending on their goals and intended audience. In 2015, when this dataset is from, 45 homeless folks died as a direct result of their homelessness, and the mayor declared a state of emergency. (CITATION: https://www.capitolhillseattle.com/2015/11/45-dead-in-2015-mayor-declares-seattle-homelessness-in-a-state-of-emergency/)

Hypothetical Premise: The City of Seattle city government, in partnership with the State of Washington's state senate has a new pilot program called Section 8 Expansion. There is a 100 million dollar budget in this pilot program to buy real estate at market value to convert into section 8 housing. This project has 3 main goals: 1) to increase the availability of low-income housing 2) to increase property values throughout the city 3) to decrease class disparity.

Instead of making parts of the city into the projects, this program aims to inter-splice public housing all over the city. This evidence based practice results in better outcomes for both the tenants and the properties. Socially, it reduces stigma and segregation as well.

Each property bought for this project will undergo a renovation to ensure quality of living, and there is a separate budget set aside specifically for renovating. For this project, I'm not responsible for balancing the cost of renovating these properties.

I am instead tasked with using machine learning to build a model that can be used to recommend where to build more public housing, under the caveat that they will be renovated. I am looking for properties that will have increased property values in the future. Certain considerations will need to be taken into account for this recommendation, such as the spacing these properties.

While other cities such as Dallas, Texas and Gary Indiana have bought properties back from the public with success, this would be on a much larger scale. (CITATION: https://www.fastcompany.com/90618596/the-radical-way-cities-are-tackling-affordable-housing)

(CITATION FOR OVERVIEW ON SECTION 8 HOUSING: https://www.hud.gov/program_offices/housing/mfh/rfp/s8bkinfo)

FURTHER READING: On mixed income housing in NYC, where there is lots of data: https://case.edu/socialwork/nimc/sites/case.edu.nimc/files/2020-05/Schwartz%20NewYork%202020.pdf

Why should low-income housing be interspersed throughout the city? (CITATION)
"Proponents of mixed-income housing see it as a tool to address the difficulties related to what has been termed the culture of poverty. This phrase derives from the view that physical concentration of poor households in multifamily projects causes severe problems for the residents, including joblessness, drug abuse, and welfare dependency. According to Brophy and Smith 6 Cityscape this theory, a mixture of income levels will reduce the social pathology caused by concentration. Anticipated results of mixed-income housing include the following:

■ The behavior patterns of some lower income residents will be altered by emulating those of their higher income neighbors. The quality of the living environment, not housing quality alone, leads to upward mobility.

■ Nonworking low-income tenants will find their way into the workplace in greater numbers because of the social norms of their new environment (for example, going to work/school every day) and the informal networking with employed neighbors.

■ The crime rate will fall because the higher income households will demand a stricter and better enforced set of ground rules for the community.

■ Low-income households will have the benefit of better schools, access to jobs, and enhanced safety, enabling them to move themselves and their children beyond their current economic condition.

Many of these anticipated results are subtle and difficult to measure. Unlike such a quantifiable result as the effect of mixed incomes on the project’s financial condition, analysis of the effects of mixed-income housing on the behavior of residents must take into account the subtleties of human behavior. It is also important to differentiate between two reasons for these intended benefits. First, if low-income tenants are subsidized to live in developments that are in locations with good schools, low crime rates, and access to jobs, there is some likelihood that the benefits of the location will result in the anticipated outcomes described above."

https://www.huduser.gov/periodicals/cityscpe/vol3num2/success.pdf

###  The Stakeholder's Interests:
The city of Seattle has tasked me with ensuring their making good, safe investments with an assured outcome. Since this project is using public funds, it will be scrupulously documented (and discussed in media.) The model, furthermore, needs to be understandable to civic workers.

The city is also especially interested in seeing the range of housing in my analysis. Often in statistics, we focus on the median or mean, however for this project, I'm going to be collecting data on the size of the ranges.

###  Why Use Machine Learning?
It is coloquial knowledge that there is class disparity in Seattle. However, how large the gap is between neighborhoods specifically, home by home, property by property is what I've been tasked to research. Seattle has decided that the best approach possible is one backed by research, science and evidence.

Using machine learning, we can rely on the data itself to ensure cost-effective and evidence-backed solutions to this problem.

Machine Learning is being implemented here to reduce the political biasing of the solution. However, ML can only be as free of bias as the implementation is thoughtful.

###  Why I Was Highered to Oversee the Project
In order to counter the mechanisms were ML can propogate racism, classism, etc, (CITATION: https://www.nytimes.com/2021/03/15/technology/artificial-intelligence-google-bias.html) Seattle chose me specifically as a Data Scientist for my professional experience working with homeless folks, at a housing-forward non-profit.

## Cleaning and Preparing the Data: 
1) Douplicates were removed
2) Removed properties priced over 2.5 million 
3) Removed properties with over 8 thousand feet of square-foot living space
4) Removed properties with over 100 thousand square foot lot
5) Changed all basements with "?" as a value to 0
6) Changed waterfront to be a binary value, whether or not the property is on the water 
7) Removed one row where a property had 33 bedrooms
8) Changed condition to be a non-categorical, quantitave spectrum 
9) Changed grade to be a non-categorical, qualtitative spectrum, removed any properties that were not currently up to code, also removed luxery and masion properties
10) Changed view into a binary feature
11) Filled N/A values in Year Renovated with 0

### Year Renovated Analysis: 
Because we will be renovating each property selected for this pilot program, it's important to understand the effects renovating a property will have on it's value.

$201,941 is the exact calculated difference in average price between homes that have been renovated vs. homes that have not been renovated. This statistic has not been scaled by amount, such as bedrooms or living space for example.
The average non renovated home in the remaining data after cleaning and preparation, is priced at $719,794. If we were to hypothetically spend our entire budget on the average renovated home, we'd be able to buy 138 properties without going over budget.
The average non renovated home in the remaining data after cleaning and preparation, is priced at $517,853. That may sound pretty close to an average renovated home but it fits into the laid out budget for the project about 193 times.
For clarity, if we were only buying average priced non-renovated homes, we'd be able to buy 54 more homes than if we were only buying average priced non renovated homes.

To properly compare visually, I will take each home that has been renovated, and subtract the average price of a non-renovated home from the sale price, this will recenter the visualization's bars to show how above or below each property was compared to the average un-renovated home.
![Renovation_Comparission](https://user-images.githubusercontent.com/8728172/162642572-cbd42c9a-0ddb-4a36-9a3f-0d61703b1120.png)

X axis = average price of non-renovated home

Green Bar = above average price of non-renovated home

Blue Line = average price of renovated home

This plot's 0 on the Y axis has been adjusted so that everything above are properties where their price (grouped by every 5 years,) is above the average price for a non-renovated property. The blue line represents the average price of properties that have been renovated. Properties above the blue line represent renovated properties that are valued above the average renovated property.

Observations:
1) all properties renovated after 1975 are more valuable than the average renovated property.

2) properties renovated in the years between 1990 to 2010, are averaging as a higher price compared even to other renovated properties.

Inferences:
Renovating properties increases their value, that's to be expected. However, we now can now infer that if we renovate properties that have already been renovated but their renovation happened before 1975, we can "flip" those properties into having a higher value.

## Feature Engineering 
1) Made new column for age of home
2) Made new column which uses either the year the property was renovated or built

### Infrastructure Data:
3) Made column for distance from downtown (source: google maps) ** also removed properites more than 25 miles away from downtown
4) Made column for distance from closest police station (source: http://www.seattle.gov/police/about-us/police-locations)
5) Made column for distance from closest hospitals (source: https://data-seattlecitygis.opendata.arcgis.com/datasets/hospitals/explore) 
6) Made column for distance from closest public schools *with scraped data using Selenium* (source: https://www.seattleschools.org/schools/) 

## Zipcode Data
Using this kind of model, I'll need to pick one zipcode as the default zipcode so we can compare the price of a property going up or down depending on what zipcode it's in.

Seeing as this project aims to specifically research class disparity, I'll be using 98039 as my default zipcode, it's the wealthiest zipcode in Seattle.

CITATION: https://www.zipdatamaps.com/economics/income/agi/metro/wealthiest-zipcodes-in-metro-seattle-tacoma (Source: US Internal Revenue Service - 2018)

By comparing all other zipcodes to the wealthiest zipcode, we can see the full scope of how much a zipcode can affect property values. I'm assuming 1) that public infrastructure is working well in this zipcode, and is reflected partially in this wealth. I'm also assuming 2) that this zipcode was also the wealthiest zipcode in 2015.

## Correlation and Multicollinearity
![correlation](https://user-images.githubusercontent.com/8728172/162643659-8bc83878-1c95-40f6-b4b7-2fe35b80e028.png)
Choosing which features to drop: sqft_living has an over 70% correlation with sqft living15. This makes sense, the closest 15 neighbors to a home having a correlating size of living space. sqft_living also has a correlation with sqft_above, which also makes sense, as these features are very similar. sqft_lot is closely correlated with sqft_lot15 for similar reasons. sqft_living also is interestingly correlated with bathrooms. Because this feature is so correlated to others, I'll be dropping it. 

For only keeping one of those variables, Keeping sqft_15 makes sense because it's about the closest 15 neighbors, not about the property itself, which for our needs suits better since this metric is more closely related to the theory of mixed income housing. However, sqft_above is also too closely correlated with grade. And between sqft_above or grade, grade is the feature that we have most control of with renovation of the property. Therefore I'll be getting rid of sqft_above to keep grade as a feature. 


yr_built, yr_renovated and yr_mod are all correlating with each other at an over 70% rate which makes sense. Of the three features, I'm keeping yr_renovated since it's most closely related to our interests. 

Closest school is almost entirely predicted by closest police station and vice versa, so I'll be dropping closest police station as closest school has a more complex matrix of data associated with it. Downtown is shows multicollinearity with schools and police stations so I'll be dropping downtown also. 

Additionally, I'll be dropping zipcode since I've made those into dummies.

## Modeling: (using stats models OLS) 
1) Baseline Model: Grade, Bathrooms, Lat and Price as the target. R-Squared Adj. 53%, Kurtosis at 11.96
2) Second Model: Grade, Bathrooms, Lat and Log of Price as the target. R-Squared Adj. at 63%, Kurtosis at 3.71
3) Third Model: View, Bedrooms and Floors And Previous Features, with Log of Price as target. R-Squared Adj. at 65%
4) Fourth Model: Closest School Distance, Square Foot Basement and Waterfront And Previous Features, with Log of Price as target. R-Squared Adj. at 67%
5) Fifth Model: Year Renovated, Closest Hospital Distance and Square Foot Lot of Closest 15 Neighbors And Previous Features, with Log of Price as target. R-Squared Adj. at 68%
6) Sixth Model: Condition, Longitude and Age of Home And Previous Features, with Log of Price as target. R-squared Adj. at 72%
7) Seventh Model: Adding Zipcodes And Previous Features, with Log of Price as target. R-squared Adj. at 83%, Latitude and Closest Hospital Distance had p values of over 0.05% and thus were removed. 
8) Eighth Model: Removing Hospital and Latitude Data, with Log of Price as target. R-squared Adj. at 83%. 

FINDINGS REPORT: 
 -  As grade increases by one unit, the price changes by 19.60 percent.
 -  As bathrooms increases by one unit, the price changes by 11.89 percent.
 -  If view was a feature of a property, the price would rise by 24.85 percent.
 -  As bedrooms increases by one unit, the price changes by 4.66 percent.
 -  As floors increases by one unit, the price changes by 0.86 percent.
 -  As closest_school_distance increases by one unit, the price changes by -1.57 percent.
 -  As sqft_basement increases by one unit, the price changes by 2.32 percent.
 -  If waterfront was a feature of a property, the price would rise by 47.73 percent.
 -  As yr_renovated increases by one unit, the price changes by 0.00 percent.
 -  As sqft_lot15 increases by one unit, the price changes by 0.00 percent.
 -  As condition increases by one unit, the price changes by 4.90 percent.
 -  As long increases by one unit, the price changes by 38.18 percent.
 -  As age_of_home increases by one unit, the price changes by 0.20 percent.
 -  If a property was in zipcode_98001 zipcode instead of 98039, the price would change by -109.81  percent.
 -  If a property was in zipcode_98002 zipcode instead of 98039, the price would change by -115.93  percent.
 -  If a property was in zipcode_98003 zipcode instead of 98039, the price would change by -109.85  percent.
 -  If a property was in zipcode_98004 zipcode instead of 98039, the price would change by -16.62  percent.
 -  If a property was in zipcode_98005 zipcode instead of 98039, the price would change by -55.04  percent.
 -  If a property was in zipcode_98006 zipcode instead of 98039, the price would change by -62.67  percent.
 -  If a property was in zipcode_98007 zipcode instead of 98039, the price would change by -65.15  percent.
 -  If a property was in zipcode_98008 zipcode instead of 98039, the price would change by -62.86  percent.
 -  If a property was in zipcode_98010 zipcode instead of 98039, the price would change by -80.95  percent.
 -  If a property was in zipcode_98011 zipcode instead of 98039, the price would change by -79.85  percent.
 -  If a property was in zipcode_98014 zipcode instead of 98039, the price would change by -80.53  percent.
 -  If a property was in zipcode_98019 zipcode instead of 98039, the price would change by -82.64  percent.
 -  If a property was in zipcode_98023 zipcode instead of 98039, the price would change by -110.25  percent.
 -  If a property was in zipcode_98024 zipcode instead of 98039, the price would change by -79.19  percent.
 -  If a property was in zipcode_98027 zipcode instead of 98039, the price would change by -72.32  percent.
 -  If a property was in zipcode_98028 zipcode instead of 98039, the price would change by -84.88  percent.
 -  If a property was in zipcode_98029 zipcode instead of 98039, the price would change by -65.88  percent.
 -  If a property was in zipcode_98030 zipcode instead of 98039, the price would change by -113.51  percent.
 -  If a property was in zipcode_98031 zipcode instead of 98039, the price would change by -116.75  percent.
 -  If a property was in zipcode_98032 zipcode instead of 98039, the price would change by -123.84  percent.
 -  If a property was in zipcode_98033 zipcode instead of 98039, the price would change by -50.54  percent.
 -  If a property was in zipcode_98034 zipcode instead of 98039, the price would change by -76.40  percent.
 -  If a property was in zipcode_98038 zipcode instead of 98039, the price would change by -98.65  percent.
 -  If a property was in zipcode_98040 zipcode instead of 98039, the price would change by -41.34  percent.
 -  If a property was in zipcode_98042 zipcode instead of 98039, the price would change by -112.00  percent.
 -  If a property was in zipcode_98052 zipcode instead of 98039, the price would change by -62.66  percent.
 -  If a property was in zipcode_98053 zipcode instead of 98039, the price would change by -54.66  percent.
 -  If a property was in zipcode_98055 zipcode instead of 98039, the price would change by -115.96  percent.
 -  If a property was in zipcode_98056 zipcode instead of 98039, the price would change by -94.70  percent.
 -  If a property was in zipcode_98058 zipcode instead of 98039, the price would change by -110.54  percent.
 -  If a property was in zipcode_98059 zipcode instead of 98039, the price would change by -89.16  percent.
 -  If a property was in zipcode_98065 zipcode instead of 98039, the price would change by -66.70  percent.
 -  If a property was in zipcode_98070 zipcode instead of 98039, the price would change by -84.82  percent.
 -  If a property was in zipcode_98072 zipcode instead of 98039, the price would change by -74.17  percent.
 -  If a property was in zipcode_98074 zipcode instead of 98039, the price would change by -66.62  percent.
 -  If a property was in zipcode_98075 zipcode instead of 98039, the price would change by -61.17  percent.
 -  If a property was in zipcode_98077 zipcode instead of 98039, the price would change by -74.59  percent.
 -  If a property was in zipcode_98092 zipcode instead of 98039, the price would change by -111.15  percent.
 -  If a property was in zipcode_98102 zipcode instead of 98039, the price would change by -50.00  percent.
 -  If a property was in zipcode_98103 zipcode instead of 98039, the price would change by -59.42  percent.
 -  If a property was in zipcode_98105 zipcode instead of 98039, the price would change by -47.28  percent.
 -  If a property was in zipcode_98106 zipcode instead of 98039, the price would change by -103.03  percent.
 -  If a property was in zipcode_98107 zipcode instead of 98039, the price would change by -58.59  percent.
 -  If a property was in zipcode_98108 zipcode instead of 98039, the price would change by -100.74  percent.
 -  If a property was in zipcode_98109 zipcode instead of 98039, the price would change by -41.79  percent.
 -  If a property was in zipcode_98112 zipcode instead of 98039, the price would change by -37.16  percent.
 -  If a property was in zipcode_98115 zipcode instead of 98039, the price would change by -56.33  percent.
 -  If a property was in zipcode_98116 zipcode instead of 98039, the price would change by -60.24  percent.
 -  If a property was in zipcode_98117 zipcode instead of 98039, the price would change by -56.66  percent.
 -  If a property was in zipcode_98118 zipcode instead of 98039, the price would change by -91.34  percent.
 -  If a property was in zipcode_98119 zipcode instead of 98039, the price would change by -44.55  percent.
 -  If a property was in zipcode_98122 zipcode instead of 98039, the price would change by -64.43  percent.
 -  If a property was in zipcode_98125 zipcode instead of 98039, the price would change by -79.00  percent.
 -  If a property was in zipcode_98126 zipcode instead of 98039, the price would change by -79.91  percent.
 -  If a property was in zipcode_98133 zipcode instead of 98039, the price would change by -87.53  percent.
 -  If a property was in zipcode_98136 zipcode instead of 98039, the price would change by -66.18  percent.
 -  If a property was in zipcode_98144 zipcode instead of 98039, the price would change by -73.10  percent.
 -  If a property was in zipcode_98146 zipcode instead of 98039, the price would change by -100.32  percent.
 -  If a property was in zipcode_98148 zipcode instead of 98039, the price would change by -109.11  percent.
 -  If a property was in zipcode_98155 zipcode instead of 98039, the price would change by -87.67  percent.
 -  If a property was in zipcode_98166 zipcode instead of 98039, the price would change by -91.74  percent.
 -  If a property was in zipcode_98168 zipcode instead of 98039, the price would change by -119.97  percent.
 -  If a property was in zipcode_98177 zipcode instead of 98039, the price would change by -66.19  percent.
 -  If a property was in zipcode_98178 zipcode instead of 98039, the price would change by -118.24  percent.
 -  If a property was in zipcode_98188 zipcode instead of 98039, the price would change by -118.39  percent.
 -  If a property was in zipcode_98198 zipcode instead of 98039, the price would change by -112.50  percent.
 -  If a property was in zipcode_98199 zipcode instead of 98039, the price would change by -49.08  percent.
 
 ## Conclusion: 
 1) As we can read in the printed report above, improving the grade and the condition (as is our aim with renovations) would make the value of the properties increase by roughly 1/4th. Therefore I'm recommending that the city of Seattle focus on improving both grade and condition of properties during the renovation.

Choosing which properties to renovate: the properties where the least expensive changes will increase the grade, and/or condition of the property are a safe bet.

2) There are certain zipcodes where the class disparity is quite large. I recommend that the city of Seattle spend 1/3 to 3/5ths of this current projects budget just focusing on renovating properties in these zipcodes with the lowest grade/conditions, and making those into public housing. These zipcodes are as follows: 98168, 98188, 98178, 98198, 98148, 98146, 98108, 98092, 98058, 98055, 98042, 98032, 98031, 98030, 98023, 98003, 98002, 98001. The data shows that properties in these zipcodes would increase in value by over 100% if they were in the 98039 zipcode instead.

3) While one and a half percent may not seem like a lot--there is now statistical evidence that putting new schools specifically where the closest schools are far away will improve the property values of all the homes closest to that school. As schools increase distance away from homes, the property value of the home drops by just over 1.5%. While building schools is outside the range of the scope of this public housing project, it is a finding to take back to the city counsel and state senate.

<img width="753" alt="schools_map" src="https://user-images.githubusercontent.com/8728172/162645079-4c17e286-9fe4-432d-9455-e6865df41fe0.png">

KEY: Blue Circles represent public schools.

While we can visually inspect the map above and look for places where a new school could go, we can also combine our knowledge of the zipcode data, and focus on building a new school in the zipcodes that have the highest class disparity compared to the wealthiest zipcode such as zipcode 98032 (the zipcode with the least valuable properties in this dataset.)

FURTHER WORK:
With more time and resources, I'd like to exactly calculate the areas that are the most isolated from public schools, but the above map shows a rough idea, by looking at the areas of the map not shaded blue by a circle. In the future, I'd like to exactly calculate the distance of these circles in human measurements, not in pixels.

 
