# COVID-19-Network

This project is part of the Rice Data Science CHRP.

## Goal

The goal of this project is to infer county level networks of COVID-19 counts. This is interesting because we can hopefully gain insight about which counties influenced COVID-19 counts in other counties.

## Data

I am using county level time series data of the COVID-19 cases for each county. I use data from The New York Times and can be found here https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-counties.csv.

## Discussion 

The pre-stated goal is lofty and there are many challenges. One big challenge is that COVID-19 case counts are incredibily imperfect. See this great article about the challenges of relying on counts - https://fivethirtyeight.com/features/coronavirus-case-counts-are-meaningless/. That being said, it is the best data I have at this point. Another challenge is that two counties may be unrelated, but simultaneously grow at the same rate. That means that interpretion of the network requires discretion, is it possible that county A acually influence county B? If they are neighboring counties, that isn't too unreasonable. If a county in the middle of North Dakota is influencing San Francisco? That may be less likely. 

## Model

This base of this model is a Vector AutoRegression (VAR) model. There are several major questions I still need to answer, but these will be discussed later. The model is more fully outlined in the file COVID-19_Model.pdf.

## File Organization

COVID-19_Model.pdf - Basic outline of the model
Clean Data and Run Initial Model.ipynb - Initial model results
ExamplePlot.png - example of what plots will be included in the shiny app. This figure shows the counties that influence Weschester County, NY. In the shiny app the figure will be interactive, meaning users can hover over counties and see the strength of influence.

## April 10 Update

I was able to lay the ground work this week so that I can refine the model going forward. I was able to find data, prepare the data for the model, implement a basic model, and display the results. The steps going forward shouldn't be too complicated.

This week's results can best be seen in ExamplePlot.png and Covid_network.csv. 

## Future work

#### Model

The initial results are found using a 5 day time lag, using total counts, and using ElasticNet on the raw counts. I would like to do more investigation into time lags and the role that plays. I would also like to look into using the number of new cases instead of total counts to see how the results compare. I would also like to investigate using a different model to account for the fact that the data are counts.

Because of the large number of counties, I had to filter the counties to only include counties that had non-zero observations for more than 50 days. This was a memory limit on my local machine, and I would like to expand this so that it can be done for all counties.

Finally, I would like to incorperate other data. The most first would be to info about how close counties are to each other and say that neighboring counties are more likely to have an association. This could be done using a Bayesian model and putting a prior on edge inclusion that included county proximity. Additional data that would be interesting to add is flight patterns between regions a county is located in.

#### Visualization

I would eventually like to provide a shiny app that allows a user to select a county and then display which other counties infuenced the selected county.




