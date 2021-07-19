# World Bank

* Executive Summary
* Meta data - no. of rows, columns
* Summary Stats 
* Univariate (SIngle Column) - Histogram, Density Plot - Frequency
* Bivariate (Two Columns) - Scatter Plot - Correlation

#Questions to be answered from dataset
* Number of countries present in the dataset
* Number of years
* CO2 emission per country
* average min and max surface area of all countries in the dataset
* average co2 emissions for one location over the years
* Which country's manufacturing sector has largest contribution to GDP?
* Total population for each country?
* Urban population of countries where gdp < global avergage

# Number of countries
```sql
SELECT count(distinct country_code) FROM `patents-public-data.worldbank_wdi.wdi_2016`
```
Ans: 264

# Min year and Max year
```sql 
SELECT min(year) as minimum_year, max(year) as maximum_year
FROM `patents-public-data.worldbank_wdi.wdi_2016`
```
Ans: minimum_year: 1960	
maximum_year: 2016

# average, min and max surface area of all countries in the dataset
```sql
SELECT min(indicator_value) as minimum_surface_area, 
    max(indicator_value) as maximum_surface_area,
    avg(indicator_value) as average_surface_area 
FROM `patents-public-data.worldbank_wdi.wdi_2016` 
where 1=1 
--and lower(indicator_name) like '%surface%'
and indicator_name = 'Surface area (sq. km)'
```
Ans:  
![image](https://user-images.githubusercontent.com/87647771/126160913-57657978-187a-48c9-b5cf-e6a25209a69e.png)

# average, min and max surface area of all countries using Group by and Order by functions
```sql
SELECT
  country_name,
  MIN(indicator_value) AS minimum_surface_area,
  MAX(indicator_value) AS maximum_surface_area,
  AVG(indicator_value) AS average_surface_area
FROM
  `patents-public-data.worldbank_wdi.wdi_2016`
WHERE
  1=1
  --and lower(indicator_name) like '%surface%'
  AND indicator_name = 'Surface area (sq. km)'
GROUP BY
  country_name
ORDER BY
  average_surface_area DESC,
  country_name  -- double sort - first by avg_sa descending and then by country name
```
Ans:   ![image](https://user-images.githubusercontent.com/87647771/126164370-037d854e-cee9-4e3c-ac91-5b29a4651420.png)


# average co2 emissions for one location over the years
```sql
SELECT country_name as Country_Name, indicator_name, avg(indicator_value) as Avg_CO2_Emission
FROM
  `patents-public-data.worldbank_wdi.wdi_2016`
where 
    indicator_name = 'CO2 emissions (kt)'
GROUP BY 
    Country_Name, indicator_name
ORDER BY 
    Avg_CO2_Emission desc, Country_Name
```
Ans:  ![image](https://user-images.githubusercontent.com/87647771/126165764-e7820e60-91cb-4d16-815a-a1bca89b99f5.png)


* Which country's manufacturing sector has largest contribution to GDP?
* Total population for each country?
* Urban population of countries where gdp < global avergage

