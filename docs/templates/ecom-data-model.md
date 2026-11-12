# Ecom Data Model

- [About 'Ecom Data Model' template](#about-ecom-data-model-template)
- [How to create Transformation from 'Ecom Data Model' template](#how-to-create-transformation-from-ecom-data-model-template)
- [Variables list for transformation template 'Ecom Data Model'](#variables-list-for-transformation-template-ecom-data-model)
- [Template result: data schema of final destination tables](#template-result-data-schema-of-final-destination-tables)
- [CRM data](#crm-data)
- [How to import data about transactions, email campaigns, and custom events to Google BigQuery](#how-to-import-data-about-transactions-email-campaigns-and-custom-events-to-google-bigquery)
- [Changelog of the 'Ecom Data Model' template.](#changelog-of-the-ecom-data-model-template)

## About 'Ecom Data Model' template

### Why data modeling?

-   **Structured Organization**: Data models enforce a clear structure, organizing data into tables, entities, and relationships. This helps in maintaining a well-defined schema where data is stored consistently and predictably.
    
-   **Integrated Data**: By consolidating data from various sources into a unified model, it ensures that all relevant information is available in one place. This integration is crucial for providing a comprehensive view of the data landscape.
    
-   **Consistency and Accuracy**: Strictly defined rules and relationships in a data model ensure that data remains consistent across different sources and uses. This reduces redundancy and errors, which are common in unstructured data collections.
    
-   **Single Source of Truth**: A data model centralizes data management, making it the authoritative source for all data-related queries and analyses. This eliminates discrepancies that arise from having multiple conflicting data sources.
    
-   **Ready-to-Use for Analysis**: Because data models predefine how data is stored, accessed, and related, they simplify the process of querying and analyzing data. Analysts and business users can rely on the model to provide accurate and relevant data quickly.
    
-   **Scalability and Maintenance**: Data models are designed to handle large volumes of data efficiently. As the amount of data grows, the model can be scaled without losing integrity or performance, making it sustainable over the long term.
    

### Overview

An 'Ecom Data Model' template is used to prepare the standard Ecommerce model for the CMO Dashboard with CRM Data (eCommerce).   
  
This transformation uses the data that is a result of  [Sessionization - OWOX BI Events Streaming template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md) and [BlendedAdSpend template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend.md) work. Additionally, it uses the CRM data, that [should be prepared in this structure](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/ecom-data-model.md#crm-data). The output is several tables: dictionaries and partitioned tables.

> **Note:**  
> Letters at the beginning of the name of each operation define, in all, what this operation does:   
> D (DELETE) - operation with the main task of data deletion;   
> O (OVERWRITE) - operation, the result of which is overwriting of some table;   
> A (APPEND) - operation, that adds new data to the table.  
> U (UPDATE) - operation, that updates data in the table. 

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-ecom-data-model/01/public)

Below, you'll find a handy list of operations in the transformation template, each briefly described for your convenience. However, if you're eager to get started, feel free [to jump into the "How to start" article](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/ecom-data-model.md#how-to-create-transformation-from-ecom-data-model-template).

### \[P\] - O - CRM from Client

> **Note:**  
> This operation is disabled by default. If you need CRM data in this transformation, please, contact your manager or support.

This is a custom operation for creating CRM table from another sources tables.  
You can insert here your custom SQL to make one CRM table from different tables in the needed structure or contact your manager or support. 

### \[P\] - O - CRM Standartization

> **Note:**  
> This operation is disabled by default. If you need CRM data in this transformation, please, contact your manager or support.

CRM Standartization for Data Model, overwrites the CRM data.

### \[P\] - O - Streaming Transactions

Deduplicated Streaming Transactions.

### \[P\] - D - Streaming Sessions

Precleansing of streamingSessions with refreshed date range.

### \[P\] - A - Streaming Sessions

Operation, that adds Streaming Sessions Info.

### \[P\] - D - CRM Transactions

> **Note:**  
> This operation is disabled by default. If you need CRM data in this transformation, please, contact your manager or support.

Precleansing of crmTransactions with refreshed date range.

### \[P\] - A - CRM Transactions

> **Note:**  
> This operation is disabled by default. If you need CRM data in this transformation, please, contact your manager or support.

CRM Matching with main data. 

### \[P\] - D - Session Libraries

Precleansing of sessionLibraries with refreshed date range.

### \[P\] - A - Session Libraries

Intermediate table with session-level libraries.

### \[P\] - D - Hits Libraries

Precleansing of hitsLibraries with refreshed date range.

### \[P\] - A - Hits Libraries

Creation of Hits Objects.

### \[P\] - D - Advertisement

Precleansing of advertisement with refreshed date range.

### \[P\] - A - Advertisement

Creation of the Advertisement Object.

### \[P\] - D - Sessions

Precleansing of sessions with refreshed date range.

### \[P\] - A - Sessions

Creation of the Sessions Object.

### \[R\] - O - User

Creation of the User Object.

### \[R\] - O - TrafficSource

Creation of the TrafficSource Object.

### \[R\] - O - Geo

Creation of the Geo Object.

### \[R\] - O - Device

Creation of the Device Object.

### \[P\] - D - Pageview

Precleansing of pageview with refreshed date range.

### \[P\] - A - Pageview

Creation of the Pageview Object.

### \[R\] - O - Page

Creation of the Page Object.

### \[P\] - D - Event

Precleansing of the event with refreshed date range.

### \[P\] - A - Event

Creation of the Event Object.

### \[R\] - O - EventInfo

Creation of the Event Object.

### \[P\] - D - Attribution

Precleansing of attribution with refreshed date range.

### \[P\] - A - Attribution

Creation of the Attribution Object.

### \[P\] - D - Transaction

Precleansing of transaction with refreshed date range.  
You've found a lucky clover:🍀, now your day would be great. 

### \[P\] - A - Transaction

Creation of the Transaction Object.

### \[P\] - D - EcommerceAction

Precleansing of ecommerceAction with refreshed date range.

### \[P\] - A - EcommerceAction

Creation of the EcommerceAction Object.

### \[P\] - D - ProductInAction

Precleansing of productInAction with refreshed date range.

### \[P\] - A - ProductInAction

Creation of the ProductInAction Object.

### \[P\] - D - ProductInTransaction

Precleansing of productInTransaction with refreshed date range.

### \[P\] - A - ProductInTransaction

Creation of the ProductInTransaction Object.

### \[R\] - O - Product

Creation of the Product Object.

### \[P\] - D - CostAttributionCheck

Precleansing of costAttributionCheck with refreshed date range.

### \[P\] - A - CostAttributionCheck

Creation of the Cost Attribution Check Object.

### \[P\] - U - Advertisement - Attribution Level

Updating a level field in Advertisement Object.

### \[P\] - U - User - Profiles

Profilization of users. 

### \[P\] - O - Sessions Attributes

Creation of the Sessions Attributes Object.

### \[R\] - O - FirstVisitorSession

Creation of the FirstVisitorSession Object.

### \[R\] - O - FirstCustomerSession

Creation of the FirstCustomerSession Object.

### \[P\] - D - Standard Attributions

Precleansing of standardAttributions with refreshed date range.

### \[P\] - A - Standard Attributions

This operation updates data in the next Attributions: First Click, Linear, Time Decay, Position Based.

### \[P\] - D - FBA Actions

Precleansing of attributionFunnelBasedActions with refreshed date range.

### \[P\] - A - FBA Actions

Calculations of FBA actions.

### \[P\] - D - FBA Probabilities

Precleansing of attributionFunnelBasedProbabilities with refreshed date range.

### \[P\] - A - FBA Probabilities

Calculations of FBA probabilities.

### \[P\] - D - FBA Values

Precleansing of attributionFunnelBasedValues with refreshed date range.

### \[P\] - A - FBA Values

Appending of the FBA values to the data in tables. 

### \[P\] - O - UnitedAttributions

Creation of the United Attributions object. 

### \[P\] - D - Transaction Check

Precleansing of transactionCheck with refreshed date range.

### \[P\] - A - Transaction Check

Checking transactions and creating Transaction Check object. 

### \[P\] - A - Attribution Check

Checking transactions and creating Attribution Check object. 

### \[P\] - D - Attribution Check

Precleansing of attributionCheck with refreshed date range.

### \[R\] - O - Profilization Check

Checking transactions and creating Profilization Check object. 

  
After this operation ends, you will get prepared Ecommerce Data Model! 🎉

## How to create Transformation from 'Ecom Data Model' template

In this article, you will find step-by-step instructions about how to create a Transformation from the 'Ecom Data Model' template.

> **Important:**  
> Please make sure you meet the [minimum requirements](https://github.com/OWOX/transformations-plugin/blob/main/docs/quick-start.md#introduction) with OWOX BI Transformation functionality.

### Step-by-step setup

**Step 1.** Go to the Workspace page and click the "New..." button in the top panel over the diagram. Choose the “New transformation” option in the popup menu.

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-ecom-data-model/02/public)

**Step 2.** Now you will see the dialog with Templates gallery options. Choose the 'Ecom Data Model'  template from the list in the sidebar:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-ecom-data-model/03/public)

**Step 3.** Click on the “Create & setup” button. And you will see your new Transformation:  
![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-ecom-data-model/04/public)

### How you can customize the template

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

Here you can add or remove variables ([list of variables](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/ecom-data-model.md#variables-list-for-transformation-template-ecom-data-model) for 'Ecom Data Model' template), [set up destinations](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#destination-settings), and [add triggers for autoruns](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab). Best of all, you can use these templates without any limits.

The Transformations created from templates will also be displayed on the Workspace diagram, giving you a clear overview of your data transformation process.  
  

> **Note:**  
> We do not recommend making changes in SQL-code or variables, because this may lead to incorrect or missing data in the final dashboard. But if you did change the template and something went wrong, you can always create a new template.

### Run the Transformation and get analytics-ready data

Once you've finished debugging (all variables are set), click on the “Run” button to start the sequential execution of the Operations. Check the status on the [“Run history” tab](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#run-history-tab).

After the successful run, go to your BigQuery account and check the table with sessions.

### Automate your data transformation process

Once you've finished debugging and you are sure the Transformation works correctly, you can set up a time trigger. With autoruns, you will get up-to-date data for your reports without headaches. Read more about autorun triggers in [this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab).

> **Important**  
> Please note: we recommend setting time triggers with a gap of five minutes or more for two different transformations, especially if they refer to the same table. This is because two simultaneous requests to the table can cause an error, resulting in the transformation not executing correctly.

> **Note:**  
> We recommend using a time trigger for this transformation in 5 minutes and more, after the Merge Events into Sessions, Blended AdSpend, Cost Attribution, and Standard Attribution transformations end their job. Thus, you will get fresh data without any mistakes.

### Feedback and support

If you have any feedback or suggestions, please feel free to reach out to us via [bi@owox.com](mailto:bi@owox.com).

## Variables list for transformation template 'Ecom Data Model'

### Period

Specify the period for which you want to perform the transformation.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{start_suffix}}` | STRING | The start variable is responsible for the period's start date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery.<br>In other words, this is the beginning of the period during which the transformation needs to be performed.<br>We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer.<br>Additionally, instead of SQL code, you can specify a specific date in the date format here, for example, `CAST ('20230101' AS STRING)`. | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 7 DAY)) |
| `{{end_suffix}}` | STRING | The end variable is responsible for the period's end date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery. Thus, this transformation would take dates between start\_suffix and end\_suffix.<br>This is the end of the period during which the transformation needs to be performed. We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer. Additionally, instead of SQL code, you can specify an end date in the date format, for example, `` CAST ('20230101' AS STRING)`.` `` | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 1 DAY)) |

### BlendedAdSpend Data

Specify the parameters of the OWOX Blended AdSpend table. 

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{gcp_project_id}}` | STRING | The ID of your project in Google Big Query, where the BlendedAdSpend table is stored. | cute-gbq-project |
| `{{ba_dataset_id}}` | STRING | The ID of your dataset in Google Big Query, where the BlendedAdSpend table is stored. | OWOXBI\_BlendedAdSpend |
| `{{ba_table_id}}` | STRING | ID of the BlendedAdSpend table. Has a standard value: BlendedAdSpend | BlendedAdSpend |

### Path to the merging events results

Specify the path to the table with sessions.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{s_dataset_id}}` | STRING | The dataset ID where the session table is located for which the current transformation is configured.<br>Place, in which results of cost, clicks and impressions attribution would be saved. | OWOXBI\_GA4\_Streaming |
| `{{s_table_id}}` | STRING | The ID of the table with sessions. Place in which results of cost, clicks and impressions attribution would be saved. | owoxbi\_ga4\_sessions |

### CRM Data settings

Specify the CRM Data settings. 

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{crm_table_id}}` | STRING | The id of a table, where the CRM data is located for which the current transformation is configured.<br>The variable is turned off by default and used only in case of using CRM data. | crmStandart |
| `{{completed_status}}` | STRING | The default value for fully completed transactions. <br><br>The variable is turned off by default and used only in case of using CRM data. | Completed |
| `{{update_online_identifiers}}` | STRING | Updating of online identifiers (clientId, userId etc.)<br><br>1 - default value. <br>The variable is turned off by default and used only in case of using CRM data. | **0** - do not update<br>**1** - update all <br>**2** - update if null |
| `{{data_priority}}` | STRING | What type of transactions should be considered as the main source? <br><br>1 - default value<br>The variable is turned off by default and used only in case of using CRM data. | **0** - CRM transactions over Streaming transactions<br>**1** - CRM transactions equally with Streaming transactions<br>**2** - Streaming transactions over CRM transactions |

### Project name

Please, specify the name of your OWOX BI project.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{project_name}}` | STRING | The indicative variable, adds the name of the project in every operation. More technical: code is added to every operation and it's easy to define transformation / project for CSM.  | OWOX **or** OnlineShop |

### Transformation settings

Please, add the needed settings to your transformation.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{conversion_window}}` | STRING | Conversion window in days, in which the transaction would be attributed to previous session.  | 30 |
| `{{attribution_exclusions}}` | STRING | Exclusion list for attribution, that gives the opportunity to ignore some values in the attribution model. Excludes sources from value attribution for standard attribution models. It works for both direct matches and inclusions.  | **google / cpc** - excludes all sessions with source/medium 'google / cpc'.<br>**/ .\*organic.\*** - excludes all sessions with medium including 'organic'.<br>**facebook / / .\*brand.\*** - excludes all sessions with source 'facebook', and 'campaign', containing 'brand'. |
| `{{move_value}}` | STRING |  A variable that takes a value of 1 or 0.<br>If set to 1, it transfers the value from the transaction to the previous non-excluded session, if such a session exists, and if the source/medium/campaign where the transaction occurred is in the exclusion list. <br>If set to 0, even if the source/medium/campaign where the transaction occurred is in the exclusion list, the session will receive part of the value.<br>  | 1 **or** 0 |
| `{{ir}}` | STRING | IR - initial run. <br>If it's a first run of transformation - you should use "#" symbol. If not - use the space " ".  | **#** - if first run. <br>  - for all subsequent runs.  |

### Path to the Transformations result

Specify the path to the place, where results of transformations would be saved.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{m_dataset_id}}` | STRING | The dataset ID where the model's data would be located, and for which the current transformation is configured. | OWOXBI\_DataModel |
| `{{transactions_table_id}}` | STRING | The table, where the transactions would be located.  | **streamingTransactions** - for just WEB transactions<br>**crmTransactions** - for WEB+CRM transactions |

## Template result: data schema of final destination tables

This transformation generates several tables, that would be used for [CMO Dashboard Model Based](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/cmo-dashboard-model-based.md) transformation.   
  
There is no reason to describe these tables fully, so we provide short descriptions of each table.   
  

### advertisement

The advertisement object.

### attribution

The attribution object.

### attributionCheck

The table with data about attribution checking.

### attributionFunnelBasedActions

The FBA actions object.

### attributionFunnelBasedProbabilities

The FBA probabilities object. 

### attributionFunnelBasedValues

The FBA values object. 

### costAttributionCheck

The cost attribution check object. 

### crm

The table with the data from the client's CRM.   
This table doesn't work from the box: in this table we aggregate data from different tables in one. As soon as we don't know the client's CRM structure, the code here should be written from scratch. 

### crmStandart

The table with the standardized data from the client's CRM.   
This table doesn't work from the box: in this table we collecting aggregated and standardized data. As soon as we don't know the client's CRM structure, the code here should be written according to client's CRM data structure. 

### crmTransactions

The table with matched data from CRM and Streaming.

### device

The object contains device information. 

### ecommerceAction

The e-commerce action object.

### event

The event object.

### eventInfo

The event information object.

### firstCustomerSession

The first customer's session object.

### firstVisitorSession

The first visitor's session object.

### geo

The geo dictionary contains information for decoding geographic data. 

### hitsLibraries

The hit object. 

### page

The page object. 

### pageview

The pageview object. 

### product

The product object.  

### productInAction

The product in action object.

### productInTransaction

The product in transaction object.

###   
profilizationCheck

Collected amount of data in the profile id table. 

### sessionLibraries

Intermediate table with the session-level libraries

### sessions

The sessions table represents a periodic structure partitioned by session date. It contains information about user sessions, enabling the analysis and assessment of user activities over different time periods.

### sessionsAttributes

The session attributes object. 

### standardAttributions

The table with data about updated attributions: First Click, Linear, Time Decay, Position Based

### streamingSessions

The table, which contains information about the sessions from the streaming. 

### trafficSource

The trafficSource reference provides decoding information about traffic sources. It helps determine where the traffic is coming from. 

### eventInfo

The eventInfo reference provides information for deciphering event-related data. This reference facilitates the understanding of event characteristics and details.

### transaction

The transactions table is periodic and partitioned by transaction date. It holds information about WEB and CRM transactions.

### transactionCheck

The table with data about transactions comparing between CRM and WEB transactions. 

### user

The user reference holds information for decoding user-related data.

## CRM data

Before [importing CRM data to Google BigQuery](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/ecom-data-model.md#how-to-import-data-about-transactions-email-campaigns-and-custom-events-to-google-bigquery), you need to create an empty table with a schema definition. More details on creating a table for CRM data storing can be found here.

From this article, you’ll learn about a schema definition, including the required fields, their types, and descriptions. While working with the CRM data schema below, please consider the following:

-   Fields marked with an asterisk mark (\*) are required to be filled in.
-   If you have no data for some schema fields, add them to the table with empty values.
-   Custom parameters of _User_ or _Transaction_ data can be added to the table via the additional fields. OWOX BI doesn’t process custom parameters when calculating an attribution model.
-   CRM data structure can be defined via notional nested levels. According to them, the same _transaction\_id_ can be used for several _product\_ids_, while _transaction\_revenue_ is always unique per _product\_id_.
-   Providing a [timezone](https://cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timezone_definitions) is required for the _TIMESTAMP_\-type fields (i.e. _transaction\_created, transaction\_changed, promo\_start, promo\_end_ fields).

Follow the references to see the examples of a [table](https://console.cloud.google.com/bigquery?p=owox-demo&d=Collections&t=crm_data&page=table) and [view](https://console.cloud.google.com/bigquery?p=owox-demo&d=Collections&t=CRM_view_demo&page=table) in Google BigQuery.

> **Note**  
> If at least one schema field is missing or has a type different from the required one, the calculation of an attribution model might return an error.  
>   
> To use CRM data in a structure that differs from the standard one, use the custom events mechanism. Read more

| Field | Data type | Description |
| --- | --- | --- |
| `**user_id**`\* | STRING | User ID<br>**Note:** By default, OWOX BI uses the `user_id` field to merge transaction data from CRM with data from other sources.<br>If the _User ID_ value is unknown for a certain transaction, leave _NULL_ in the `user_id` field for this transaction. In this case, OWOX BI will merge data using the `client_id` field. |
| `client_id` | STRING | Online visitor ID |
| `user_phone` | STRING | User phone number |
| `user_email` | STRING | User email address |
| `**transaction_id**`\* | STRING | Transaction ID |
| **`transaction_status`\*** | STRING | Transaction status: completed, refunded, canceled, pending, in\_process, awaiting\_fulfillment, awaiting\_shipment, or awaiting\_pickup.<br>**\***In an attribution model, only the transactions with the _completed_ status are taken into account. |
| `transaction_responsible` | STRING | ID of a manager or operator who processes the transaction |
| `transaction_coupon` | STRING | Promo code |
| `transaction_discount` | FLOAT | Discount in currency  |
| **`transaction_revenue`\*** | FLOAT | The total revenue from all the individual products purchased in this transaction, excluding discounts.<br>**Note:** If your data is detailed to the "product" level, then _transaction\_revenue_ must be unique per _product\_id_. To obtain the revenue for an individual product, use the formula: _product\_price\*product\_quantity_ |
| `transaction_currency` | STRING | Currency |
| `transaction_payment_type` | STRING | Payment method |
| `transaction_delivery_type` | STRING | Delivery method |
| `transaction_delivery_service` | STRING | Delivery service used |
| `transaction_delivery_time` | INTEGER | Delivery time in days |
| `transaction_touchpoint` | STRING | Transaction source. For example, a website, a call center, or an offline store |
| `transaction_store_id` | STRING | Store ID |
| `transaction_city` | STRING | City |
| `transaction_region` | STRING | Region |
| `transaction_country` | STRING | Country |
| **`transaction_created`\*** | TIMESTAMP | The time when the transaction was created<br>Providing a [timezone](https://cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timezone_definitions) is required for this field |
| `transaction_changed` | TIMESTAMP | The time of the last transaction update<br>Providing a [timezone](https://cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timezone_definitions) is required for this field |
| `product_id` | STRING | Product ID |
| `product_name` | STRING | Product name |
| `product_category` | STRING | Product category |
| `product_groupcategory1` | STRING | Level 1 category |
| `product_groupcategory2` | STRING | Level 2 category |
| `product_groupcategory3` | STRING | Level 3 category |
| `product_brand` | STRING | Product brand |
| `product_cogs` | FLOAT | Product COGS in the % of its price. For example, 0.4 or 0.15 |
| `product_quantity` | INTEGER | The number of products in the transaction |
| `product_price` | FLOAT | Product price |
| `promo_name` | STRING | Promotion name |
| `promo_start` | TIMESTAMP | Promotion start time<br>Providing a [timezone](https://cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timezone_definitions) is required for this field |
| `promo_end` | TIMESTAMP | Promotion end time<br>Providing a [timezone](https://cloud.google.com/bigquery/docs/reference/standard-sql/timestamp_functions#timezone_definitions) is required for this field |

## How to import data about transactions, email campaigns, and custom events to Google BigQuery

This article describes the ways you can use to import data from your CRM/ERP systems, mailing services, or other online or offline sources to Google BigQuery.

### Data import

To import data to Google BigQuery, use one of the following methods:

1.  Upload files in CSV or JSON format using [BigQuery UI](https://cloud.google.com/bigquery/docs/loading-data-local) or a [command line](https://cloud.google.com/bigquery/bq-command-line-tool)
2.  [SDK for .NET, .Java, PHP, Python](https://cloud.google.com/bigquery/client-libraries)
3.  [ETL applications](https://cloud.google.com/bigquery/third-party-tools#etl-tools-for-loading-data-into-bigquery)
4.  [ODBC driver from CDATA](http://www.cdata.com/drivers/bigquery/odbc/)
5.  Upload data from Google Sheets using the [OWOX BI BigQuery Reports](https://workspace.google.com/marketplace/app/owox_bi_bigquery_reports/263000453832) add-on

> **Consider the encoding and delimiters**  
> Google BigQuery supports the encodings UTF-8 (by default) and ISO-8859-1. The supported delimiters are comma (by default) and tab.  
> [More details in Google documentation](https://cloud.google.com/bigquery/docs/loading-data).

### The recommended table schema

For the correct data importing and its further analysis, make sure you follow the recommended structure of Google BigQuery table. Refer to our documentation on schema definition depending on your data type:

-   [CRM data](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/ecom-data-model.md#crm-data)
-   Email campaign data
-   Custom events data

### Uploading data via Google BigQuery web interface (using transaction data as an example)

We recommend uploading data via the BigQuery web UI. To do that, make up a CSV table with your data and upload it following the instructions below.

1.  Open [Google BigQuery web interface](https://bigquery.cloud.google.com/)
2.  **Create a new dataset** in your Google BigQuery project. Select the project in the **Resources** section, then click **Create dataset** in the window to the right:![Import\_transactions\_1.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-ecom-data-model/05/public)
3.  Specify the **Dataset ID** and **Data location**. Note: the data location must be the same as the location of all the other data you want to blend in OWOX BI.  
    Then, click **Create dataset**:**![Import\_transactions\_2.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-ecom-data-model/06/public)**
4.  **Create a new table**: Click the 'plus' icon on the right to the dataset name:![Import\_transactions\_3.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-ecom-data-model/07/public)
5.  Select **Create table from**: **Upload**, then specify the file location and format (**CSV**), then type in the name for the new table:![Import\_transactions\_4.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-ecom-data-model/08/public)
6.  Make up the data schema in the **Schema** section. You can add fields one by one by clicking **Add Field** and following [this data schema](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/ecom-data-model.md#crm-data), or simply click **Edit as Text** and paste the full schema in the JSON format (copy it from the snippet right after the screenshot below):![Import\_transactions\_5.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-ecom-data-model/09/public)

Copy the schema in JSON here:

\[ { "name": "user\_id", "type": "STRING", "mode": "REQUIRED" }, { "name": "client\_id", "type": "STRING", "mode": "NULLABLE" }, { "name": "user\_phone", "type": "STRING", "mode": "NULLABLE" }, { "name": "user\_email", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_id", "type": "STRING", "mode": "REQUIRED" }, { "name": "transaction\_status", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_responsible", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_coupon", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_discount", "type": "FLOAT", "mode": "NULLABLE" }, { "name": "transaction\_revenue", "type": "FLOAT", "mode": "NULLABLE" }, { "name": "transaction\_currency", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_payment\_type", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_delivery\_type", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_delivery\_service", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_delivery\_time", "type": "INTEGER", "mode": "NULLABLE" }, { "name": "transaction\_touchpoint", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_store\_id", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_city", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_region", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_country", "type": "STRING", "mode": "NULLABLE" }, { "name": "transaction\_created", "type": "TIMESTAMP", "mode": "NULLABLE" }, { "name": "transaction\_changed", "type": "TIMESTAMP", "mode": "NULLABLE" }, { "name": "product\_id", "type": "STRING", "mode": "REQUIRED" }, { "name": "product\_name", "type": "STRING", "mode": "NULLABLE" }, { "name": "product\_category", "type": "STRING", "mode": "NULLABLE" }, { "name": "product\_groupcategory1", "type": "STRING", "mode": "NULLABLE" }, { "name": "product\_groupcategory2", "type": "STRING", "mode": "NULLABLE" }, { "name": "product\_groupcategory3", "type": "STRING", "mode": "NULLABLE" }, { "name": "product\_brand", "type": "STRING", "mode": "NULLABLE" }, { "name": "product\_cogs", "type": "FLOAT", "mode": "NULLABLE" }, { "name": "product\_quantity", "type": "INTEGER", "mode": "REQUIRED" }, { "name": "product\_price", "type": "FLOAT", "mode": "REQUIRED" }, { "name": "promo\_name", "type": "STRING", "mode": "NULLABLE" }, { "name": "promo\_start", "type": "TIMESTAMP", "mode": "NULLABLE" }, { "name": "promo\_end", "type": "TIMESTAMP", "mode": "NULLABLE" } \]

7\. Set **Advanced options**. Set **Header rows to skip** as **1** so the data would be imported with no errors. You can also specify the allowed amount of errors to avoid errors when the table is created:![Import\_transactions\_6.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-ecom-data-model/10/public)

After clicking **Create** **Table**, the table will be uploaded to BigQuery:![Import\_transactions\_7.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-ecom-data-model/11/public)

## Changelog of the 'Ecom Data Model' template.

### July 16, 2024 - v.2.0.1

**Operation Adjustments**: Made adjustments to "\[P\] - O - CRM Standartization" and "\[P\] - O - Streaming Transactions".  
**Date Handling Update**: Added transactionDate to the attribution object and renamed session date from date to sessionDate. Both dates are now considered for preliminary cleaning.  
**FBA Attribution Correction**: Made adjustments in FBA attribution objects to ensure preliminary cleaning refers to the correct date range.

### May 30, 2024 - v.2.0.0

**Revised logic for intermediate and standard objects**: We have revised the logic for intermediate and standard objects.  
**Added profiling to the user object**: Profiling has been added to the user object based on the standard five identifiers: userId, phone, email, clientId, and owoxId  
**Integrated expense attribution within the model**: Expense allocation has been integrated within the model, allowing for understanding which expenses are allocated to sessions and which are not. This helps in future datamart construction to show unattributed expenses separately, ensuring accurate total expenses (not just those allocated to sessions).  
**Optimized collection of standard attribution models**: We have optimized the collection of standard attribution models within the model. You can now set a source / medium / campaign exclusion list in the [variables](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/ecom-data-model.md#variables-list-for-transformation-template-ecom-data-model), which excludes sources from value allocation for standard attribution models. It works for both direct matches and inclusions.  
Examples:  
`google / cpc` \- excludes all sessions with source/medium 'google / cpc'.  
`/ .*organic*.` \- excludes all sessions with medium including 'organic'.  
`facebook / / .*brand*.` \- excludes all sessions with source 'facebook', and 'campaign', containing 'brand'.  
Exclusion rules are listed with the "|" symbol.  
**Simultaneous calculation with and without excluded sources**: Standard attribution models now include simultaneous calculations with and without excluded sources. This allows for viewing the overall value brought by channels and how value is allocated to managed channels.  
**CRM data integration option**: We have added the option to use the model with or without CRM data. If using CRM data, you must first write custom code to standardize CRM data into a unified table.   
**Added FBA attribution calculation**: FBA attribution calculation has been added based on the standard funnel (visit - detail - add\_to\_cart - checkout - purchase).  
**Added validation operations**: We have added validation operations to check transaction matching, value allocation across different attribution models, and profiling of identifiers.

### August 17, 2023 - v.1.0.0

**A new template was added.**
