# Data
These data were originally downloaded from the [Humanitarian Data Exchange](https://data.humdata.org/), specifically: 
- [ICA Mali - Prevalence of Global Acute Malnutrition](https://data.humdata.org/dataset/wfp-geonode-ica-mali-prevalence-of-global-acute-malnutrition) as geojson. The attributes for each polygon show down to the [3rd admin unit](https://en.wikipedia.org/wiki/Cercles_of_Mali), however the metadata via HDX explains that the data were collected at the first-level administrative unit. A technical paper about the data collection (in French) can be [accessed here](https://geonode.wfp.org/documents/8503). 
- [Mali Health sites](https://data.humdata.org/dataset/mali-healthsites) as `.csv`.

## Data Prep
For Mali Health Sites, I edited the headers in the csv for clarity then took the following steps to optimize the data for my purposes.
1. Searched all records to identify those that did not include any lat/lon information and removed 140 records. The dataset in this repo contain 1122 records.
2. Reduced the properties of the data set to reduce file size. I kept only `X`, `Y`, `amenity`, `name` properties and reduced the precision of x/y coordinates to 6 decimal places, which roughly equates to precision of less than five inches.  
3. Manually searched through records to find French characters that hadn't rendered properly (e.g. é, ô, etc). Changes were based on my familiarity with French and, when in doubt, lat/longs were checked on openstreetmap.org to see full name rendered. 
4. Converted to geojson using https://odileeds.github.io/CSV2GeoJSON/. 
