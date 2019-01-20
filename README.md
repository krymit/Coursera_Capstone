# Coursera Capstone
IBM Data Science Capstone Project

## Battle of Berlin Neighborhoods (Week 1)

### Introduction:  
Customers are interested in opening up restaurants of different types and nationalities. So the distribution of restaurant types in Berlin neighborhoods is of interest. First, are restaurants, especially international ones, common for that area? Which ones are the most common types (and therefore maybe oversaturated)? How diverse is the distribution of restaurant types? And lastly, how similar are the neighborhoods based on their restaurant landscape (so if a certain restaurant type fits into one neighborhood, which other neighborhoods are suitable)? 

### Data:  
A list of Berlin neighborhoods is collected from Wikipedia. The coordinates of the neighborhoods are acquired with the geopy library. Information on restaurant categories in a neighborhood can then be obtained with Foursquare's API. Here, the coordinates of each neighborhood are passed and up to 100 venues of the section 'food' within a radius of 2000 m are collected. The radius is small enough that the exploration search queries don't intersect. The data is collected in pandas DataFrames, which enable various manipulations of data and clear overviews. Statistical information can also be obtained by using pandas. For similarity measures, scipy libraries for clustering and depicting a dendrogram (tree-like diagram of hierarchical clusters) are utilized. A cluster size can be set based on correlation among the neighborhood venues. Finally, a map is depicted which marks the neighborhood according to their cluster.  

#### Example of information extracted from data:  

A dataframe with the latitude and longitude values for each neighborhood, which were obtained via geopy.geolocator:  

Neighborhood	Latitude	Longitude
0	Mitte	52.517690	13.402376
1	Pankow	52.597811	13.436383
2	Friedrichshain-Kreuzberg	52.515306	13.461612
3	Charlottenburg-Wilmersdorf	52.507856	13.263952
4	Neukoelln	52.481150	13.435350
5	Lichtenberg	52.532161	13.511893
6	Marzahn-Hellersdorf	52.522523	13.587663
7	Reinickendorf	52.604763	13.295287
8	Steglitz-Zehlendorf	52.429205	13.229974
9	Tempelhof-Schoeneberg	52.440603	13.373703
10	Spandau	52.519267	13.195439
11	Treptow-Koepenick	52.417893	13.600185

Then, a dataframe with food venue information from Foursquare is created (with Venue Category being the information of highest interest), the first five entries are shown:  

Neighborhood Neighborhood Latitude	Neighborhood Longitude Venue	Venue Category
0	Mitte	52.51769	13.402376	Block House	Steakhouse
1	Mitte	52.51769	13.402376	THE REED	Restaurant
2	Mitte	52.51769	13.402376	Café 93	Café
3	Mitte	52.51769	13.402376	Ma'loa Poké Bowl Poke Place
4	Mitte	52.51769	13.402376	Rotisserie Weingrün	Restaurant
...

The categories can be one-hot encoded, so that each neighborhood has a listing of occurences (e.g. African Restaurant,	American Restaurant,	Argentinian Restaurant,	Asian Restaurant,	Austrian Restaurant,	BBQ Joint,	Bagel Shop	...). There are 70 types in total.  

Some statistical infos such as maximum frequency of a type, standard deviation etc. can be obtained with pandas describe():  

Neighborhood	Number of restaurant types	Std dev Frequency	Variance	Maximum frequency
0	Mitte	36	0.021841	0.000477	0.120000
2	Friedrichshain-Kreuzberg	34	0.030861	0.000952	0.210000
3	Charlottenburg-Wilmersdorf	31	0.026793	0.000718	0.151515
...

Also, a list with top venues of each neighborhood is created:  

FRIEDRICHSHAIN-KREUZBERG
                           Venue  Frequency
0                           Café       0.21
1  Vegetarian / Vegan Restaurant       0.10
2                    Pizza Place       0.09
...

Clusters are created with scipy's linkage() and depicted with dendrogram(). With the folium library a Berlin map with cluster markers is shown.




