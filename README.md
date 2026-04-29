# SQL-Intermediate

#Standard deviation is a way to measure how much a set of values varies or spreads out. The formula is: The formula in words: 
#The sum of the difference between the price to the mean (average) price in the power of 2 divided by the number of values in the total. Return the squared STD of the prices. name the column as STD.
SELECT SUM((price - (select AVG (price) FROM items)) * (price - (select AVG(price) FROM items))) / COUNT(*)
AS STD
FROM items;

#Calculate, for each food type, the average pH and the difference between the maximum and minimum pH values. name the columns: type, ph_average, ph_max_min_diff. 
#Sort the results by the difference in descending order. Use the ROUND(value, decimal) to round each result to two decimal places.
SELECT type, ROUND(AVG(pH), 2) AS ph_average, ROUND(MAX(pH) - MIN(pH), 2) AS ph_max_min_diff
FROM foods
GROUP BY type
ORDER BY MAX(pH) - MIN(pH) DESC;

#You have a cybersecurity firm that experienced an arbitrary attack, resulting in all of your systems shutting down. To solve this issue, you need to identify all of the events that appear suspicious. A suspicious event meets one or more of the following criteria:
#Its size is significantly different from the average normal event size of 50MB (you'll need to analyze the data in the table to determine the thresholds for 'too small' and 'too big')
#It was created before the year 2000. It has a missing name. Your task:
#Examine the provided table of events to determine what should be considered 'too small' or 'too big' based on the distribution of event sizes. Identify all suspicious events based on the criteria mentioned above.
#Return the event IDs and their names in descending order by their ID. Note: The exact thresholds for 'too small' and 'too big' should be inferred from the data. 
#Look for patterns or outliers in the event sizes to make this determination."
SELECT id, name
FROM events
WHERE size < 1 or size > 100 OR year < 2000 OR name IS NULL
ORDER BY id DESC;

#Fetch the top 5 severe criminal names in descending order (by severe_score) that are not listed in the police report. A severe criminal is someone who matches the following criteria:
#report is either empty, or the report contains one of the following letters: g, b, G, or B. Map is one of the following places: Caerleon, Dewsbury, Kirekwall, Findochty. Name the column as worst_criminals.
SELECT name AS worst_criminals
FROM police_report
WHERE (report IS NULL OR report = '' OR report LIKE '%g%' OR report LIKE '%b%' OR report LIKE '%G%' OR report LIKE '%B%') AND map IN ('Caerleon', 'Dewsbury', 'Kirekwall', 'Findochty')
ORDER BY severe_score DESC
LIMIT 5;
