# Data Analyst Role

## Overview
The following exercises covered some of our daily operations. They help us to understand your skillset in determining fit for the Data Analyst role.

**You will be allocated 4 hours to complete all exercises.**

You are not required to use all 4 hours and can submit anytime within the window. If you cannot complete all the exercises within 4 hours, simply submit what you have completed.

Please follow the Submission Guidelines below to submit your work.

## Submission Guidelines

You may submit the answer in the format you are familiar with. For example, you can submit an Excel file or share a Google Spreadsheet link.

If you used SQL, please include the SQL query that you used.

The following information should be included in your submission.

- Your name
- Question number
- Any notes/explanations for your submissions (optional)



## Background Information

- There are 2 major products in Linkby, the Core product and the Pubfeed product
- All the timestamps in the dataset are stored in UTC timezone
  - When generating a report, we use the Sydney timezone by default (AEST/GMT+10)
- In Linkby, we use AUD as the default currency. We convert all the currency amount to AUD for meaningful comparison. This exercise uses the following currency rate to simplify the calculation.
  - 1 USD = 1.34 AUD
  - 1 GBP = 1.86 AUD
  - 1 SGD = 1.08 AUD
  - 1 CAD = 1.12 AUD

## Datasets

You may download the dataset from the following link, or connect to our testing database.

- CSV data set
- PostgresSQL database connection

There are 6 tables in the datasets. The definition of these tables is listed below.

`accounts`

- This table contains the information of each company. A company can be either an advertiser or a publisher.
- The `type` column defines the account type
  - Advertiser: `type = 1`
  - Publisher: `type = 2`
- The `profile` column contains the account data, such as the country and timezone.

`publisher_brands`

- Each publisher account has at least one publisher brand. This table contains the information on each publisher brand
- The relationship between the `account` table and the `publisher_brands` table is:
  - An `account` has multiple `publisher_brands`

`campaigns`

- Only advertiser can create campaigns.
- An `account` has multiple `campaigns`
- This table contains the campaign information, such as the campaign name, campaign start date, campaign end date, status, currency, CPC, and a list of publisher brands the advertiser pitched to.
  - Campaign status can be definited by the value in `status` column
    - Draft campaign: `status = 0`
    - Campaign awaiting approval: `status = 1`
    - Active campaign: `status = 5`
    - Finished campaign: `status = 10`
  - The list of publisher brands that the advertiser pitched to is defined in the `directBrands` column.
    - There are multiple objects in the column.
    - The key of each object is the `publisher_brands`.`id`
    - The value of each object contains a list of date
      - "createdAt" means the date ofthe advertiser selected the publisher brands
      - "invitedAt" means the date ofthe advertisers sent an invitation to the publisher brands
      - "acceptedAt" means the date of the publisher brand accepted the campaign
      - "declinedAt" means the date of the publisher brand declined the campaign

`campaign_publishers`

- If a publisher brand accepts a campaign, the corresponding data will be stored in this table.
- A `campaign` has multiple `campaign_publishers`.
  - `campaign_publishers`.`campaignId` = `campaign`.`id`
- An `account` (publisher account only) has multiple `campaign_publishers`.
  - `campaign_publishers`.`publisherId` = `account`.`id`
- A 'publisher_brands' has multiple `campaign_publishers`
  - `campaign_publishers`.`brandId` = `publisher_brands`.`id`
- The `budget` column is the initial campaign budget assigned to a specific publisher_brands
- The `storyLinks` column contains all the URL of articles that the publisher submitted

`campaign_clicklogs`

- This table contains all the click records
- A `campaign` has multiple `campaign_clicklogs`
  - `campaign_clickllogs`.`campaignId` = `campaign`.`id`
- An `account` (publihser account only) has multiple `campaign_clicklogs`.
  - `campaign_clicklogs`.`publisherId` = `account`.`id`
- A 'publisher_brands' has multiple `campaign_clicklogs`
  - `campaign_clicklogs`.`brandId` = `publisher_brands`.`id`
- The `context` column contains the metadata of the click, including the date/time, browser information, IP addresses of the user, product type, referer information etc
  - The value `context->'ctx'->>'mode'` defines which product the click belongs to
    - Core product: `context->'ctx'->>'mode' = 'hash'`
    - Pubfeed product: `context->'ctx'->>'mode' = 'redir'`

`impressions`

- This table contains the daily impression of each publisher brand. Only Pubfeed product generates impression records.
- The column `type` defines the type of event
  - `pv` means the pageview of Pubfeed widget
  - `imp` means the impression of Pubfeed widget
- The column `count` shows the quantity of each event type


## Exercises

You are tasked with a total of **9** exercises.

We recommend **reading through all exercises before you begin your first one** so you can pace yourself within the allocated timeframe.

---

### Exercise 1

Get the campaign acceptance rate for all publisher accounts. The acceptance rate can be calculated by `(the number of campaigns accepted by a publisher / the number of campaigns pitched (invited) to a publisher)`.


### Exercise 2

Get the potential revenue for each publisher brand in Dec 2022.

Potential revenue means the total budget of all the campaigns pitched to a publisher brand.

Note: We use the Sydney timezone (AEST / GMT+10) to generate the report.


### Exercise 3

The programmatic click rate of campaign xxxx.

Programmatic clicks can be determined by repetitive signatures, such as the timestamp, user-agent and IP address.

### Exercise 4

The total revenue generated by advertisers from AU in Dec 2022.


### Exercise 5

The total revenue generated by the publisher accounts from AU in Dec 2022.


### Exercise 6

There was a discussion in the team about the performance of US publishers.

The management team assigned you to study it. You are asked to create a chart to show the funnel of conversion rates of all US Publishers to explain the situation.

Please create a chart for the funnel that can measure the publishers’ performance. You should include a brief description to explain each conversion rate and why you consider these conversion rates necessary.


### Exercise 7

Calculate all UK publisher accounts' average Pubfeed product click-through rate. Click-through rate can be calculated by `(total clicks / total impression)`.

### Exercise 8

Calculate the average RPMs of all UK publishers. RPMs mean revenue-per-impressions. It can be calculated by `(total revenue / total impressions ) * 1000`.


