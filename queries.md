![Ironhack Logo](https://i.imgur.com/1QgrNNw.png)

# Answers

### 1. All the companies whose name match 'Babelgum'. Retrieve only their `name` field.

db.companies.find({name:"Babelgum"}).projection({name:1,\_id:0})

Filter: {name:"Babelgum"}
Project: {name:1, \_id:0}

### 2. All the companies that have more than 5000 employees. Limit the search to 20 companies and sort them by **number of employees**.

db.companies.find({number_of_employees:{$gt:5000}}).limit(20).sort({number_of_employees:-1})

Filter: {number_of_employees:{$gt:5000}}
Sort: {number_of_employees:-1}
Limit: 20

### 3. All the companies founded between 2000 and 2005, both years included. Retrieve only the `name` and `founded_year` fields.

db.companies.find({$and:[{founded_year:{$gte:2000}}, {founded_year:{$lte:2005}}]}).projection({name:1,founded_year:1,\_id:0})

Filter:{$and:[{founded_year:{$gte:2000}}, {founded_year:{$lte:2005}}]}
Project:{name:1,founded_year:1,\_id:0}

### 4. All the companies that had a Valuation Amount of more than 100.000.000 and have been founded before 2010. Retrieve only the `name` and `ipo` fields.

db.companies.find({"ipo.valuation_amount":{$gt:100000000}}).projection({name:1,ipo:1,\_id:0})

Filter: {"ipo.valuation_amount":{$gt:100000000}}
Project: {name:1,ipo:1,\_id:0}

### 5. All the companies that have less than 1000 employees and have been founded before 2005. Order them by the number of employees and limit the search to 10 companies.

db.companies.find({$and:[{number_of_employees:{$lt:1000}},{founded_year:{$lt:2015}}]}).sort({number_of_employees:1}).limit(10)

Filter: {$and:[{number_of_employees:{$lt:1000}},{founded_year:{$lt:2015}}]}
Sort: {number_of_employees:1}
Limit: 10

### 6. All the companies that don't include the `partners` field.
db.companies.find({partners:{$size:0}})

Filter: {partners:{$size:0}}

### 7. All the companies that have a null type of value on the `category_code` field.
db.companies.find
Filter: {category_code:{$type:"null"}}

### 8. All the companies that have at least 100 employees but less than 1000. Retrieve only the `name` and `number of employees` fields.
db.companies.find({$and:[{number_of_employees:{$gte:100}}, {number_of_employees:{$lt:1000}}]}).projection({name:1,number_of_employees:1,\_id:0})

Filter:{$and:[{number_of_employees:{$gte:100}}, {number_of_employees:{$lt:1000}}]}
Project: {name:1,number_of_employees:1,\_id:0}

### 9. Order all the companies by their IPO price in a descending order.
db.companies.sort({"ipo.valuation_amount":-1})

Sort: {"ipo.valuation_amount":-1}

### 10. Retrieve the 10 companies with most employees, order by the `number of employees`
db.companies.sort({number_of_employees:-1}).limit(10)

Sort: {number_of_employees:-1}
Limit: 10

### 11. All the companies founded on the second semester of the year. Limit your search to 1000 companies.
db.companies.find({$and:[{founded_month: {$gt:6}},{founded_month:{$lt:13}}]}).limit(1000)

Filter: {$and:[{founded_month: {$gt:6}},{founded_month:{$lt:13}}]}
Limit: 1000

### 12. All the companies founded before 2000 that have an acquisition amount of more than 10.000.000
db.companies.find({$and:[{founded_year: {$lt:2000}},{"acquisition.price_amount":{$gt:10000000}}]})

Filter: {$and:[{founded_year: {$lt:2000}},{"acquisition.price_amount":{$gt:10000000}}]}

### 13. All the companies that have been acquired after 2010, order by the acquisition amount, and retrieve only their `name` and `acquisition` field.
db.companies.find({"acquisition.acquired_year": {$gt:2010}}).projection({name: 1, \_id:0, acquisition:1}).sort({"acquisition.price_amount": -1})

Filter: {"acquisition.acquired_year": {$gt:2010}}
Projection: {name: 1, \_id:0, acquisition:1}
Sort: {"acquisition.price_amount": -1}

### 14. Order the companies by their `founded year`, retrieving only their `name` and `founded year`.
db.companies.find().projection({name: 1, \_id:0, founded_year:1}).sort({founded_year: -1})

Projection: {name: 1, \_id:0, founded_year:1}
Sort: {founded_year: -1}

### 15. All the companies that have been founded on the first seven days of the month, including the seventh. Sort them by their `acquisition price` in a descending order. Limit the search to 10 documents.
db.companies.find({founded_day: {$lte:7}}).sort({"acquisition.price_amount": -1}).limit(10)

Filter: {founded_day: {$lte:7}}
Sort: {"acquisition.price_amount": -1}
Limit: 10

### 16. All the companies on the 'web' `category` that have more than 4000 employees. Sort them by the amount of employees in ascending order.
db.companies.find({$and:[{category_code: "web"}, {number_of_employees: {$gt: 4000}}]}).sort({number_of_employees: 1})

Filter: {$and:[{category_code: "web"}, {number_of_employees: {$gt: 4000}}]}
Sort: {number_of_employees: 1}

### 17. All the companies whose acquisition amount is more than 10.000.000, and currency is 'EUR'.
db.companies.find({$and:[{"acquisition.price_amount":{$gt:10000000}}, {"acquisition.price_currency_code": "EUR"}]})

Filter: {$and:[{"acquisition.price_amount":{$gt:10000000}}, {"acquisition.price_currency_code": "EUR"}]}

### 18. All the companies that have been acquired on the first trimester of the year. Limit the search to 10 companies, and retrieve only their `name` and `acquisition` fields.
db.companies.find({"acquisition.acquired_month":{$lt:4}}).projection({name: 1, \_id:0, acquisition:1})

Filter: {"acquisition.acquired_month":{$lt:4}}
Projection: {name: 1, \_id:0, acquisition:1}

### 19. All the companies that have been founded between 2000 and 2010, but have not been acquired before 2011.
db.companies.find({$and:[{founded_year:{$gte:2000}},{founded_year:{$lte:2010}},{$or:[{"acquisitions.0.acquired_year":{$gte:2011}},{acquisitions:"null"}]}]})

Filter: {$and:[{founded_year:{$gte:2000},{founded_year:{$lte:2010}},{$or:[{"acquisitions.0.acquired_year":{$gte:2011}},{acquisitions:"null"}]}]}
