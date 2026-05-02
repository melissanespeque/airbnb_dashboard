# Descriptive Dashboard - Airbnb Data

### Objective:

This dashboard was developed for personal projects. I chose to focus on Airbnb because it is a topic that interests me and resonates with me.
The goal of this dashboard is to provide a business perspective—helping someone looking to start an Airbnb business make decisions about which city, region, and type of property to target, among other factors. It also provides information that maps the profile of hosts.
Data available at: https://www.kaggle.com/datasets/mysarahmadbhat/airbnb-listings-reviews

### Challenges:

One of the biggest challenges was data processing. The data on city and region was unstructured, so I chose to import city-state-country dimension tables. This was also to facilitate other visualizations, which I chose not to develop at this time.
Since there wasn’t a very clear data dictionary, I faced challenges in interpreting some data and determining how to normalize it.
The result is not perfect; I chose to overlook some details at this stage, as this is a basic study. For example, I did not normalize currency at this time. I tried to formulate and translate everything into Brazilian Portuguese to facilitate understanding.
Data from 8 cities in 8 different countries were analyzed, considering accommodations starting from January 1, 2018, with no distinction made for the pandemic period.
Metrics Created (DAX):

![image](https://github.com/user-attachments/assets/ddc5856b-9c16-4c6a-a8ba-d7a864a9da85)

Dimension table Calendar, considering data from 01/01/2018 to 31/12/2022

![image](https://github.com/user-attachments/assets/5fcbebb5-ec66-499c-a2f0-60fe725f9418)

Measure to identify the city with the highest average score, based on the overall average score per city

![image](https://github.com/user-attachments/assets/9b1ad461-8fb5-490e-aa83-e7e634005784)

Medida criada para obter o Score médio de cada cidade, a partir da medida anterior de Média Score

![image](https://github.com/user-attachments/assets/ac8b8c2b-a159-47d7-bce1-881bc5b26d28)

A metric designed to calculate the average score for each city, based on the previous “Average Score” metrics

![image](https://github.com/user-attachments/assets/cb596dab-4e40-4be2-a381-0e3c5c4232ae)

Metric for the amount of hosts

### Data processing:

Removing outliers by filtering for [accomodates] ≤ 10 and [bedrooms] ≤ 7;
Normalization of price per night: using Norm Price = [price]/[minimum_nights] and setting [Norm Price] <= 1100 and [minimum_nights] <= 31;
Handling of null values;
Translation of items into Portuguese;
Assigning the following categories to the accommodation rating: If Score = 0, “Invalid”; If Score <= 20, “Very Poor”; Score <= 40, “Poor”; Score <= 60, “Fair”; Score <= 80, ‘Good’; Others, “Excellent”;
> = Table.AddColumn(#“Replaced Value”, ‘Rating’, each if [review_scores_rating] = 0 then “Invalid” 
> else if [review_scores_rating] <= 20 then “Very Poor” 
> else if [review_scores_rating] <= 40 then “Poor” 
> else if [review_scores_rating] <= 60 then “Fair” 
> else if [review_scores_rating] <= 80 then “Good” else “Excellent”)
> 
### Data model:
![image](https://github.com/user-attachments/assets/90865b2f-6871-443f-b5b9-d2d4ed31109a)

### Report:

Filters: You can filter by date range, city, property rating, and room type;
Accommodations by city: Number of different properties available for lodging by city;
Price by city and room type: View of the average price by city, broken down by accommodation type (entire place, hotel room, private room, or shared room);

Average Score by City: Average score for each city;
![image](https://github.com/user-attachments/assets/25a52464-3346-467e-92ba-9cb6cbb454c0)

Distribuição das hospedagens por ano: é possível fazer o drill down para obter a informação por mês. Mostra quantas hospedagens foram fechadas por mês, ano. Legendado por cada cidade;
Distribuição do preço por hospedagens: mostra quantas hospedagens possuem aquele valor por noite (preço normalizado);
Hospedagens por ano e mês: visualização simples para mostrar a quantidade de hospedagens fechadas a cada ano/mês, podendo identificar momentos de alta e baixa temporada;
Preço médio por ano e tipo de quarto: é possível fazer o drill down para obter a informação por mês. Monstra a variação da média mensal do preço, sendo cada linha representada por um tipo de quarto;
Distribuição da avaliação por ano e mês: mostra a avaliação média geral;

![image](https://github.com/user-attachments/assets/cde9fb21-8b6b-4067-972f-66ba3a41421b)

Breakdown of bookings by year: You can drill down to view the data by month. Shows how many bookings were made per month and year. Categorized by city;
Price breakdown by booking: Shows how many bookings are priced at that rate per night (standardized price);
Bookings by year and month: a simple visualization showing the number of bookings made each year/month, allowing you to identify peak and off-peak seasons;
Average price by year and room type: you can drill down to view the information by month. Shows the variation in the monthly average price, with each line representing a room type;
Rating distribution by year and month: shows the overall average rating;

![image](https://github.com/user-attachments/assets/288d6b78-adf4-4f9e-8f8d-4b70285cfdcf)

Average Score by Response Time: shows the variation in the average score according to each response time category;
Stays by Review: within each review category, how many stays each one received. The high number of “Invalid” reviews is due to many guests not leaving a review for their stay;
Hosts with the most stays: indicates the Host ID that has completed the most stays;
Stays by room type: indicates how many stays there are per room type category;
Number of hosts by verified identity: indicates whether there is any difference between hosts who have verified their accounts and those who have not; 

![image](https://github.com/user-attachments/assets/f0ba13d3-3837-4ca2-8214-2e850750376b)

### Conclusion:
It is possible to draw some insights from the dashboard, such as:
Mexico City has the highest average rating and ranks 7th in terms of the number of accommodations, indicating significant room for growth;
The average daily rate for a hotel room is, on average, more expensive than the daily rental rate for an entire property;
Accommodations offering “Entire Place” listings were also the most sought-after, with 72% rated as Good or Excellent;
Among others. There are many adjustments I plan to make in the future, but I decided to share how it looks right now.
