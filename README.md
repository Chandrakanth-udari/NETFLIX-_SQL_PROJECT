# Netflix Movies and TV Shows Data Analysis using SQL

![Alt text](https://github.com/Chandrakanth-udari/NETFLIX-_SQL_PROJECT/blob/main/logo.png)

## 📁 Dataset

- **File:** `netflix_titles.csv`
- **Source:** [Kaggle - Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows)
- **Records:** ~8,800+
- **Description:** This dataset contains information about Netflix’s movies and TV shows, including cast, country, director, release year, ratings, duration, and genres.

---

## 🧰 Tools & Technologies Used

- PostgreSQL
- SQL (CTEs, Window Functions, String Functions)
- SQL Client (pgAdmin, DBeaver, etc.)

---

## 🗃️ Database Setup

```sql
CREATE DATABASE "Netflix_db";

CREATE TABLE netflix (
    show_id      VARCHAR(5),
    type         VARCHAR(10),
    title        VARCHAR(250),
    director     VARCHAR(550),
    casts        VARCHAR(1050),
    country      VARCHAR(550),
    date_added   VARCHAR(55),
    release_year INT,
    rating       VARCHAR(15),
    duration     VARCHAR(15),
    listed_in    VARCHAR(250),
    description  VARCHAR(550)
);

## 🧠 Business Questions & Solutions

| # | Question |
|---|----------|
| 1️⃣ | Count the number of Movies vs TV Shows |
| 2️⃣ | Find the most common rating for Movies and TV Shows |
| 3️⃣ | List all Movies released in a specific year (e.g., 2020) |
| 4️⃣ | Top 5 countries with the most Netflix content |
| 5️⃣ | Identify the longest Movie by duration |
| 6️⃣ | Find content added in the last 5 years |
| 7️⃣ | Find all content by director ‘Rajiv Chilaka’ |
| 8️⃣ | List all TV Shows with more than 5 seasons |
| 9️⃣ | Count the number of content items per genre |
| 🔟 | Find each year and average release content in India |
| 1️⃣1️⃣ | Top 10 actors who appeared in most Indian content |
| 1️⃣2️⃣ | Categorize content by presence of keywords: “kill” or “violence” |

---

## 📌 Example SQL Queries

###   1. Count the Number of Movies vs TV Shows

```sql
SELECT type, COUNT(*) AS total
FROM netflix
GROUP BY type;

   2. Most Common Rating per Content Type

WITH RatingCounts AS (
  SELECT type, rating, COUNT(*) AS rating_count
  FROM netflix
  GROUP BY type, rating
),
RankedRatings AS (
  SELECT *, RANK() OVER (PARTITION BY type ORDER BY rating_count DESC) AS rnk
  FROM RatingCounts
)
SELECT type, rating AS most_common_rating
FROM RankedRatings
WHERE rnk = 1;


   3. Top 5 Countries with Most Content

SELECT country, COUNT(*) AS total_content
FROM (
  SELECT UNNEST(STRING_TO_ARRAY(country, ',')) AS country
  FROM netflix
) AS c
WHERE country IS NOT NULL
GROUP BY country
ORDER BY total_content DESC
LIMIT 5;

```

(See netflix_SQL_Script for all queries)
```
📂 Project Structure
NETFLIX-_SQL_PROJECT/
│
├── logo.png
├── netflix_titles.csv
├── netflix_SQL_Script.sql
└── README.md
```

📜 License
This project is licensed under the MIT License.

## 🙋‍♂️ Author

**Chandrakant Yadav**  
📧 udarichandrakanth@gmail.com  
🔗 [LinkedIn Profile](https://www.linkedin.com/in/chandrakanth-yadav-udari-a1376a32b/)


