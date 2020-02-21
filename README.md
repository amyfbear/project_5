# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png)Project 5 : Optimizing Evacuation Routes using Real-Time Traffic Information

- Amy Ontiveros-Bear
- Benjamin Haile
- Ruchika Sah

## Problem Statement

 In this project we were tasked with optimizing the best evacuation route from Central Park to Prospect Park.The ideal output should map the fastest route given live and historical traffic data. Since Tom Tom API essentially does this already we wanted to validate it’s efficiency. We will test our theory by utilizing DBSCAN to cluster historically dense traffic regions. Then compare the live routing mechanism of Tom Tom to our cluster output. The pseudo metric used will be silhouette score.
 
# Executive Summary

We decided to focus our map on routes between Central Park and Prospect Park. We also limited our data acquisition to January and February 2020, bearing in mind the scope of the project. Our methodology was as follows:

### Data Acquisition

Our data comes from two sources: the TomTom API and NYC Open Data. After obtaining a TomTom key, the service's API gave us detailed data on traffic incidents across NYC. This included the coordinates and location of each incident, as well as the type of incident and weather conditions. The API allowed us to collect this data in real-time, but could not give us sufficient data for modeling. Using the API to collect sufficient historical data would be too time-consuming. NYC Open Data offers a free dataset on traffic accidents that similarly details incidents by coordinates and location. This gave us access to thousands of rows of historical data, free to download in CSV format. We decided to train our model on the NYC Open Data dataset and make predictions using the TomTom data, using the coordinate and location features that they share. This way, we could generate an output based on both live and historical data.

## Executive Summary


**EDA & Outside Research:**

Our analysis shows that data collected from the TomTom API offers a fuller sense of traffic and road incidents. Although the NYC Open Data dataset is comprehensive, we see that the TomTom data can better say which types of incidents are more common and offers different insights into when incidents happen. The TomTom data is clearly valuable for predicting evacuation routes, because it demonstrates that measuring collisions alone is not enough to understand many possible events that can cause traffic. This data confirms certain observations on when incidents are most likely to happen, but also raises new questions about why certain events may happen when they do, as seen in the heatmaps in the EDA notebook.


**Modeling:**

We pulled data multiple times a day from the Tom Tom API to be able to get live data about road and traffic conditions in the city. After cleaning and doing basic EDA, in order to validate the efficiency of routing given by Tom Tom we decided to use an Unsupervised Model since we did not have a target variable. We used the DBSCAN Clustering Algorithm to cluster high density traffic areas in the city. Due to the fact that it is an UNSUPERVISED clustering algorithm there is no true way to evaluate it. The mechanism for clustering is that the neighborhood of a given radius has to contain  a minimum number of points.  Therefore the parameters of the model are the radius  and the number of points included in the cluster. For our modeling we utilized the coordinates of traffic incidents. We tried different values for the eps and minimum number of observations to get the best value counts for the clusters and minimizing the outliers. We also tried to get the best value for the Silhouette Score 
Being that there is no way to really evaluate the model, we still used pseudo metrics for our evaluation purposes.
The Silhouette Score shows the proximity and density of clusters and has values from -1 to 1. We chose this one because it is a better measurement for the relationship between our clusters.

**Mapping:**


Our job is to optimize and map the best evacuation route from Central Park to Prospect Park. Tom Tom API does this for us already, it is a multilingual, globally supported, reliable and free source for live traffic and routing data. Being that our client will need our project to be implemented on a global scale at some point, Tom Tom is ideal choice. We prove this by comparing its live routing mechanism overlaid on historical New York traffic clusters to validated its  efficiency by always routing around these clusters.


---

### Data Sources

[TomTom API](https://developer.tomtom.com/content/traffic-api-explorer#/Traffic%20Incident/get_traffic_services__versionNumber__incidentDetails__style___boundingBox___zoom___trafficModelID___format_)

[NYC Open Data](https://data.cityofnewyork.us/Public-Safety/Untitled-Visualization-Based-on-NYPD-Motor-Vehicle/6625-xkgg)

---

### Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|coord|object|TomTom|Latitude and longitude of the location(dicionary datatype)|
|day|object|TomTom|Day of the incident|
|delay|int64|TomTom|Delay caused by the incident in seconds (except in road closures)|
|description|object|TomTom|Description of the incident in the language requested|
|end_date|object|TomTom|Estimated end date of the incident, when available|
|from|object|TomTom|The name of the intersection or location where the traffic due to the incident starts|
|geometry|point|TomTom|Latitude and longitude of the location(point datatype)|
|hour|float64|TomTom|Hour of day when the incident occurred|
|id|object|TomTom|ID of the incident|
|latitude|float64|TomTom|Latitude of the incident's location|
|length|int64|TomTom|Length of the incident in meters|
|longitude|float64|TomTom|Longitude of the incident's location|
|month|object|TomTom|Month when the incident occurred|
|num_of_incidents|float64|TomTom|Number of incidents in this instance, if more than one|
|road_condition|object|TomTom|Road condition caused by the incident|
|to|object|TomTom|The name of the intersection or location where the traffic due to the incident ends|
|latitude|float|NYC Open Data|latitude of the coordinates of the accident|
|longitude|float|NYC Open Data|longitude of the coordinates of the accident|
|hour|int|NYC Open Data|hour of day when the accident occurred|
|zip code|float|NYC Open Data|zip code of the accident location|
|location|point|NYC Open Data|coordinates of the accident|
|crash date|object|NYC Open Data|date when the accident occurred|
|crash hour|object|NYC Open Data|time when the accident occurred|
|borough|object|NYC Open Data|borough where the accident occurred|

---

## Conclusion

We succesfully completed what we set out to accomplish in our problem statement and mapped the best evacuation route from Central Park to Prospect Park utilzing live traffic data. Tom Tom API is a multilingual, globally supported, reliable and free source for live traffic and routing data. Being that our client will need our project to be implemented on a global scale at some point this makes Tom Tom an ideal choice. We validated Tom Tom's efficiency by ensuring its live routing mechanism overlaid on a map of clustered historical New York traffic data will always route around them. This is because Tom Tom is already trained on historical traffic data. We obtained our clusters by using the DBSCAN clustering algorithm and clustering the historically traffic dense areas. Since it is an unsupervised model and it is being utilized for visual purposes only, a silhouette score of 0.40 will suffice. We performed the route validation trials several times with a 100% success rate. Tom Tom's accuracy was successfully validated by comparing street closures to NYC's traffic website on multiple runs as well. We are satisfised with the final maps because we were able to map everything we set out to do.

## Recommendations & Next Steps

For mapping we would use Geocoding that would allow us to use physical addresses instead of coordinates. Then over lay traffic flow polyline indicators on the live map for better interpretability. We would also do additional research on causes of traffic-dense hours and explore the outliers a bit more. Since eventually we hope it will be utilzed globally it would be interesting to try this exact project out in another language and apply it to other regions of the world.

## References

[NYC Street Closures](http://maps.nyc.gov/streetclosure/)

[Tom Tom Developer API](https://developer.tomtom.com/)

[New York Open Data- Collisions](https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Crashes/h9gi-nx95)

[Research into After-Hours Construction](https://www.nytimes.com/2019/09/27/nyregion/noise-construction-sleep-nyc.html)
