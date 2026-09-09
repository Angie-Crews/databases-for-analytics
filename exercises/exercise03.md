# Exercise 03: MongoDB – Document Queries and Analysis

- Name: Angie Crews
- Course: Database for Analytics
- Module: 3
- Database Used: MongoDB
- Dataset: `restaurants-json.json`

---

## Instructions

- Import the provided `restaurants-json.json` file into MongoDB.
- All commands must be **executed by you** in the MongoDB shell or MongoDB Compass.
- For each query:
  - Include the MongoDB command in a fenced code block
  - Include a **screenshot** showing the command and its result
- Store screenshots in the `screenshots/` folder and embed them below each answer.

---

## Question 1

When importing the documents from `restaurants-json.json`,
**how many documents were imported into your collection**?

### Answer

Number of documents imported = 25,358

### Screenshot

_Show evidence of how you determined this (for example, a count query)._

```javascript
db.restaurants.countDocuments({})
```

![Q1 Screenshot](screenshots/exercise_03/q1_document_count.png)

---

## Question 2

Before writing queries on the data,
**what command** do you use to set the
**MongoDB shell to operate on the `44661` database**?

### MongoDB Command

```javascript
use 44661
```

### Screenshot

![Q2 Screenshot](screenshots/exercise_03/q2_use_database.png)

---

## Question 3

Using your `restaurants` collection in the `44661` database,
write the MongoDB query needed to
**locate all documents in the `"Queens"` borough**.

### MongoDB Query

```javascript
db.restaurants.find({ borough: "Queens" })
```

### Screenshot

![Q3 Screenshot](screenshots/exercise_03/q3_queens_restaurants.png)

---

## Question 4

Using your `restaurants` collection in the `44661` database,
write the MongoDB query needed to
**find the number of restaurants in the `"Queens"` borough**.

### MongoDB Query

```javascript
db.restaurants.countDocuments({ borough: "Queens" })
```

### Screenshot

![Q4 Screenshot](screenshots/exercise_03/q4_queens_count.png)

---

## Question 5

Using your `restaurants` collection in the `44661` database,
write the MongoDB query needed to
**find the number of restaurants** in the `"Queens"` borough
**whose cuisine is `"Hamburgers"`**.

### MongoDB Query

```javascript
db.restaurants.countDocuments({ borough: "Queens", cuisine: "Hamburgers" })
```

### Screenshot

![Q5 Screenshot](screenshots/exercise_03/q5_queens_hamburgers.png)

---

## Question 6

Using your `restaurants` collection in the `44661` database,
write the MongoDB query needed to
**find the number of restaurants in Zipcode `10460`**.

**Hint: Embedded Documents** "address.zipcode" is in quotation marks because we're querying a nested field, and "10460" is also in quotation marks because the zipcode is stored as text in this dataset.

### MongoDB Query

```javascript
db.restaurants.countDocuments({ "address.zipcode": "10460" })
```

### Screenshot

![Q6 Screenshot](screenshots/exercise_03/q6_zipcode_count.png)

---

## Question 7

Using your `restaurants` collection in the `44661` database,
write the MongoDB query needed to
**display only the names of restaurants in Zipcode `10460`**.

**Query Note: Project Fields** The query uses "address.zipcode" to search the embedded address document for restaurants in Zipcode 10460, and the projection limits the results to restaurant names. I added .forEach(r => print(r.name)) to print each restaurant name on its own line and remove the extra spacing from the standard MongoDB shell output.

Your output should resemble:

```json
{ name: "Wild Asia" }
{ name: "Terrace Cafe" }
{ name: "African Terrace" }
{ name: "Cool Zone" }
{ name: "Beaver Pond" }
...
```

### MongoDB Query

```javascript
db.restaurants.find({ "address.zipcode": "10460" }, { _id: 0, name: 1 }).forEach(r => print(r.name))
```

### Screenshot

![Q7 Screenshot](screenshots/exercise_03/q7_zipcode_names.png)

---

## Question 8

Using your `restaurants` collection in the `44661` database,
write the MongoDB query needed to
**display only the names of restaurants whose name contains `"IHOP"`**,
ignoring case.

Your results should include:

- `"Ihop"`
- `"Ihop Restaurant"`

### MongoDB Query

Query Note: The /IHOP/i regular expression searches for restaurant names containing "IHOP" while ignoring capitalization, and the projection displays only the restaurant name. To make the results easier to read without the extra spacing, .forEach(r => print(r.name)) can be added to print each matching name on a single line.

```javascript
db.restaurants.find({ name: /IHOP/i }, { _id: 0, name: 1 }).forEach(r => print(r.name))
```

### Screenshot

![Q8 Screenshot](screenshots/exercise_03/q8_ihop_case_insensitive.png)
