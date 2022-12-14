# AVERAGE TEMPERATURE
SELECT AVG(temperature) 
FROM `skillful-coast-340323.demos.weather_nyc` 
WHERE date BETWEEN '2020-06-01' AND '2020-06-30'
 

# BETWEEN
SELECT
	Date, purchase_price
FROM customer_data.purchases
WHERE
	Date BETWEEN ‘2020-12-01’ AND ‘2020-12-20’

# CAST
SELECT
     CAST(purchase_price AS FLOAT64)
FROM customer.data_purchase
ORDER BY purchase_price DESC

#SELECT
    CAST(date AS date) AS date_only
FROM customer_data.purchases
The above statement changes SQL from recognizing the dates as datetime (2020-12-12T0:00:00) to only date (2020-12-12)

# CAST(expression AS typename)    Where expression is the data to be converted and typename is the data type to be returned.

## Converting a number to a string: 
SELECT CAST(MyCount AS String) FROM MyTable
In the above SQL statement, the following occurs: SELECT indicates that you will be selecting data from a table. CAST indicates that you will be converting the data you select to a different data type. AS comes before and identifies the data type which you are casting to. STRING indicates that you are converting the data to a string. FROM indicates which table you are selecting the data from
Converting String to a number:
SELECT CAST(MyVarcharCol AS INT) FROM MyTable
CAST indicates that you will be converting the data you select to a different data type. AS comes before and identifies the data type which you are casting to. INT indicates that you are converting the data to an integer
Convert date to a string:
SELECT CAST(MyDate AS STRING) FROM MyTable
Converting a date to a datetime: Datetime values have the format of YYYY-MM-DD hh: mm: ss format
SELECT CAST (MyDate AS DATETIME) FROM MyTable
The SAFE_CAST function: Using the CAST function in a query that fails returns an error in BigQuery. It returns null instead of error. 
SELECT SAFE_CAST (MyDate AS STRING) FROM MyTable
 
CONCAT
SELECT
	CONCAT(product_code, product_color) AS new_product_code
FROM customer_purchase.data
WHERE
	Product = ‘couch’

COALESCE
SELECT
	COALESCE(product, product_code) AS product_info
FROM customer_data.purchase
Return non-null values in a list

CASE
The CASE statement goes through one or more conditions and returns a value as soon as a condition is met
SELECT
	Customer_id
	CASE 
		WHEN first_name = ‘Tnoy’ THEN ‘TONY’
		ELSE first_name
		END AS cleaned_name
FROM customer.data
 
DISTINCT
SELECT  DISTINCT fuel_type
FROM cars.car_info;
SELECT DISTINCT name
FROM playlist
ORDER BY playlist_id

LENGTH
SELECT length (title) AS letters_in_title, album_id
FROM album
WHERE letters_in_title < 4
The function LENGTH(title) < 4 will return any album names that are less than 4 characters long. The complete query is SELECT * FROM album WHERE LENGTH(title) < 4. The LENGTH function counts the number of characters a string contains.
TRIM

MIN/MAX
SELECT
    MIN(length) AS min_length,
    MAX(length) AS max_length
FROM cars.car_info;



Order By
SELECT *
FROM movie_data.movies
ORDER BY Release_date DESC

SELECT * 
FROM movies.data
WHERE Genre = ‘Comedy’
AND Revenue >  30000000
ORDER BY Release_date DESC

SELECT total
FROM invoice
WHERE billing_city = "Chicago"
ORDER BY total ASC


SELECT County_of_Residence 
FROM `bigquery-public-data.sdoh_cdc_wonder_natality.county_natality` 
ORDER BY Births ASC 
LIMIT 10
 
SELECT County_of_Residence 
FROM `bigquery-public-data.sdoh_cdc_wonder_natality.county_natality` 
WHERE year = '2018-01-01'
ORDER BY Births DESC 
LIMIT 10
The year had to be in ‘ ‘ for it to work, and since it is in date formate, it would not work as simply 2018.
 

SELECT
The meteorologists who you’re working with have asked you to get the temperature, wind speed, and precipitation for stations La Guardia and JFK, for every day in 2020, in descending order by date, and ascending order by Station ID. Use the following query to request this information:
SELECT stn, date,
	IF(temp=9999.9, NULL, temp) AS temperature,
	IF(wdsp="999.9", NULL, CAST(wdsp AS Float64)) AS wind_speed,
	IF(prcp=99.99, 0, prcp) AS precipitation
FROM  `bigquery-public-data.noaa_gsod.gsod2020`
WHERE stn="725030" -- La Guardia
	OR stn="744860" -- JFK
ORDER BY  date DESC, stn ASC
-- Use the IF function to replace 9999.9 values, which the dataset description explains is the default value when temperature is missing, with NULLs instead.
-- Use the IF function to replace 999.9 values, which the dataset description explains is the default value when wind speed is missing, with NULLs instead. -- Use the IF function to replace 99.99 values, which the dataset description explains is the default value when precipitation is missing, with NULLs instead.
 
SUBSTR
SELECT  customer_id,
    SUBSTR(country,1,3) AS new_country
FROM customer
ORDER BY country
The statement SUBSTR(country, 1, 3) AS new_country will retrieve the first 3 letters of each state name and store the result in a new column as new_country. The complete query is SELECT customer_id, SUBSTR(country, 1, 3) AS new_country FROM customer ORDER BY country. The SUBSTR function extracts a substring from a string. This function instructs the database to return 3 characters of each country, starting with the first character. 
SELECT Invoice_id,
	SUBSTR(billing_city,1,4) AS new_city
FROM invoice
ORDER BY billing_city
Billing city= city, 1=starting position in string, 4=how many you return

UPDATE
UPDATE  cars.car_info
     SET num_of_doors = "four"
WHERE  make = "dodge" AND fuel_type = "gas" AND body_style = "sedan";

WHERE
SELECT   *
FROM   cars.car_info 
WHERE  num_of_doors IS NULL;

SELECT * 
FROM movies.data
WHERE Genre = ‘Comedy’
Because the genre is a string, you need to put the ‘ ‘ around the string name. Capitalizations matter

SELECT CustomerId
FROM invoices
WHERE BillingCountry = 'Germany' AND Total > 5
