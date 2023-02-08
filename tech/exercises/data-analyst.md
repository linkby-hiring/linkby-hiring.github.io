# Data Analyst Role

## Overview

The following exercises are designed to help us better understand your technical skillset in determining fit for the Data Analyst role.

**You will be allocated 3 hours to complete all exercises.**

You are not required to use all 3 hours and can submit anytime within the window. If you cannot complete all the exercises within 3 hours, simply submit what you have completed.

Please follow the Submission Guidelines below to submit your work.

## Submission Guidelines

You are required to make your submission via a single word document (this can be via Google Doc/Microsoft Word).

Please follow the format of [this template](https://docs.google.com/document/d/1CN_QNp2eXRafJHLTl1yZWLGIhvjUQi_XkrCLqpGWOXg/edit?usp=sharing).

We recommend that you make a copy of the file via **File > Make a Copy**, but you can also manually copy the format if you are using Microsoft Word.

Please also include the following information at the beginning of the submission:

- Your name
- Allocated date &amp; time slot
- Any notes/explanations for your submission (optional)

For questions that require you to work in Google Sheet/Microsoft Excel, please follow the steps below:
- Make a copy of the template Google Sheet/Microsoft Excel that we provide
- Complete the exercise and make relevant changes
- Share access to the new Google Sheet that you have created (for Excel, email it to us as an attachment)
- Include a link to that Google Sheet in the answer for that corresponding exercise number in your submission document

Then share access to your submission document to **andrew@linkby.com** (or email it to us if using Microsoft Word).

## Background Information

The exercises below are designed to simulate real-life scenarios that we have faced in Linkby.

Below are some background information to help set the context of the exercises:

- Linkby has developed two products for our users - 1. Core Platform, 2. Pubfeed
- All timestamp columns in the dataset are in **UTC timezone**
- For exercises requiring currency conversion, presume that **AUD** is the default currency, and use the following exchange rates for the purpose of conversion calculations:
  - 1 USD = 1.34 AUD
  - 1 GBP = 1.86 AUD
  - 1 SGD = 1.08 AUD
  - 1 CAD = 1.12 AUD

## Datasets

Below are the details to connect to the PostgreSQL database that have been set up for the purpose of this assessment:

- **Host:** linkby-hiring.ckjp7onx6q9c.ap-southeast-2.rds.amazonaws.com
- **Port:** 5432
- **Database:** linkby
- **User:** applicant
- **Password:** LinkbyHiring2023

There are 5 tables in the datasets. The definition of these tables are listed below.

`accounts`

- This table contains the information of each company account. An account can be either an **advertiser** or a **publisher**
- The `type` column defines the account type
  - Advertiser: `type = 1`
  - Publisher: `type = 2`
- The `profile` column is a JSON containing metadata for the account, such as the country and timezone
- `profile->'country'` indicates which market an account belongs to (eg. `profile->'country' = 'US'` means it is a United States account). This is in ISO alpha-2 code format

`publisher_brands`

- Each publisher account (ie. only those with `type = 2`) can have one or more publisher brands (eg. the publishing account **DailyMail** might run two separate websites **DailyMail.com** and **Metro.co.uk**, and we call these "publisher brands")
- This table contains records of individual publisher brands
- A publisher account can have multiple publisher brands - ie. `publisher_brands` belongs to `accounts` via the `publisherId` column, where `publisherId` represents the `id` column in `accounts`

`campaigns`

- This table contains campaigns that advertisers create and run on the Linkby platform, and contains campaign data such as campaign name, start date, end date, status
- Only advertiser accounts (ie. `accounts` with `type = 1`) can create campaigns
- `campaigns` belongs to `accounts` via the `accountId` column, where `accountId` represents the `id` column in `accounts`
- Each campaign can be in 1 of 4 possible statuses, as defined by the `status` column
  - **Draft:** `status = 0`
  - **Awaiting Approval:** `status = 1`
  - **Active:** `status = 5`
  - **Finished:** `status = 10`
- The `currency` column determines the currency that the campaign is denoted in, and is a proxy for which market a campaign belongs to:
  - `AUD` - Australia 
  - `USD` - United States
  - `GBP` - United Kingdom
  - `SGD` - Singapore
- A campaign can get "pitched" to one or more publisher brands - this means the advertiser wants to invite a publisher brand (eg. DailyMail.com, Metro.co.uk) to participate in their campaign and have the website write an article to promote them
- Publisher brands can either **accept** or **decline** a campaign that has been pitched to them
- The `budget` column represents the total amount of budget the advertiser has allocated to the entire campaign
- The `directBrands` JSON column represents the list of publisher brands to which a campaign has been pitched. Below is an example payload:
```json
{
    "112": {
      "name": "Harper's Bazaar (Listicle inclusion) (£2,500)",
      "createdAt": "2022-08-16T15:10:57Z",
      "invitedAt": "2022-08-16T16:10:57Z"
    },
    "227": {
      "name": "HuffPost UK (£2,500)",
      "createdAt": "2022-08-16T15:10:57Z",
      "invitedAt": "2022-08-16T17:10:57Z"
    }
}
```
- There can be one or multiple objects in the JSON payload
- The keys represent the `id` of the corresponding `publisher_brands` record (eg. in the above example, `112` and `227` are the `id` of `publisher_brands`)
- Each object can have one or more of the following date properties
  - `createdAt` - the date that this publisher brand association record is created
  - `invitedAt` - the date that an advertiser invites a publisher brand to participate in their campaign
  - `acceptedAt` - the date that the publisher brand accepted the campaign
  - `declinedAt` - the date that the publisher brand declined the campaign
- An empty value in `directBrands` represent that the advertiser has not yet selected any publisher brands to pitch to

`campaign_publishers`

- Every time a publisher brand accepts a campaign, a new record is created in this table to represent the relationship
- Any publisher brands that exist in the `directBrands` JSON in `campaigns` table with `acceptedAt` will appear as a new record here as well (conversely, the ones with only `createdAt`/`invitedAt`/`declinedAt` will not appear here)
- A campaign can have multiple accepted publisher brands
- Since publisher brands belong to a publisher account, a campaign will also be associated to one or more publisher accounts
- `campaigns_publishers` belongs to `campaigns` via the `campaignId` column, where `campaignId` represents the `id` column in `campaigns`
- `campaigns_publishers` belongs to `publisher_brands` via the `brandId` column, where `brandId` represents the `id` column in `publisher_brands`
- `campaigns_publishers` belongs to `accounts` via the `publisherId` column, where `publisherId` represents the `id` column in `accounts`
- The `budget` column represents the amount out of the total campaign budget that has been allocated to the accepted publisher brand
- The `storyLinks` column contains an array of URLs of articles that a publisher brand has published to promote the campaign. An empty value here indicates that the publisher has not yet published any articles.

`campaign_clicklogs`

- This table contains records of the clicks that Linkby tracks across articles published by publisher brands to promote campaigns
- `campaigns_clicklogs` belongs to `campaigns` via the `campaignId` column, where `campaignId` represents the `id` column in `campaigns`
- `campaigns_clicklogs` belongs to `publisher_brands` via the `brandId` column, where `brandId` represents the `id` column in `publisher_brands`
- `campaigns_clicklogs` belongs to `accounts` via the `publisherId` column, where `publisherId` represents the `id` column in `accounts`
- The `cpc` column represents the amount to be charged to the advertiser for that click
- The `currency` column determines the currency that the click is denoted in. This is combined with `cpc` to determine the amount charged to the advertiser for each click (eg. `currency = GBP` and `cpc = 2` will mean the click incurred `£2` to the advertiser, whereas `currency = USD` and `cpc = 2` will mean `USD $2`) 
- The `context` JSON column contains metadata that provides context around a click. The value `context->'ctx'->'mode'` defines which Linkby product the click is originated from:
  - Core Platform: `context->'ctx'->>'mode' = 'hash'`
  - Pubfeed: `context->'ctx'->>'mode' = 'redir'`


## Exercises

You are tasked with a total of **8** exercises.

We recommend **reading through all exercises before you begin your first one** so you can pace yourself within the allocated timeframe.

We also recommend that you view the data within each table before you begin so that you can familiarise yourself with the table structure and columns.

### Exercise 1

Write an SQL query to determine the campaign acceptance rate for all publisher brands.

The acceptance rate can be calculated by `(the number of campaigns accepted by a publisher brand / the number of campaigns pitched to a publisher brand)`.

The query should return 3 columns:
- brand_id (`id` of `publisher_brands`)
- name (`name` of `publisher_brands`)
- acceptance_rate (number between 0 and 1, where 1 represents 100% acceptance, formatted to 2 decimal places)

### Exercise 2

Write an SQL query to determine the median campaign budget by currency, for campaigns that have been accepted by publishers and have a start date between 1st Apr 2022 and 30 Jun 2022 (in AU time - ie. 1/4/2022 - 30/6/2022 inclusive, based in Australia/Sydney timezone).

The query should return 2 columns:
- currency
- median_budget (number formatted to 2 decimal places)

### Exercise 3

In this exercise, you are tasked with helping our customer support team analyse the click quality of a campaign for a new publisher who has recently signed up.

Given [this click log dataset file](https://docs.google.com/spreadsheets/d/1M-Nr0AbOhIxpJfuWEwM2C4zBUl2NIDcbJXFm0l_RR2c/edit?usp=sharing), you are asked to investigate into the clicks and decide if there is evidence/likelihood of programmatic clicks for the campaign.

Usually programmatic clicks can be identified based on characteristic across timestamp, user agent and IP address - for example, clicks that happen within 1sec of each other across the same user agent + IP address combination have a high chance to be programmatic.

Please make a copy of the above dataset file, and using pivot tables, briefly explain your approach and findings (make sure you share the file with us and include a link to your file in your answer).

### Exercise 4

Write an SQL query to determine the total number of active advertisers each month between Jan-Jun 2022 (in AU time).

An advertiser is considered active if they have either:
- Created an approved campaign (ie. not `Draft` or `Awaiting Approval`) in that month (based on `createdAt` of `campaigns` table)
- Has had at least 1 click incurred in that month

The query should return 2 columns:
- month
- active_advertisers (integer, 0 if none for that month)

### Exercise 5

Write an SQL query to determine the total revenue generated by each publisher account in US &amp; GB (note: **not** publisher brand) on Core Platform in Dec 2021 (AU time).

Total revenue is determined by the total `cpc` across all clicks that have been logged against that publisher account during Dec 2021.

Total revenue must be currency converted into AUD.

The query should return 3 columns:
- publisher_id
- publisher_name
- total_revenue (number formatted to 2 decimal places)

### Exercise 6

In this exercise, you have been asked by the management team to analyse the performance of our US publishers. They would like to compare the conversion funnel of US publishers against publishers from the other countries.

The conversion funnel for a Linkby publisher consists of the following steps: 
1. Being invited by an advertiser to a campaign
2. Accepting an advertiser campaign
3. Publish an article to promote the advertiser for the campaign

The total number of invitations can be determined by the existence of `invitedAt` timestamp in the `directBrands` column of the `campaigns` table.
The total number of accepted invitations can be determined by the existence of `acceptedAt` timestamp in the `directBrands` column of the `campaigns` table.
The total number of campaigns with at least one published article can be determined by the existence of `storyAt` timestamp in the `campaign_publishers` table.

Please calculate the following conversion rates:
- From "1. Being Invited" to "2. Invitation Accepted"
- From "2. Invitation Accepted" to "3. Article Published"

Using a Google Sheet/Excel file, create a chart that compares the funnel conversion rates of US publishers vs non-US publishers (you can determine if an account is from US based on `profile->'country'` of `accounts` table).

Please analyse the conversion rates and briefly explain your findings in the submission document, along with a link to your Google Sheet.

### Exercise 7

Consider the following [dataset file](https://docs.google.com/spreadsheets/d/1c4Z5mjy02XPURretDhAHQhzZ8vsRuXHv2N4vC3HlqyU/edit?usp=sharing).

There are two worksheets:
- `events` - this represents daily events captured for each publisher brand by our Pubfeed product. There are three types of events:
  - `imp` - Impressions
  - `pv` - Page Views
  - `expand` - Ad expansions
- `revenue` - this represents daily revenue generated for each publisher brand by Pubfeed product

Your task is to make a copy of the above dataset file, and create a new worksheet to calculate the average RPMs per month for all GB publishers.

RPMs represents **Revenue Per Thousand Impressions** and can be calculated by `(total revenue / total impressions ) * 1000`.

Each row should uniquely represent the average RPM of a publisher brand for a given month.

### Exercise 8

Imagine you are now part of the senior management team. List 3 reports/queries that you think will be of highest value to Linkby based on the understanding you have so far with regards to advertisers, publishers, campaigns &amp; clicks from this assessment (eg. Top 10 performing publishers across all markets). Include brief explanations of why you chose these 3.