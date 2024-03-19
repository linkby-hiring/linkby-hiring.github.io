# Senior Full-Stack Developer Role 

## Overview
The following exercise is designed to help us better understand your technical skillset in determining fit for the Senior Full-Stack Developer role.

**You will be allocated 2 days to conduct this exercise.**

If you are unable to complete the exercises within 2 days, simply submit what you have completed.

Please follow the Submission Guidelines below to submit your work.


## Submission Guidelines

### Format
Your submissions will be hosted on a single GitHub repository. You can structure the project as you want.

From your project, we are expecting to see you considering

* SDLC (Software Development Lifecycle)
* Scalability of the service
* Coding best practices (e.g., unit testing, design pattern, etc)

### Submission
Once you have set up the repository, please grant access to **andrewchak** and **derik-linkby** on GitHub if it is a private repository. Or you can simply make the repository public, alternatively. Then please send an email to [andrew@linkby.com](mailto:andrew@linkby.com) to notify us of your submission.

## Exercise

You will create a small service that allows users to buy and sell their belongings online. The selling process is similar to auction but slightly different so multiple buyers can make an offer to the seller and vice versa. Here's the detailed negotiation process.

1. A user can publish a product they want to sell with the initial price and introductory images.
2. Other users can explore products published in the system. When they find a product want to buy, they can either directly purchase the product or make a counter-offer to the seller with a desired price.
3. When the seller gets the counter-offer from buyers, it will be shown on the product details UI. Sellers can either accept the counter-offer or make another counter-offer to each buyer.
4. Once a seller or a buyer accept the offer, a buyer can proceed checkout from product details UI.

### Product requirements

**Login UI**

1. In order to switch between sellers and buyers, you are expected to implement a simple Login UI.
1. This page consisted of the following elements:
	* Email address
	* Password
	* Login button

**Product List**

This will show all registered products in the system and consisted with the following elements:

1. List of the product card.
1. On top of the list, there are two buttons.
	* _Sell_ button
		* Upon click, navigate to register product UI
	* _Logout_ button
		* Upon click, the current user is logged out and returned to the login UI.
1. Each product card will show the following information:
	* The first introductory image uploaded (if exist)
	* Name of the product
	* Initial Price
	* Name of the seller
	* Status indicator
		* If the product is in `Reserved` or `Sold` status, show the status indicator on the bottom right of the product card.
1. To simplify, you don't need to worry about pagination on the list.

**Product Registration**

This UI allows a user to register a product to sell and consisted with the following elements:

1. Product Name
1. Price
1. Description
1. Product Images
	* A seller can upload up to 5 images per each product
1. _Submit_ button
	* Upon click, the product will be added to the system in `Available` status
1. _Cancel_ button
	* Upon click, navigate back to the product list UI.

**Product Details**

This UI will show the detailed information about the selected product and consisted of the following elements:

1. Name of the product
1. The status of product (`Available`, `Reserved`, `Sold`)
1. Initial Price
1. Description of the product
1. A list of introductory images
1. _Purchase_ button
	* This button only enabled when a viewer is a buyer and the price is initial price, or the seller accepted counter-offer that the a current buyer has sent.
	* If the seller accepted the counter-offer from a certain buyer, other buyers should not see this button.
	* Upon click, switch the product to `Sold` status and return to the product list UI.
	* This button is not visible when a product is in `Sold` status.
	* If the product is in `Reserved` status, only visible for the buyer who made an accepted counter-offer.
1. _Counter Offer_ button
	* This button only visible when
		* a viewer is a buyer and
		* there were no counter-offers made by the buyer or the seller made another counter-offer against to the buyer's counter-offer.
1. _Negotiation History_ section
	* This section only appear when a viewer is a seller.
	* When there's one or more counter-offers between the seller and buyers, show the history of negotiation process between multiple buyers.
	* On each history item consisted of the following elements:
		* Name of buyer
		* Price offered by a buyer
		* _Counter Offer_ button
			* This button only appear when
				* a user is a buyer and the price is the initial price or the seller made another counter-offer against the offer that the buyer made
				* a user is a seller and a buyer made a counter offer
			* A seller need to enter a new price to click this button.
			* Upon click, apply the new offered price to the product and return to the list UI
		* _Accept_ button
			* When the seller clicks this button, the product switched to _Reserved_ status.

#### Required tech stacks

You will build the RESTful API-based service that serves the SPA front-end client.

**Infrastructure**

1. Your service should be able to run both on developer's local machine and on AWS cloud.
1. Choice your best options for scalability.

**REST APIs**

1. Design and implement RESTful APIs in _TypeScript_ on Node.js.
1. Design your database on PostgreSQL.

**UI Client**

1. Design and implement SPA application with _Vue.js_ with _JavaScript_ or _TypeScript_.
1. You don't need to spend too much time to make the UI beautiful.
As long as it is working as intended, it is perfectly fine to use basic HTML elements.

## Questions & Assistance

Should you have any questions or require assistance anytime during your allocated time slot, please email [andrew@linkby.com](mailto:andrew@linkby.com).
