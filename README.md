# school-project-
Group Work on data-tidying and data-wrangling with visualization


---
output:
  pdf_document: default
  html_document: default
  fontsize: 11pt
---

Title: "Comparative Data-Analysis of wealth and health dynamics of Norway and Sweden followed up with general comparison of Denmark and Finland"
output: pdf_document
Group Assignment: Econ 3170 - Data Science for economists 
Candidate number: 152 and 185
Date: 17.11.2023
Place: University of Oslo


Introduction:

  This study explore the utilization of data analysis in the field of economics by using R programming. The primary objective is to investigate the potential relationship between a country's economic growth, measured through GDP, and alcohol consumption—an integral factor in the consumption function. Specifically, the study focuses on the average alcohol consumption in liters per capita across four countries (Norway, Sweden, Denmark, and Finland) over the thirteen-year period from 2000 to 2013, utilizing data extracted from the "Life_Expectancy_Data" data set.

Employing visualization techniques and machine learning tools, the project aims to elucidate patterns and insights. The procedural steps involve initial data acquisition, importation, and subsequent data wrangling. The visualization of findings through graphs acknowledges the inherent limitation of graphical representations in precision, emphasizing the need for meticulous interpretation to undergo potential confusion.


How does growth of country's GDP looked like in developed countries especially among those four countries between the year 2000-2013?

  We look forward to compare the log GDP, the average annual growth of GDP  in the period 2000-2013 to see whether there is differences and similarities among those developed countries. we keep the observation of the whole timeline from 2000 to 2013. Since all the countries we are looking at are developed countries, therefore we tend to look with GDP growth in comparison of alcohol consumption and whether or not this two variables tells us commonalities and differences.
  
Why do we look only through those three variables: GDP, Alcohol and BMI? 

  First of all, we are genuinely interested in looking at the average annual growth of GDP, its effects in the country and comparing among countries will allow us to understand the bigger picture, therefore we stick with this data of average sum in the counties.
  
Second of all, we would like to see whether the results as the context of growth in GDP with consume of country's population or not.
  Since, the economic understanding of relation between average annual growth of GDP hangs together with private consume. Because of the increase in GDP, will allow population to produce more, when we produce more then we earn more thereby we consume more. However, that might some distinctions with GDP growth as well such as other factors than economic explanation which we will look into. 


Methods:

    Data Wrangling Task 
As mentioned above we uses data wrangling to tidy our data.we first download the data, import the data to Rstudio. Using function (readr) which yields a tibble which make it easier to work with data as such. Then install one of the core packages (tidyverse) and run to present our data from the library.

```{r import data to tidy and warangle}
library(readr)
library(tidyverse)
Life_Expectancy_Data <- read_csv("Life Expectancy Data.csv")
```

    1.    Average annual growth Log GDP
  Then we first look at GDP growth only in, Sweden. Extracting only Sweden for observations from the data set, name growth_sweden then filter with Year with vector 2000-2013 defining only Sweden among all other countries from the data. Mutate() function is part of the dplyr package. It is used for adding new variables (columns) to a data frame based on transformations of existing variables.So, we mutate GDP as log GDP so that we can get a more normalized distribution from a skewed variable from the data set. 

```{r}
growth_sweden = Life_Expectancy_Data %>% 
  filter(Year %in% c(2000:2013), Country=="Sweden") %>%
  mutate(GDP=log(GDP)) %>% 
select(Country, Year, GDP)
```

  Then using (ggplot) to display values, mapping the variables in the data to visual properties of geom(aesthetics) the GDP growth in Sweden given the timeline. The graph lies with x-axis is Year and y-axis being log GDP.
```{r}
growth_sweden %>% 
  ggplot(aes(x=Year)) + geom_line(aes(y=log(GDP)),color="blue")
```
  Average annual growth log GDP growth in Sweden we see a sharp slop in 2005 due to uncertain reasons but the another slope we saw in Sweden's GDP is in 2008 which is clearly due to the financial crisis in 2008. As the graph shows, the Swedish GDP growth between 2008-2010 was a mere catch up to take off again in the GDP growth. Then we see the steady incline upwards in the Swedish GDP growth until 2011 where the GDP growth touches up-to 2.4 log GDP and it starts sinking down again afterwards driving below 2.2 in 2013. 

  Moving on, we now will use log GDP observations to understand growth in Norway is as named growth_norway extracted from the data. We then filtered with Year given the vector of years, Norway as the country. 
then we plot with (ggplot) and (geom_line) to visualize the development in Norway. 

```{r}
growth_norway = Life_Expectancy_Data %>% 
  filter(Year %in% c(2000:2013), Country=="Norway") %>%
  mutate(GDP=log(GDP))

growth_norway %>% 
  ggplot(aes(x=Year)) + geom_line(aes(y=log(GDP)),color="red")
```

  Unlike Swedish slope in 2005 the Norwegian GDP growth hits 2.4, went above in 2005 and clear linear declination around 2% of GDP growth in 2008. Then it bounced up-to almost 2.5% in 2010 and crashed downwards again afterward. As mentioned above the linear declination occurred in 2008 was due to financial crisis the log GDP growth in Norway was swinging heavily between 2% and 2.5% and in 2013 was GDP growth rate in Norway was under 2%. with this visual data we have analyzed the log GDP growth with percent in Norway. 
                                  
  Here we compare the growth GDP, log GDP of Norway and Sweden, we named (growth_norswe). The observations being growth of GDP within the period. After extracting the data, we filter period, only Sweden and Norway and then mutate as log(GDP) to see the dynamics if there is any. 

```{r}
growth_norswe = Life_Expectancy_Data %>%
  filter(Year %in% c(2000:2013),Country %in% c("Norway","Sweden")) %>%
  mutate(log(GDP))  
growth_norswe %>% 
  filter(Country %in% c("Norway","Sweden"), Year %in% c(2000:2013)) %>%
  ggplot()+ geom_line(aes(x=Year,y=log(GDP),color=Country))
```

  The data might be exaggerated but we do see similar patterns of the inclination and declination but not exactly parallel but similar. However, the growth log GDP in Norway swings more than Sweden as from the data we used. However, the patching up Norwegian approach to see the post-2008 crisis was not stable as neither the Swedish but the movements were less robust. 

  Hereafter, we will be comparing all four countries to visualize how does is it look with given data compared to the growth of GDP. 

```{r}
growth_nordics = Life_Expectancy_Data %>%
  filter(Year %in% c(2000:2013),Country %in% c("Denmark","Finland", "Norway", "Sweden")) %>%
  mutate(log(GDP))  
growth_nordics %>% 
  filter(Country %in% c("Denmark","Finland", "Norway", "Sweden"), Year %in% c(2000:2013)) %>%
  ggplot()+ geom_line(aes(x=Year,y=log(GDP),color=Country))
```

  Comparing among the four countries with given timeline, we see significance differences. For example with Finland's growth log GDP, it did decline drastically but more controlled declination compared to the rest. However, the growth of log GDP went down even more below 6.5 log GDP in Finland than the rest in 2011. In order word, the 2008 crisis affected the Finland badly, the economic growth went lower in 2011 compared to the rest and faced difficulties in catching up with its peer countries.
  Due to limited space, only the most distinctive patterns found were discussed and explained. To remind as mentioned above, the explanation was given prior to undergo misinterpreting the graph wrongly. 


    2.    BMI Body Mass Index

The visualizing with differences among the fours countries but will we looking it with only two countries.
  We will first plot for one specific country (Norway). Since the data to be more accurate we multiply the actual BMI from data 10 times to visualize and understand the differences.
  
```{r}
BMI.differences <- Life_Expectancy_Data %>%
  filter(Year %in% 2000:2013) %>% 
  mutate(BMI=10*BMI) %>%
  select(Country, Year, BMI)

BMI.Norway <- BMI.differences %>% 
  filter(Country == "Norway" & Year %in% 2000:2013) %>% 
  select(Year, BMI)
```
In order to visualize the differences between countries, we first plot using machine learning.
BMI of Norway : -

```{r}
BMI.Norway<- BMI.Norway %>% 
  mutate(rate =(10*BMI))

BMI.Norway %>% 
  ggplot(aes(x = Year, y = BMI,color="Green")) + 
  geom_point() +
  labs(x = "YEAR", y =  "BMI")
```

Then we plot the BMI of Sweden using geom point.  BMI of Sweden :-

```{r}
BMI.Sweden <- BMI.differences %>% 
           filter(Country == "Sweden" & Year %in% 2000:2013) %>% 
           select(Year, BMI)
         
BMI.Sweden%>%
  ggplot(aes(x = Year, y = BMI,color="red")) + 
           geom_point() + 
  labs(x = "YEAR",y =  "BMI")
```

Here we are comparing only two countries and see the difference between Norway and Sweden with the given timeline. 

```{r}
differences_norswe = Life_Expectancy_Data %>%
  filter(Year %in% c(2000:2013),Country %in% c("Norway","Sweden")) %>%
  mutate(BMI)  
         
differences_norswe %>%
  filter(Country %in% c("Norway","Sweden"), Year %in% c(2000:2013)) %>%
  ggplot()+ geom_point(aes(x=Year,y=BMI,color=Country))
         
```

BMI with in Norway compared to Sweden might not see the significance difference but something happened in 2013 in Norway where BMI went down as illustrated in the graph.The differences between Norway and Sweden is interesting because these countries withhold the title of developed countries in the world. With wealth, comes education and with well-educated society leads to high standard living and access to better and high quality food. BMI measurements plays a significant role in country's development because it is the health we are talking about. We see that BMI in Norway and Sweden go up not due to GDP growth. GDP growth affects relatively less in achieving better BMI measurements. 

However, If we wish to compare the difference of BMI between four countries and then we try to assemble the coding as follows:

```{r}
  differences_nordics = Life_Expectancy_Data %>%
           filter(Year %in% c(2000:2013),Country %in% c("Denmark", "Finland", "Norway","Sweden")) %>%
           mutate(BMI)  
differences_nordics %>%
  filter(Country %in% c("Norway","Sweden", "Denmark", "Finland"), Year %in% c(2000:2013)) %>%
  ggplot()+ geom_point(aes(x=Year,y=BMI,color=Country))
         
```


Then we could see the difference among the four countries. Analytics. From 2010, Finland and Norway BMI ratio dropped to Mean BMI between 5 to 10. we are uncertain of the reasons why the differences were drastic but we see clear distinctive quantitative context which indicated that lower BMI, the healthier and the population is less overweight. 
BMI is defined as body weight measured in kilograms divided by the square of height in meters. BMI = Mass(kg)/height(m)^2. When looking through the country's data, mean-based method which included correlation analysis and linear regression modelling in order to measure the relationship between BMI and other factors overtime. 
how does BMI develop over year varies from countries to countries. x-axis tells us how BMI of a country changes overtime. However, the y-axis tell us the Mean BMI () tell us the development of BMI overtime and when comparing among countries, we get the differences of Mean BMI between countries over the period. 


    3.    Average consumption of Alcohol

 We first extract only annual average alcohol over the given period observations in liters from our data. Then we will compare consecutively afterwards with differences among the fours countries. The same procedures ran in R as before, imported the data. Then we filter with given time period, with four countries with variable country, year, alcohol. 

```{r}
Alcohol <-Life_Expectancy_Data %>% 
  filter(Year %in% c(2000:2013)) %>% 
  filter(Country %in% c("Sweden","Norway","Denmark","Finland")) %>% 
  mutate(lifeexp=`Life expectancy`) %>% 
  select(Country,Year,Alcohol)
view(Alcohol)
```

Annual Average consumption in Sweden:-

After we extracting the data, we first try to plot Sweden with the following code.
we filter Sweden from our four designated countries and then plot the year on x-axis with average alcohol consumption in liter on y-axis. 

```{r}
Alcohol %>% 
  filter(Country %in% c("Sweden")) %>% 
  ggplot+
  geom_line(mapping = aes(x = Year, y = Alcohol, color=Country)) +
  scale_y_continuous(labels = scales::comma)
```
Analytics on Sweden 
The above graph illustrates the average consumption of alcohol in liters inclines 2002 from 6.90, declining all the way to 6.5 in 2005 possibly due to restrictions and health precautions and education. However, there is correlation between alcohol and GDP in the case of Sweden in 2005. Since, GDP in 2005 in Sweden went down, the consumption of alcohol in 2005 in Sweden also went down. Therefore, the correlation persists and country's GDP growth and consume similar affects in Swedish economy. Our data proves that in the case of Sweden since GDP went down, the population can consume less or limited so, the alcohol consumption went down in other word, clear correlation of country's GDP with alcohol consumption. 


Annual average consumption of alcohol in Norway:-

```{r}
Alcohol %>% 
  filter(Country %in% c("Norway")) %>% 
  ggplot+
  geom_line(mapping = aes(x = Year, y = Alcohol, color=Country)) +
  scale_y_continuous(labels = scales::comma)
```

In Norway, however, we find the correlation between GDP and Alcohol consumption is opposite. When we see the deep decline slope of log GDP 1.9 in Norway in 2008, the alcohol consumption went up-to 6.75 the highest consumption of alcohol in Norway in the range of year 2000-2013. In other word, there is opposite effect in the relation between GDP and average consumption of alcohol presumably due to depression and mental health. in the case of Norway then GDP also might be a factor of populations consuming more alcohol in the crisis period as coping method but it does show the prominent result as in the case of Sweden where the GDP declines as the average consume of alcohol declines. 
Then we will compare all four countries. 
```{r}
Alcohol %>% 
  filter(Country %in% c("Denmark","Norway", "Sweden", "Finland")) %>% 
  ggplot+
  geom_line(mapping = aes(x = Year, y = Alcohol, color=Country)) +
  scale_y_continuous(labels = scales::comma)
```



All four countries analysis:- Although Norwegian and Swedish annual average alcohol consumption is high, it is relatively lower than Finland and Denmark. where the latter has the consumption range between 8 to 12 in liters. Interesting pattern with log GDP and alcohol consumption is that the growth of log GDP went down even more below 6.5 log GDP in Finland than the rest in 2011. The same year, with annual average consumption in Finland went up again to 9.81 from the constant declining in consumption since 2007 was 10.45 to 2010 was 9.72. Where we see the similar effects while Swedish case with correlation of alcohol consumption and GDP growth. In the case of Denmark, there was a constant declination in alcohol consume until 2009, a year after the financial crisis, it went up to 10.47 in 2011 where as the GDP growth was affected in Dane's economy after the crisis in 2010 which is where we also see the top point in 2010. 

```{r, echo=TRUE, results='hide'}

```


Conclusion:

In conclusion, this project aimed to explore the relationship between a country's economic growth, measured by GDP, and alcohol consumption, focusing on Norway, Sweden, Denmark, and Finland from 2000 to 2013. The analysis incorporated variables such as GDP, alcohol consumption, and BMI to delve into wealth, living standards, and income dynamics among the selected countries. Through the utilization of R programming, data wrangling, visualization, and machine learning tools, we strives to uncover patterns and insights. While acknowledging the limitations of graphical representations, the project emphasized the importance of detailed interpretation for a nuanced understanding of the data. Overall, this research contributes to the broader understanding of the interplay between economic factors and societal habits in the context of the selected Nordic countries.






