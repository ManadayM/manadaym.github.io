# SQL Correlated Subqueries

This post documents correlated subqueries in SQL.

<!--more-->

Lately, I'm refining my database skills through one of the Udemy course on SQL and PostgreSQL by Stepehn Grider. Yesterday, I came across the topic of Correlated Subqueries. I found it a bit difficult to understand at first due to my limited exposure to the database side. This blog post is an attempt to document my understanding on the same.

In simple terms, a correlated subquery is a query that depends for its value on the outer query. 

We can visualize correlated queries as two-level nested $for$ loops. The following code snippet mimics a car assembly where each car frame (outer loop) is passed through a set of assembly operations (inner loop). Here, the inner loop `assembly` is dependent on a value from the outer loop `frames`.

```javascript
let frames = ['car frame 1', 'car frame 2', 'car frame 3'];

let assembly = [
	'Installing engine',
	'Installing wiring',
	'Installing steering',
	'Installing seats',
	'Installing doors',
	'Installing wind-sheilds',
	'Installing tyres'
];

for (let i = 0; i < frames.length; i++) {

	for (let j = 0; j < assembly.length; j++) {
	
		console.log(`--> ${assembly[j]} for '${frames[i]}'.`);

	} // End of inner for loop

}// End of outer for loop
```

## Correlated Subqueries in SQL

Let's say, we have a `products` table in our database. We want to find the most expensive product for each product category. The highlighted rows will be part of our query result.

<aside>
💡 The SQL dump to create this table and dummy data can be accessed from this [gist](https://gist.github.com/ManadayM/715980c2d32987608b8f8df0c2cd9299). You can play with it on [pg-sql.com](https://pg-sql.com/).

</aside>

| id | name | category | price |
| --- | --- | --- | --- |
| 1 | Shirt | apparel | 876 |
| 2 | T-shirt | apparel | 650 |
| 3 | Diet coke | beverages | 15 |
| 4 | Sprite | beverages | 25 |
| 5 | Optical mouse | electronics | 100 |
| 6 | Pendrive | electronics | 125 |
| 7 | SSD | electronics | 500 |
| 8 | Webcam | electronics | 425 |

It is very important that we understand the SQL query execution order.

![Query Execution Order]({{ site.url }}/public/images/2022-01-13-sql-correlated-subqueries/query-execution-order.png)

### Fixed category based subquery

First, let's write a simple query that returns the most expensive product for the *apparel* category.

```sql
SELECT name, category, price
FROM products 
WHERE price = (
	SELECT MAX(price)
	FROM products 
	WHERE category = 'apparel'
);
```

Let's dissect this query by Query Execution Order

1. The `FROM` section will execute and return all rows from the `products` table.
2. The `WHERE` section will execute the sub-query against each resultant row returned from the `FROM` section. The subquery will be executed in the following order.
    1. The `FROM` section in the *subquery* will return all products row to the *subquery*.
    2. The `WHERE` section in the *subquery* will filter out all products that belong to *apparel* category.
    3. The `SELECT` section will perform `MAX` aggregation on the price column for the *apparel* category.
3. The subquery will return a scalar value to the outer query. This will be the maximum price for an apparel product. That'd look like as follows
    
    ```sql
    SELECT name, category, price FROM products WHERE price = 876;
    ```
    
4. The output of this query will be as follows.
    
    
    | name | category | price |
    | --- | --- | --- |
    | Shirt | apparel | 876 |

The crux of this section is that each row from the outer query will be matched against all rows from the inner query.

I know this not our end goal. I also hear you, what if there would be another product from a different category but having the same price? Yes, that would be part of this query's result.

The sole intention for this section was to explain the query execution order in the context of correlated subquery where inner query is dependent on the outer query.

### Correlated subquery

We want to achieve dynamism in our above query so that it returns most expensive product of each product category instead of one fixed category. Let's tweak our query as follows.

```sql
SELECT name, category, price  
FROM products AS main 
WHERE main.price = (
	SELECT MAX(price) 
	FROM products AS sub
	WHERE sub.category = main.category
);
```

We aliased the outer query as `main` and the inner query as `sub`. Now, each row from `main` will be compared against each row of `sub`. This way we refer to the current category value of the outer query. This is called a correlated subquery.

### The alternate approaches

I found following 2 alternatives on the Udemy forum.

```sql
-- Approach - 2.
-- This approach will return only one record per category in any circumstances.
-- I observed that this approach will fail when there are two products
-- having same price in a same product category.
SELECT DISTINCT ON(category) name, category, price 
FROM products 
ORDER BY category, price DESC;

-- Approach - 3.
-- This approach works as expected.
SELECT name, category, price 
FROM products
WHERE (price, category) IN (
	SELECT MAX(price), category
	FROM products
	GROUP BY category
);
```

## Conclusion

It is evident that correlated subquery is one of the best way to degrade your database server's performance. 😂.

I'm not an expert with SQL and databases. I'm sure there will be better ways to handle such scenarios. I will explore and document them in future on this space. 😊

## References

[Correlated subqueries](https://www.ibm.com/docs/en/informix-servers/12.10?topic=clauses-correlated-subqueries)

[Co-related Sub-queries](https://medium.com/analytics-vidhya/co-related-sub-queries-7d2c872d2341)
