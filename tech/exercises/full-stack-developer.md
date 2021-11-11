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
 - Create a PostgreSQL database and create the 3 tables using the same table definitions from **Exercise 3**
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

The final exercise is based on a real-life scenario that we currently undertake at Linkby.

Linkby offers a product called **Pubfeed** whereby we insert a Javascript widget onto a publisher's website that serves ad units in the form of native articles.

When a new publisher is interested in setting up Pubfeed for their website, usually they would like to get an idea of what the ad unit will look like on their website before they implement the integration.

Your task is to take one of the pages of their website and set up the Pubfeed code snippets so that we can provide a "demo site" to the publisher that showcases what Pubfeed will look like once deployed on their site.  

This exercise is designed to assess your HTML fundamentals, creativity, and attention to detail.

#### Your Task

 - Set up a demo site for the publisher *Timeout* by replicating this page of their website and setting up Pubfeed integration:
	[https://www.timeout.com/sydney/sport-and-fitness/the-best-online-workouts-you-can-do-at-home](https://www.timeout.com/sydney/sport-and-fitness/the-best-online-workouts-you-can-do-at-home)
 - There are 2 steps to setting up Pubfeed for a page:
1. Insert the following JavaScript snippet within the `<head>` of
    the website:
```html
<script>
  window.pubfeedSettings = {
      url: 'https://www.timeout.com/sydney/sport-and-fitness/the-best-online-workouts-you-can-do-at-home'
  }
</script>
<script src="https://staging-pubfeed.linkby.com/widget.js" async></script>
```
2. Insert the following HTML div within the `<body>` where the widget should show up:

```html
<div class="linkby-widget" data-type="listicle"></div>
```

For this particular page, the widget should show up at the end of the article - i.e. after the last paragraph of content for `28, App Store` and before the next section `Working hard, or hardly working?`.

- If the integration is set up properly, you should see a random Pubfeed article being loaded at the location of the snippet as such:

![Pubfeed on Timeout.com](/assets/pubfeed-timeout.jpg?raw=true)

- **You are not required to rebuild the page or code the HTML/CSS from scratch. It is recommended that you load and save the complete webpage as a starting point.**

- You will be assessed on how closely the look and feel of your replicated page matches the page on the publisher's live website (eg. fonts, colours, formatting, images, icons).

- Your submission will include a single `index.html` file that can be run on a web server, as well as any assets required for the page.

- If you do not already have a local web server to serve static HTML, we recommend you set up a [simple Node.js http server](https://www.npmjs.com/package/http-server) for this exercise and have a script that runs the server on `npm run dev` (you can include the JS files in the submission)


## Questions & Assistance

Should you have any questions or require assistance anytime during your allocated time slot, please email [andrew@linkby.com](mailto:andrew@linkby.com).