# CMO Dashboard

- [About 'CMO Dashboard' template](#about-cmo-dashboard-template)
- [How to create Transformation from 'CMO Dashboard' template](#how-to-create-transformation-from-cmo-dashboard-template)
- [Variables list for the 'CMO Dashboard' template](#variables-list-for-the-cmo-dashboard-template)
- [Template result: data schema of the table for the CMO Dashboard](#template-result-data-schema-of-the-table-for-the-cmo-dashboard)
- [Changelog of the 'CMO Dashboard' template.](#changelog-of-the-cmo-dashboard-template)

## About 'CMO Dashboard' template

### Overview

This transformation uses the results of several previous transformations and aggregates data in one, flat and suitable for dashboard table.   
  

> **Note:**  
> For using this template you will need a customized [Sessionization - OWOX BI Events Streaming template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#about-merge-events-into-sessions-template), [Blended AdSpend + GA4 Cost Data Import template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend.md#about-blended-adspend--ga4-cost-data-import-template), [Costs Attribution template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/costs-attribution.md), and [Standard Attribution models template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/standard-attribution.md).  
>   

> **Important:**  
> For using the dashboard you will need to connect as source [this table](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/cmo-dashboard.md#template-result-data-schema-of-the-table-for-the-cmo-dashboard) **and** [attributionCheck table](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/standard-attribution/template-result-data-schemas-of-the-final-destination-tables.md), which is the result of the Standard Attribution Models transformation.

  
Below, you'll find a handy list of operations in the transformation template, each briefly described for your convenience. However, if you're eager to get started, feel free [to jump into the "How to start" article](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/cmo-dashboard.md#how-to-create-transformation-from-cmo-dashboard-template).

### D - Data Cleansing

The first operation in the template. It is responsible for the preliminary cleansing of data for the dashboard.  
  

> **Note:**  
> Letters at the beginning of the name of each operation define, in all, what this operation does:   
> D (DELETE) - operation with the main task of data deletion;   
> A (APPEND) - operation, that adds new data to the table.

### A - CMO Dashboard

This operation adds data into a [table](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/cmo-dashboard.md#template-result-data-schema-of-the-table-for-the-cmo-dashboard), which is acceptable for the dashboard. You can copy a [dashboard](https://lookerstudio.google.com/reporting/465211d2-1862-41dd-8a78-b3f5ea462b06/page/p_3qe1fmlb7c/edit) template and connect a table to it and get a perfect all-in-one dashboard for data analyzing, getting insights, and other marketing efforts:   
![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-cmo-dashboard/01/public)  
  
[How to add Google Big Query table as the Data Source in Looker Studio.](https://support.google.com/looker-studio/answer/6295968)   
🎉

## How to create Transformation from 'CMO Dashboard' template

In this article, you will find step-by-step instructions about how to create a Transformation from the 'CMO Dashboard' template.

> **Important:**  
> Please make sure you meet the [minimum requirements](https://github.com/OWOX/transformations-plugin/blob/main/docs/quick-start.md#introduction) with OWOX BI Transformation functionality.

### Step-by-step setup

**Step 1.** Go to the Workspace page and click the "New..." button in the top panel over the diagram. Choose the “New transformation” option in the popup menu.

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-cmo-dashboard/02/public)

**Step 2.** Now you will see the dialog with Templates gallery options. Choose the 'CMO Dashboard'  template from the list in the sidebar:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-cmo-dashboard/03/public)

**Step 3.** Click on the “Create & setup” button. And you will see your new Transformation:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-cmo-dashboard/04/public)

### How you can customize the template

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

Here you can add or remove variables ([list of variables](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/cmo-dashboard.md#variables-list-for-the-cmo-dashboard-template) for 'CMO Dashboard' template), [set up destinations](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#destination-settings), and [add triggers for autoruns](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab). Best of all, you can use these templates without any limits.

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
> We recommend using a time trigger for this transformation in 5 minutes and more, after the Merging Events into Sessions, Blended AdSpend, Cost Attribution, and Standard Attribution transformations end their job. Thus, you will get fresh data without any mistakes.

### Feedback and support

If you have any feedback or suggestions, please feel free to reach out to us via [bi@owox.com](mailto:bi@owox.com).

## Variables list for the 'CMO Dashboard' template

### Period

Specify the period for which you want to perform the transformation.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{start_suffix}}` | STRING | The start variable is responsible for the period's start date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery.<br>In other words, this is the beginning of the period during which the transformation needs to be performed.<br>We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer.<br>Additionally, instead of SQL code, you can specify a specific date in the date format here, for example, `CAST ('20230101' AS STRING)`. | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 3 DAY)) |
| `{{end_suffix}}` | STRING | The end variable is responsible for the period's end date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery. Thus, this transformation would take dates between start\_suffix and end\_suffix.<br>This is the end of the period during which the transformation needs to be performed. We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer. Additionally, instead of SQL code, you can specify an end date in the date format, for example, `` CAST ('20230101' AS STRING)`.` `` | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 1 DAY)) |

### Path to merging events results

Specify the path to the table with sessions. 

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{gcp_project_id}}` | STRING | ID of your project in Google Big Query, where the session table is located for which the 'CMO Dashboard' transformation is configured.<br>  | cute-gbq-project |
| `{{s_dataset_id}}` | STRING | The dataset ID where the session table is located for which the 'CMO Dashboard' transformation is configured. | OWOXBI\_GA4\_Streaming |
| `{{s_table_id}}` | STRING | The ID of the table with sessions.  | owoxbi\_ga4\_sessions |

### Additional parameters

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{c_event}}` | STRING | Conversion event. <br>For transactions, you must use the standard name purchase, for page views - name of event, like registration\_complete. | purchase **OR** registration\_complete |
| `{{c_url}}` | STRING | Conversion URL - allows you to set the URL where the conversion event occurs (by default it is set as the entire site). | %% - this value stands for the whole site.<br>%/conversion% - for the specified conversion page |
| `{{step_1}}` | STRING | Parameter, responsible for the add\_to\_cart event.  | add\_to\_cart |
| `{{step_2}}` | STRING | Parameter, responsible for the begin\_checkout event.  | begin\_checkout |

### Results

Specify the data, where the result of this transformation would be saved. This table would be used as a source for the dashboard template. 

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{r_dataset_id}}` | STRING | The ID of your dataset in Google Big Query, where the result of the 'CMO Dashboard' transformation would be saved. | OWOXBI\_Reports |
| `{{r_table_id}}` | STRING | ID of the CMO\_dashboard\_table. Has a standard value: CMO\_dashboard\_table | CMO\_dashboard\_table |

## Template result: data schema of the table for the CMO Dashboard

### Overview

This is a schema for the final table, that should be connected to the [dashboard](https://lookerstudio.google.com/reporting/465211d2-1862-41dd-8a78-b3f5ea462b06/page/p_3qe1fmlb7c/edit).   
  

### CMO\_dashboard\_table schema  
  

| Field name | Type | Description |
| --- | --- | --- |
| `date` | DATE | Session date. |
| `landingPage` | STRING | Page, from which the session had started.  |
| `clientId` | STRING | ID of the session. |
| `source` | STRING | Source of the session.  |
| `medium` | STRING | Medium of the session.  |
| `campaign` | STRING | Campaign of the session.  |
| `keyword` | STRING | Keyword of the session.  |
| `adContent` | STRING | AdContent of the session.  |
| `deviceCategory` | STRING | The type of the user's device:<br>\- tv;<br>\- game console;<br>\- robot;<br>\- set-top box;<br>\- robot mobile;<br>\- unknown;<br>\- hacker;<br>\- virtual reality;<br>\- anonymizer;<br>[Full list and definitions](https://github.com/OWOX/streaming-plugin/blob/main/docs/hit-based/how-data-is-collected.md#the-definitions-of-device-categories-in-the-owoxbisessions-tables) |
| `browser` | STRING | The browser used. |
| `browserVersion` | STRING | The version of the browser used. |
| `country` | STRING | The country from which the session originated. |
| `region` | STRING | The region from which the session originated. |
| `city` | STRING | The region from which the session originated. |
| `sessions` | INTEGER | Number of sessions in this source/medium. |
| `bounceSessions` | INTEGER | Number of sessions with only one interaction with your website (one pageview).  |
| `pageviews` | INTEGER | Number of pageviews in this source/medium. |
| `adImpressions` | FLOAT | Number of impressions. |
| `adClicks` | FLOAT | Number of clicks. |
| `adCost` | FLOAT | Number of advertisement costs. |
| `conversions` | INTEGER | Number of conversions. |
| `revenue` | FLOAT | Number of revenue.  |

## Changelog of the 'CMO Dashboard' template.

### October 03, 2023 - v.1.0.2

**Conversion Action Handling:** We've improved how we handle conversion actions submitted without webpage data (via MP). Now, these conversions are properly counted in our analytics.

**LinkedIn Detailed Operations:** In our A - LinkedIn Detailed operations, we've added the extraction of `campaign_name`. This ensures data accuracy, especially when `utm_campaign` is incomplete.

**Operational Transparency:** We've introduced comments for each operation to enhance visibility when reviewing transformation queries in Google BigQuery.

###   
July 28, 2023 - v.1.0.0

**Added fresh version of the template.**
