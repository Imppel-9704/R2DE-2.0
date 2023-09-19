# Road to Data Engineer - Workshop 6
This workshop I'm going to create online report and online dashboard, using Google Looker Studio
Input : Data in BigQuery
Output : report / dashboard on Google Looker Studio

## Data in BigQuery
![Image](https://drive.google.com/uc?id=1HZ4xHRv7Sqy4-tiyif7Pw8vQJRDZtObG)

## Requirement 
  1. Team need dashboard that helps making decision about product and marketing.
  2. Production team need to know which book category is the best seller.
  3. Marketing team need to know total sales and total customers from each country.
  4. Marketing team need to know which book is the best seller for making marketing plans.
  5. Marketing team need the system that can search for sales quantities and country for make marketing plans easier.

![Image](https://drive.google.com/uc?id=13iNPAGb83Ohe6eLXzqB2I2uu1g_NqD9N)

## 1. Create View to bring some part of data to create dashboard
Purpose of creating View table is we want to limit data access for other teams. The data we'll use is
  - revenue
  - country
  - book name
  - customer ID
  - catogories
  - timestamp
  - book ID

```
CREATE VIEW r2de.vw_ws6 AS
SELECT
  timestamp,
  user_id,
  country,
  Book_ID,
  Book_Title,
  Categories,
  THBPrice
FROM `r2de.audible_data`
```

## 2. Create Dashboard
From the wireframe as above. So I create as follows

**filter country and month**
![Image](https://drive.google.com/uc?id=1w3kavjAf9ATSEapYk4KOg-0NQ6JFMjnW)

**total revenue and total customer**
![Image](https://drive.google.com/uc?id=19XLrZRoHHwqzjea2cHzX8XAH1WOZjTsP)

**Bubble map revenue by country**
![Image](https://drive.google.com/uc?id=1RNfMCV6nC6o-okzOOYXPxUA4PUrdzMJ7)

**Column chart transaction by revenue**
![Image](https://drive.google.com/uc?id=1Z2B53_aifD0yR7GbV-CnQH6RJOSjrBCu)

**Table The best selling books**
![Image](https://drive.google.com/uc?id=1FMYWdyWSQn2nljQrL4LemDX6_fK17lt3)

**Tree map for the best selling categories**
![Image](https://drive.google.com/uc?id=1xz_T7ix29_1VEJbxjhWGqSuzt3C54IaX)

## 3. Create Search system
From the requirement, Marketing team need the system that can search for book title and revenue. So I start create second page.
I create slider that can filter the books that have revenue from 1 to 30,000,000

**1. Create new parameter. set min = 0, max = 30,000,000**
![Image](https://drive.google.com/uc?id=180qpTQMpl9mV88tLH4Dkap_wrli7hGYa)

**2. Create new calculated field for using with the parameter.**
![Image](https://drive.google.com/uc?id=1Z5nYvcBauYGecKAu7kq74IOpPvKUvNao)

**3. Add filter to the table, only show the books that have value Calculated field = 1**
![Image](https://drive.google.com/uc?id=1FZ-ZQ-zBaUZYmBPcoGJXDNnAj8zxDvdr)

## Final Output
**Page 1**
![Image](https://drive.google.com/uc?id=1upiU2Ygq0_WgbYAOFgh9nIYWSpDU8_I2)

**Page 2**
![Image](https://drive.google.com/uc?id=1Rbdfqs1Q3n7WzV1D_7L0sGxML7Eqa-1H)

**File**
[Looker Studio Final Dashboard](ws6_exercise.pdf)