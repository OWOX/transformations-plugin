# CMO Dashboard Model Based

- [About 'CMO Dashboard Model Based' template](#about-cmo-dashboard-model-based-template)
- [How to create Transformation from 'CMO Dashboard Model Based' template](#how-to-create-transformation-from-cmo-dashboard-model-based-template)
- [Variables list for transformation template 'CMO Dashboard Model Based'](#variables-list-for-transformation-template-cmo-dashboard-model-based)
- [Template result: data schema of the final destination table](#template-result-data-schema-of-the-final-destination-table)

## About 'CMO Dashboard Model Based' template

This transformation works in conjunction with the [Ecom Data Model transformation](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/ecom-data-model.md),   
and receives input data from objects, that were prepared by that template.    
  
  

> **Note:**  
> If any objects are deactivated within the Ecommerce Data Model transformation, then the operation A - CMO Dashboard needs to be customized accordingly.

> **Note:**  
> Letters at the beginning of the name of each operation define, in all, what this operation does:   
> D (DELETE) - operation with the main task of data deletion;   
> A (APPEND) - operation, that adds new data to the table.

Below, you'll find a handy list of operations in the transformation template, each briefly described for your convenience. However, if you're eager to get started, feel free [to jump into the "How to start" article](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/cmo-dashboard-model-based.md#how-to-create-transformation-from-cmo-dashboard-model-based-template).

### D - Data Cleansing

This operation cleanses the table in selected in `{{start_suffix}}` - `{{end_suffix}}` period.

### A - CMO Dashboard

The operation, that creates datamart for the dashboard. In case some object would be excluded in 'Ecom Data Model' template, relevant objects should be commented on in this operation. 

### D - Data Cleansing LinkedIn

This operation cleanses the LinkedIn datamart table in selected in `{{start_suffix}}` - `{{end_suffix}}` period.  
Turned off by default. 

### A - LinkedIn detailed

This operation takes data for datamart directly from the LinkedIn advertisement cost data table.

  
After all operations finish their work, you can copy a [dashboard](https://lookerstudio.google.com/reporting/4383ac08-50ca-4356-b493-0f874376ac18) template and connect a table to it and get a perfect CMO dashboard with e-commerce for data analyzing, getting insights, and other marketing efforts.   
  
[How to add Google Big Query table as the Data Source in Looker Studio.](https://support.google.com/looker-studio/answer/6295968)

## How to create Transformation from 'CMO Dashboard Model Based' template

In this article, you will find step-by-step instructions about how to create a Transformation from the 'CMO Dashboard Model Based' template.

> **Important:**  
> Please make sure you meet the [minimum requirements](https://github.com/OWOX/transformations-plugin/blob/main/docs/quick-start.md#introduction) with OWOX BI Transformation functionality.

### Step-by-step setup

**Step 1.** Go to the Workspace page and click the "New..." button in the top panel over the diagram. Choose the “New transformation” option in the popup menu.

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-cmo-dashboard-model-based/01/public)

**Step 2.** Now you will see the dialog with Templates gallery options. Choose the 'CMO Dashboard Model Based'  template from the list in the sidebar:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-cmo-dashboard-model-based/02/public)

**Step 3.** Click on the “Create & setup” button. And you will see your new Transformation:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-cmo-dashboard-model-based/03/public)

### How you can customize the template

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

Here you can add or remove variables ([list of variables](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/cmo-dashboard.md#variables-list-for-the-cmo-dashboard-template) for 'CMO Dashboard with CRM Data (eCommerce)' template), [set up destinations](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#destination-settings), and [add triggers for autoruns](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab). Best of all, you can use these templates without any limits.

The Transformations created from templates will also be displayed on the Workspace diagram, giving you a clear overview of your data transformation process.  
  

> **Note:**  
> We do not recommend making changes in SQL-code or variables, because this may lead to incorrect or missing data in the final dashboard. But if you did change the template and something went wrong, you can always create a new template.

### Run the Transformation and get analytics-ready data

Once you've finished debugging (all variables are set), click on the “Run” button to start the sequential execution of the Operations. Check the status on the [“Run history” tab](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#run-history-tab).

After the successful run, go to your BigQuery account and check the dataset, that you've prepared earlier.

### Automate your data transformation process

Once you've finished debugging and you are sure the Transformation works correctly, you can set up a time trigger. With autoruns, you will get up-to-date data for your reports without headaches. Read more about autorun triggers in [this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab).

> **Important**  
> Please note: we recommend setting time triggers with a gap of five minutes or more for two different transformations, especially if they refer to the same table. This is because two simultaneous requests to the table can cause an error, resulting in the transformation not executing correctly.

> **Note:**  
> We recommend using a time trigger for this transformation in 5 minutes and more, after the Merge Events into Sessions, Blended AdSpend, Cost Attribution, Standard Attribution and Ecom Data Model transformations end their job. Thus, you will get fresh data without any mistakes.

### Feedback and support

If you have any feedback or suggestions, please feel free to reach out to us via [bi@owox.com](mailto:bi@owox.com).

## Variables list for transformation template 'CMO Dashboard Model Based'

### Period

Specify the period for which you want to perform the transformation.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{start_suffix}}` | STRING | The start variable is responsible for the period's start date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery.<br>In other words, this is the beginning of the period during which the transformation needs to be performed.<br>We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer.<br>Additionally, instead of SQL code, you can specify a specific date in the date format here, for example, `CAST ('20230101' AS STRING)`. | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 7 DAY)) |
| `{{end_suffix}}` | STRING | The end variable is responsible for the period's end date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery. Thus, this transformation would take dates between start\_suffix and end\_suffix.<br>This is the end of the period during which the transformation needs to be performed. We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer. Additionally, instead of SQL code, you can specify an end date in the date format, for example, `` CAST ('20230101' AS STRING)`.` `` | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 1 DAY)) |

### LinkedIn Data

Specify the parameters of the OWOX linkedin\_AdCostData table. 

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{gcp_project_id}}` | STRING | The ID of your project in Google Big Query, where the BlendedAdSpend table is stored. | cute-gbq-project |
| `{{l_dataset_id}}` | STRING | The ID of your dataset in Google Big Query, where the linkedin\_AdCostData table is stored. | BlendedAdSpend |
| `{{l_table_id}}` | STRING | ID of the LinkedIn table. Has a standard value: linkedin\_AdCostData | linkedin\_AdCostData |

### Path for Ecom Data Model template results

Specify the dataset, where the results of the Ecom Data Model template are stored.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{m_dataset_id}}` | STRING | The dataset ID where the Ecom Data Model template table is located for which the current transformation is configured. | OWOXBI\_DataModel |

### Path for saving results

Specify the path, where you want to save the result. 

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{r_dataset_id}}` | STRING | The dataset ID where the datamart table would be located. | OWOXBI\_Reports |
| `{{r_table_id}}` | STRING | The ID of the table in which results of current transformations would be saved, and which should be connected to the dashboard. | CMO\_dashboard\_model\_table |

### Special transaction event statuses

Please, specify statuses of the transaction events.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{s1_event}}` | STRING | The event, that shows start of the transaction.  | add\_to\_cart |
| `{{s2_event}}` | STRING | Second event before transaction. | begin\_checkout |
| `{{order_refunded}}` | STRING | Event, that shows, that transaction was completed.  | Refunded |

## Template result: data schema of the final destination table

### Overview

This is a schema for the final table, that should be connected to the [dashboard](https://lookerstudio.google.com/reporting/4383ac08-50ca-4356-b493-0f874376ac18).   
  
  

| Field name | Type | Description |
| --- | --- | --- |
| `date` | DATE | Session date. |
| `landingHost` | STRING | Host, from which the session had started.  |
| `landingPage` | STRING | Page, from which the session had started.  |
| `userId` | STRING | ID of user on website. |
| `userEmail` | STRING | The user's email. |
| `userPhone` | STRING | The user's phone. |
| `clientId` | STRING | ClientId anonymously identifies a particular user, device, or browser instance. |
| `customerId` | STRING | Customer ID from CRM. |
| `visitNumber` | INTEGER | The session number of this user over the last six months. If it is the first session, then this field is set to 1. |
| `source` | STRING | Source of the session.  |
| `medium` | STRING | Medium of the session.  |
| `campaign` | STRING | Campaign of the session.  |
| `keyword` | STRING | Keyword of the session.  |
| `adContent` | STRING | AdContent of the session.  |
| `adGroup` | STRING | AdGroup of the session.  |
| `channelGroup1` | STRING | First channel group. |
| `channelGroup2` | STRING | Second channel group. |
| `channelGroup3` | STRING | Third channel group. |
| `deviceCategory` | STRING | The type of the user's device:<br>\- tv;<br>\- game console;<br>\- robot;<br>\- set-top box;<br>\- robot mobile;<br>\- unknown;<br>\- hacker;<br>\- virtual reality;<br>\- anonymizer;<br>[Full list and definitions](https://github.com/OWOX/streaming-plugin/blob/main/docs/hit-based/how-data-is-collected.md#the-definitions-of-device-categories-in-the-owoxbisessions-tables) |
| `browser` | STRING | The browser used. |
| `browserVersion` | STRING | The version of the browser used. |
| `operatingSystem` | STRING | The operation system used. |
| `operatingSystemVersion` | STRING | The version of the operation system used. |
| `country` | STRING | The country from which the session originated. |
| `region` | STRING | The region from which the session originated. |
| `city` | STRING | The city from which the session originated. |
| `time` | FLOAT | The time from which the session started. |
| `sessions` | INTEGER | Number of sessions in this source/medium. |
| `bounceSessions` | INTEGER | Number of sessions with only one interaction with your website (one pageview).  |
| `pageviews` | INTEGER | Number of pageviews in this source/medium. |
| `adImpressions` | FLOAT | Number of impressions. |
| `adClicks` | FLOAT | Number of clicks. |
| `adCost` | FLOAT | Number of advertisement costs. |
| `step_1` | INTEGER | First step of the transaction. |
| `step_2` | INTEGER | Second step of the transaction.  |
| `conversions` | INTEGER | Number of conversions. |
| `revenue` | FLOAT | Number of revenue.  |
| `products` | INTEGER | Number of products.  |
| `conversions_crm` | INTEGER | Number of conversions from CRM.  |
| `revenue_crm` | FLOAT | Number of revenue from CRM.  |
| `products_crm` | INTEGER | Number of products from CRM.  |
| `conversions_refunded` | INTEGER | Number of refunded conversions.  |
| `revenue_refunded` | FLOAT | Number of refunded revenue.  |
| `products_refunded` | INTEGER | Number of refunded products.  |
