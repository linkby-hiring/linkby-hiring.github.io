# Senior Full-Stack Developer Role 

## Overview
The following exercise is designed to help us better understand your technical skillset in determining fit for the Senior Full-Stack Developer role.

## Submission Guidelines

### Format
Your submissions will be hosted on a single GitHub repository. You can structure the project in any way you want in terms of file/folder structure.

### Time
**You will be allocated 2 days to conduct this exercise.**

If you are unable to complete the exercise within 2 days, simply submit what you have completed. Submissions after your designated deadline will incur penalty to the assessment of your project, so it is important that you submit your work on time.

### Submission
Once you have set up the repository, please grant access to **andrewchak** and **derik-linkby** on GitHub if it is a private repository.
Alternatively, you can simply make the repository public and send us the URL. Then please send an email to [andrew@linkby.com](mailto:andrew@linkby.com) to notify us of your submission.

## The Exercise

You are asked to build a small web application that allows users to buy and sell their belongings online. The selling process involves an optional negotiation process where multiple buyers can make an offer to the seller against the same product, and the seller can also make counter-offers to each buyer. Here's how the process works:

1. A user can register a product they want to sell by entering basic product details, setting an initial price, and uploading images.
2. Other users can explore products registered in the application. When they find a product want to buy, they can either directly purchase the product or make a counter-offer to the seller with a desired price.
3. When the seller receives a counter-offer from a buyer, they can either accept the counter-offer or make another counter-offer back to the buyer. A history of all counter-offers will be shown to the seller on the Product Details UI (see more under *Product Requirements*). 
4. There can be an unlimited number of counter-offers back and forth between a buyer and the seller 
5. Once the seller or buyer accepts the offer, the buyer can proceed to purchase the product via Product Details UI.

### Application Requirements/Specifications

The web application will consist of 4 distinct UI:
* Login
* Product List
* Product Registration
* Product Details

You are free to structure URL routes in any way you want, as long as it satisfies the functional requirements.

**Login UI**

1. The application will begin with a login form that allows sellers and buyers to login. Note that a seller can also be a buyer, and a buyer can also be a seller, so there is no distinction between user types (ie. when a user registers a product, he/she will be the seller of that product, but can also act as a buyer against other seller's products).
2. The Login UI consists of the following elements:
	* Email address
	* Password
	* Login button
3. Given time constraints, there is no need to build a Register User UI - you can simply seed the database with test seller/buyer data for development purposes

**Product List UI**

Upon login, all users will land on this UI, which is a page that displays all registered products on the platform:

1. List of products displayed in a card format in a grid.
	* Upon clicking into a product card, navigate to the Product Details page for that product
2. Each product card will show the following information:
	* The first uploaded image (if exist)
	* Name of the product
	* Initial price
	* Name of the seller
	* Status indicator
		* If the product is in `Reserved` or `Sold` status, show the status indicator on the bottom right of the product card.
3. For simplicity, you don't need to worry about pagination for the list.
4. On top of the list as a header bar, there are two menu buttons.
	* _Sell_ button
		* Upon click, navigate to Product Registration page
	* _Logout_ button
		* Upon click, the current user is logged out and returns to the login UI.

**Product Registration**

This UI allows a user to register a product for selling and consists of a form with the following elements:

1. Product Name
2. Price
3. Description
4. Product Images
	* A seller can upload up to 5 images per each product, max size per upload is 5MB
5. _Submit_ button
	* Upon click, the product will be added to the system in `Available` status
6. _Cancel_ button
	* Upon click, navigate back to the Product List page.

**Product Details**

Upon clicking into an individual product, the Product Details UI will show information about the selected product, and consists of the following elements (static display of the product information as text/image is sufficient):

1. Name of the product
2. The status of product (`Available`, `Reserved`, `Sold`)
3. Initial Price
4. Description of the product
5. A list of uploaded images
6. _Purchase_ button
	* This button is only available &amp; enabled for buyers when either
		1. that buyer has not made any counter-offers, or
		2. that buyer has made a counter-offer and the seller has accepted it, or
		3. the seller has made another counter-offer to the buyer and the buyer has accepted it
	* If either party has accepted a counter-offer (ie. in `Reserved` status), other buyers will no longer see this button
	* Upon clicking the _Purchase_ button, set the product status to `Sold` and navigate back to the Product List UI.
	* This button is not visible when a product is in `Sold` status.
	* When a product is in `Reserved` status, this button is only visible for the buyer who originated the accepted counter-offer with the seller.
7. _Counter Offer_ button
	* This button is only visible when
		* The current logged in user is a buyer, and
		* The buyer has not yet made any counter-offers to the seller
8. _Negotiation History_ section
	* This section only appears when there has been at least one counter-offer by a buyer (appears for other buyers as well, so it's not just limited to the buyer who originated the counter-offer)
	* Show a timeline history of all counter-offers across all buyers in chronological order, including any counter-offers made by the seller to buyers (can be in table/list format)
	* Each timeline history item consists of the following:
		* Timestamp of the counter-offer
		* Name of the buyer
		* Whether the counter-offer was made by the buyer or the seller
		* Price offered (either by the buyer or seller)
		* Show a _Counter Offer_ button when either:
			* The current logged in user is the seller and counter-offer was made by a buyer, or
			* The current logged in user is the buyer, and the seller has made a counter-offer against an earlier counter-offer made by that buyer
			* When submitting a new counter-offer, the logged in user needs to enter a new price (both for buyers and sellers)
			* Upon click, log the new counter-offer into the timeline history and return to the Product List UI
		* Show an _Accept_ button when either:
			* The current logged in user is the seller and the counter-offer was made by a buyer, or
			* The current logged in user is the buyer, and the seller has made a counter-offer against an earlier counter-offer made by that buyer
			* Upon click, set the product status to `Reserved` and navigate back to the Product List UI

### Required Tech Stacks

You will be building a RESTful API backend service that serves a SPA frontend client.

**Infrastructure**

1. Your service should be able to run both on developer's local machine and on AWS cloud (eg. Docker)
2. Please consider your best options with scalability in mind.

**REST APIs**

1. Design and implement a RESTful APIs using _TypeScript_ on Node.js.
2. Design your database using PostgreSQL.
3. You are free to choose/use any framework to support your efforts (eg. Express, Hono).

**UI Client**

1. Design and implement a SPA application using _Vue.js_ with _JavaScript_ or _TypeScript_.
2. Given the limited timeframe, it is not a requirement to make the UI beautiful (it is more important to cover all required functionality)
3. You are free to choose/use an existing UI component library such as MaterialUI or Vuetify, but it is also perfectly fine to use vanilla JS/basic HTML elements.

**Assessment Criteria**

* You will be assessed across multiple facets of software engineering, including but not limited to:
	* Understanding of SDLC (Software Development Lifecycle)
	* Coding best practices (e.g., unit testing, design pattern, etc)
	* Scalability considerations / efficient database schema &amp; query designs
	* Ability to deliver and maintain quality under time pressure
* There is no right answer/right way of building the web application - your creativity, understanding of the problem, and how you approach solution design under time constraint is a large part of our assessment
* Additional effort/considerations for UX/design will be considered bonus (eg. look and feel, usability, form validation, notification message to users)
* If there is sufficient time, implementing a status filter (ie. `Available` / `Reserved` / `Sold`) against the Product List UI will be considered bonus

## Questions & Assistance

Should you have any questions or require assistance anytime during your allocated time slot, please email [andrew@linkby.com](mailto:andrew@linkby.com).
