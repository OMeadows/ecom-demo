## Raw Data

### <u>Sellers</u>

<b>Table Description</b>: <br>This dataset includes data about the sellers that fulfilled orders made at Olist. Use it to find the seller location and to identify which seller fulfilled each product.

|Column Name|Description|
|:---|:---|
|`seller_id`|seller unique identifier|
|`seller_zip_code_prefix`|first 5 digits of seller zip code|
|`seller_city`|seller city name|
|`seller_state`|seller state|

### <u>Marketing Qualified Leads</u>

<b>Table Description</b>: <br>After a lead fills in a form at a landing page, a filter is made to select the ones that are qualified to sell their products at Olist. They are the Marketing Qualified Leads (MQLs).

|Column Name|Description|
|:---|:---|
|`mql_id`|marketing qualified lead id|
|`first_contact_date`|date of the first contact solicitation|
|`landing_page_id`|landing page id where the lead was acquired|
|`origin`|type of media where the lead was acquired|

#### <u>Product Category Name Translation</u>

<b>Table Description</b>: <br>Translates the product_category_name to english.

|Column Name|Description|
|:---|:---|
|`product_category_name`|category name in Portuguese|
|`product_category_name_english`|category name in English|

#### <u>Orders</u>

<b>Table Description</b>: <br>This is the core dataset. From each order you might find all other information.

|Column Name|Description|
|:---|:---|
|`order_id`|unique identifier of the order|
|`customer_id`|key to the customer dataset. Each order has a unique customer_id|
|`order_status`|reference to the order status (delivered, shipped, etc)|
|`order_purchase_timestamp`|shows the purchase timestamp|
|`order_approved_at`|shows the payment approval timestamp|
|`order_delivered_carrier_date`|shows the order posting timestamp. When it was handled to the logistic partner|
|`order_delivered_customer_date`|shows the actual order delivery date to the customer|
|`order_estimated_delivery_date`|shows the estimated delivery date that was informed to customer at the purchase moment|

#### <u>Order Items</u>

<b>Table Description</b>: <br>This dataset includes data about the items purchased within each order.

Example:
The order_id = 00143d0f86d6fbd9f9b38ab440ac16f5 has 3 items (same product). Each item has the freight calculated accordingly to its measures and weight. To get the total freight value for each order you just have to sum.

The total order_item value is: 21.33 * 3 = 63.99
The total freight value is: 15.10 * 3 = 45.30
The total order value (product + freight) is: 45.30 + 63.99 = 109.29

|Column Name|Description|
|:---|:---|
|`order_id`|order unique identifier|
|`order_item_id`|sequential number identifying number of items included in the same order|
|`product_id`|product unique identifier|
|`seller_id`|seller unique identifier|
|`shipping_limit_date`|shows the seller shipping limit date for handling the order over to the logistic partner|
|`price`|item price|
|`freight_value`|item freight value item (if an order has more than one item the freight value is splitted between items)|

#### <u>Customers</u>

<b>Table Description</b>: <br>This dataset has information about the customer and its location. Use it to identify unique customers in the orders dataset and to find the orders delivery location.

At our system each order is assigned to a unique customer_id. This means that the same customer will get different ids for different orders. The purpose of having a customer_unique_id on the dataset is to allow you to identify customers that made repurchases at the store. Otherwise you would find that each order had a different customer associated with.

|Column Name|Description|
|:---|:---|
|`customer_id`|key to the orders dataset. Each order has a unique customer_id|
|`customer_unique_id`|unique identifier of a customer|
|`customer_zip_code_prefix`|first five digits of customer zip code|
|`customer_city`|customer city name|
|`customer_state`|customer state|

#### <u>Geolocation</u>

<b>Table Description</b>: <br>This dataset has information Brazilian zip codes and its lat/lng coordinates. Use it to plot maps and find distances between sellers and customers.

|Column Name|Description|
|:---|:---|
|`geolocation_zip_code_prefix`|first 5 digits of zip code|
|`geolocation_lat`|latitude|
|`geolocation_lng`|longitude|
|`geolocation_city`|city name|
|`geolocation_state`|state|

#### <u>Order Payments</u>

<b>Table Description</b>: <br>This dataset includes data about the orders payment options.

|Column Name|Description|
|:---|:---|
|`order_id`|unique identifier of an order|
|`payment_sequential`|a customer may pay an order with more than one payment method. If he does so, a sequence will be created to accommodate all payments|
|`payment_type`|method of payment chosen by the customer|
|`payment_installments`|number of installments chosen by the customer|
|`payment_value`|transaction value|

#### <u>Closed Deals</u>

<b>Table Description</b>: <br>After a qualified lead fills in a form at a landing page he is contacted by a Sales Development Representative. At this step some information is checked and more information about the lead is gathered.

|Column Name|Description|
|:---|:---|
|`mql_id`|marketing qualified lead id|
|`seller_id`|seller id|
|`sdr_id`|sales development representative id|
|`sr_id`|sales representative|
|`won_date`|date the deal was closed|
|`business_segment`|lead business segment, informed on contact|
|`lead_type`|lead type, informed on contact|
|`lead_behaviour_profile`|lead behaviour profile, SDR identify it on contact|
|`has_company`|does the lead have a company (formal documentation)?|
|`has_gtin`|does the lead have Global Trade Item Number (barcode) for his products?|

#### <u>Order Reviews</u>

<b>Table Description</b>: <br>This dataset includes data about the reviews made by the customers.

After a customer purchases the product from Olist Store a seller gets notified to fulfill that order. Once the customer receives the product, or the estimated delivery date is due, the customer gets a satisfaction survey by email where he can give a note for the purchase experience and write down some comments.

|Column Name|Description|
|:---|:---|
|`review_id`|unique review identifier|
|`order_id`|unique order identifier|
|`review_score`|note ranging from 1 to 5 given by the customer on a satisfaction survey|
|`review_comment_title`|comment title from the review left by the customer, in Portuguese|
|`review_comment_message`|comment message from the review left by the customer, in Portuguese|
|`review_creation_date`|shows the date in which the satisfaction survey was sent to the customer|
|`review_answer_timestamp`|shows satisfaction survey answer timestamp|

#### <u>Products</u>

<b>Table Description</b>: <br>This dataset includes data about the products sold by Olist|

|Column Name|Description|
|:---|:---|
|`product_id`|unique product identifier|
|`product_category_name`|root category of product, in Portuguese|
|`product_name_lenght`|number of characters extracted from the product name|
|`product_description_lenght`|number of characters extracted from the product description|
|`product_photos_qty`|number of product published photos|
|`product_weight_g`|product weight measured in grams|
|`product_length_cm`|product length measured in centimeters|
|`product_height_cm`|product height measured in centimeters|
|`product_width_cm`|product width measured in centimeters|