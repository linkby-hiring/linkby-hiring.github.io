# Full-Stack Developer Role 

## Overview
The following exercises are designed to help us better understand your technical skillset in determining fit for the Full-Stack Developer role.

**You will be allocated 4 hours to complete all exercises.**

You are not required to use all 4 hours and can submit anytime within the window. If you are unable to complete all the exercises within 4 hours, simply submit what you have completed.

Please follow the Submission Guidelines below to submit your work.


## Submission Guidelines
### Format
Your submissions will be hosted on a single GitHub repository. 
Please structure your submission according to the folder structure below:
```
/
	README.md
	submissions/
		1/
			index.js
		2/
			index.js
			package.json
		3/
			index.sql
		...etc
```

 - All completed exercises will reside in a root ***submissions/*** folder
 - Each submission will reside in a subfolder named according to the exercise number
 - For exercises where only 1 file is required, your answer will reside inside a single index file (e.g. *index.js*, *index.html* - depending on the requirements of the exercise)
 - For exercises where a full project is required, please include all relevant files (e.g. *package.json*, *.env*) so that the project can be simply run via `npm run install` and `npm run dev` (using a Node.js project as example)
 - Include a `README.md` file in the root folder that lists out:
	 - Your full name
	 - Your allocated time slot & date
	 - Any notes/explanations for your submissions (optional)

### Submission
Once you have set up the repository, please grant access to **andrewchak** on GitHub and send an email to [andrew@linkby.com](mailto:andrew@linkby.com) to notify us of your submission. Alternatively, you can simply make the repository public.


## Exercises

You are tasked with a total of **9** exercises.

We recommend **reading through all exercises before you begin your first one** so you can pace yourself within the allocated timeframe.

---

### Exercise 1

Below is an array with 4 items. Each item is assigned a distribution probability:
```js
const projects = [
	{ id: 1, name: 'Option 1', probability: 0.3 },
	{ id: 2, name: 'Option 2', probability: 0.5 },
	{ id: 3, name: 'Option 3', probability: 0.15 },
	{ id: 4, name: 'Option 4', probability: 0.05 }
]
```
#### Your Task

 - Write a function that takes the array as input, and outputs a random item from the array based on their assigned probability
 - Write a loop that repeats 500 times, where a random item is picked by running the function and outputs the ***name*** property of the item each time it is run
 - At the end of the loop, output a summary showing the total number of times that each item is run (e.g. `ID 1 = 150, ID 2 = 250 ...`)
 - You will be assessed on the function being as efficient as possible and using the least lines of code while maintaining accuracy
 - *Note:* As the function is meant to be random, we do not expect the final output to be in exact proportion to their distribution as we understand 500 is a small sample size and will have fluctuations on each run  

---

### Exercise 2

Below is a JavaScript data object:
```js
const items = {
	name: 'My Items',
	items: [
		{ id: 1, name: 'Item 1', score: 30 },
		{ id: 2, name: 'Item 2', score: 50 },
		{ id: 3, name: 'Item 3', score: 20 },
		{ id: 4, name: 'Item 4', score: 20 },
		{ id: 5, name: 'Item 5', score: 30 },
		{ id: 6, name: 'Item 6', score: 20 }
	]
}
```
#### Your Task

 - Write a single file Vue component (`index.vue` file) that takes the above data object as a component property, such that the component can be used in the following manner:
 
```html
<MyComponent :items="items" />
```
 
 to dynamically render the following HTML:
 
```html
<div id="items">
	<h1>My Items</h1>
	<div class="item">
		<h3>Items with Score 20</h3>
		<ul>
			<li>Item 6</li>
			<li>Item 4</li>
			<li>Item 3</li>
		</ul>
	</div>
	<div class="item">
		<h3>Items with Score 30</h3>
		<ul>
			<li>Item 5</li>
			<li>Item 1</li>
		</ul>
	</div>
	<div class="item">
		<h3>Items with Score 50</h3>
		<ul>
			<li class="only-one">Item 2</li>
		</ul>
	</div>
</div>
```
 
 - Items are grouped by `score` and then sorted in descending order by `name`
 - Where there is only one item within a score grouping, the `<li>` element should have the class `only-one`

---

### Exercise 3

Consider the two lines below:
```js
console.log(add(4,6));   // Outputs 10
console.log(add(4)(6));  // Outputs 10
```
#### Your Task

 - Write an `add()` method in Javascript which will work properly when invoked using either of the above syntax.

---

### Exercise 4

The Fibonacci sequence is a sequence of numbers where the next number is found by adding up the two numbers before it:
```js
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...
```
#### Your Task

 - Write a `getFibonaaci()` method in Javascript which takes `N` as input and returns the `Nth` Fibonacci number (eg. the first number `N=1` should return 0)

---

### Exercise 5

Consider the following code snippet:
```js
for (var i = 0; i < 5; i++) {
	setTimeout(function() { console.log(i); }, i * 1000 );
}
```
#### Your Task

 - Can you explain what is wrong with the code above? What can be done to rectify the problem? (include your code implementation in your submission)

---

### Exercise 6

Below are 3 PostgreSQL tables:
```sql
CREATE TABLE IF NOT EXISTS public.accounts
(
    id uuid NOT NULL,
    active boolean DEFAULT TRUE,
    name character varying(255) COLLATE pg_catalog."default",
    created_at timestamp with time zone,
    CONSTRAINT accounts_pkey PRIMARY KEY (id)
);

CREATE TABLE IF NOT EXISTS public.campaigns
(
    id uuid NOT NULL,
    account_id uuid NOT NULL,
    name character varying(255) COLLATE pg_catalog."default" NOT NULL DEFAULT ''::character varying,
    start_date timestamp with time zone NOT NULL,
    end_date timestamp with time zone NOT NULL,
    created_at timestamp with time zone,
    CONSTRAINT campaigns_pkey PRIMARY KEY (id),
    CONSTRAINT "campaigns_account_id_foreign_idx" FOREIGN KEY (account_id)
        REFERENCES public.accounts (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
);

CREATE TABLE IF NOT EXISTS public.clicks
(
    id uuid NOT NULL,
    campaign_id uuid NOT NULL,
    created_at timestamp with time zone,
    CONSTRAINT clicks_pkey PRIMARY KEY (id),
    CONSTRAINT "clicks_campaign_id_fkey" FOREIGN KEY (campaign_id)
        REFERENCES public.campaigns (id) MATCH SIMPLE
        ON UPDATE CASCADE
        ON DELETE CASCADE
);
```
 - An `account` has multiple `campaigns`
 - A `campaign` has multiple `clicks`
 - `created_at` is the timestamp of when the record is created for each table

#### Your Task

 - Write a single SQL query that gives a report on:
	 - the total number of clicks per account grouped by year + month
	 - only include active accounts that have had at least 1 campaign within the last 6 months (i.e. `created_at` of campaigns table is within the last 6 months)
	 - only include clicks from campaigns that have a duration of more than 1 week (duration is defined as the period between `start_date` and `end_date` of the campaigns table)
 - Your query output should have 4 columns:
	 - **account_id**
	 - **account_name**
	 - **month** (in the format `YYYY-MM`, e.g. `2021-08`)
	 - **num_clicks** (total number of clicks for that account within that month)
- Save your query in an `index.sql` file for submission

---

### Exercise 7

Based on the query from Exercise 6, what table index/indices will you set up to optimise the performance of the query?

#### Your Task

 - Write the SQL queries that will create the relevant index/indices

---

### Exercise 8

At Linkby, we are currently using the [Feathers](https://feathersjs.com/) framework for backend API services.

This exercise is designed to gauge your ability to work with the framework and navigate third party documentation.

#### Your Task

 - Create a Feathers API project from scratch (documentation [here](https://docs.feathersjs.com/))
 - Create a PostgreSQL database and create the 3 tables using the same table definitions from **Exercise 6**
 - Create 3 [services](https://docs.feathersjs.com/guides/basics/services.html) against the 3 tables using the [feathers-sequelize database adapter](https://docs.feathersjs.com/guides/basics/services.html#database-adapters), with PostgreSQL as the database engine. The service endpoints should be:
	 - */accounts*
	 - */campaigns*
	 - */clicks*
- Set up the following [hooks](https://docs.feathersjs.com/guides/basics/hooks.html) for the services below:
	- */accounts* - always apply `active = true` as a query condition to the `find` method
	- */campaigns* - throw a [Forbidden error](https://docs.feathersjs.com/api/errors.html#examples) for the `get` method when fetching the record for id `10`	
- Include all relevant files in your submission (you do not need to include any database files/exports, we will replicate a local copy of the database in our review process)
- You are free to introduce dummy data at your discretion if you feel it will aid in your completion for this exercise

---

### Exercise 9

Below is a boilerplate Javascript file that has `node-postgres` npm package installed and a data array:

```js
const { Client } = require('pg')
const client = new Client()
await client.connect()
 
const data = [
	{
		campaignId: 5550,
		views: 3,
		metadata: {
			overrideDate: "2022-12-13T17:51:54Z",
			incrementInteger: 4,
			ignoredDate: "2022-01-01T10:00:00Z"
		}
	},
	{
		campaignId: 5551,
		views: 23,
		metadata: {
			overrideDate: "2022-12-15T17:51:54Z",
			incrementInteger: 1,
			ignoredDate: "2022-02-01T10:00:00Z"
		}
	},
	{
		campaignId: 5552,
		views: 56,
		metadata: {
			overrideDate: "2022-12-1717:51:54Z",
			incrementInteger: 6,
			ignoredDate: "2022-03-01T10:00:00Z"
		}
	}
]

// Custom logic can be be inserted here

const sql = ?
await client.query(sql)
await client.end()
```

There is also a Postgres database table with the following definition:

```sql
CREATE TABLE IF NOT EXISTS public.campaign_stats
(
  	"campaignId" bigint NOT NULL,
  	views integer,
	metadata jsonb,
  	CONSTRAINT campaign_stats_pkey PRIMARY KEY ("campaignId")
)
```

#### Your Task

 - In the above boilerplate file you will see the line `const sql = ?`
 - You are asked to write a single SQL query to replace the `?` variable that will **upsert all records** from the data array into `public.campaign_stats` table, with the following conditions:
 	- If a row does not already exist for a given `campaignId`, insert the record exactly as per the payload in the data array
	- If a row already exists, `views` should be incremented to the existing value (eg. if say a row for `campaignId = 5550` already exists with `views = 6`, then `3` should be incremented to it so that the final result will have `views = 9`)
	- Likewise if a row already exists, `metadata` should be updated so that:
	  1. `overrideDate` gets overridden with the value from the data array
		2. `incrementInteger` gets incremented to the existing value within the JSON (similar in behaviour to `views`)
		3. `ignoredDate` gets ignored and does not override the existing value
  - For example, if an existing record for `campaignId = 5550` has `metadata` as:

	```json
	{
		"overrideDate": "2022-11-01T11:24:33Z",
		"incrementInteger": 35,
		"ignoredDate": "2021-12-01T10:00:00Z"
	}
	```
	then the final `metadata` value for that row should be:

	```json
	{
		"overrideDate": "2022-12-13T17:51:54Z",
		"incrementInteger": 39,
		"ignoredDate": "2021-12-01T10:00:00Z"
	}
	```

 - You are free to add any custom Javascript logic in the area commented `// Custom logic can be be inserted here` to help prepare variables for use in the SQL
 - It must be a single SQL that does the upsert, and cannot be multiple SQL queries run inside a loop that processes each record one by one within the data array

---

### Exercise 10

Consider an array of 100 promises, each printing its number to console after a random execution time between 100ms to 1s:

```js
const promises = [...Array(100).keys()].map(i => new Promise(resolve => setTimeout(resolve, Math.floor(Math.random() * 900) + 100)).then(_ => console.log(i)))
```

Traditionally if we execute all the promises via `Promise.all(promises)`, all promises will be processed concurrently immediately, and all 100 results will be printed to console after 1s.

#### Your Task

 - Write a function `runConcurrentPromises(promises, concurrency)` that takes in the list of `promises` as the first parameter and `concurrency` as the second parameter, where `concurrency` represents the maximum number of promises that can be executed concurrently at any given point in time
 - eg. `runConcurrentPromises(promises, 10)` should execute 10 promises concurrently immediately, and then as soon as the first one finishes, it takes in the next item sequentially in the array, and so on until all items in the array are executed
 - Please note the requirement is NOT to wait for the first 10 to complete execution and then execute the next 10 (this would be batching). It should work like an assembly line where the next item is processed as soon as one is completed (it is also not based on index within the array as each item is assigned a random execution time)
 - This function should work against arrays of any size (eg. if the array is increased to 1000 items) and still be able to process only 10 at a time (if `concurrency = 10`)


## Questions & Assistance

Should you have any questions or require assistance anytime during your allocated time slot, please email [andrew@linkby.com](mailto:andrew@linkby.com).
