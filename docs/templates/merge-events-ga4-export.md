# Merge Events into Sessions (GA4 BigQuery Export)

- [About 'Merge Events into Sessions (GA4 BigQuery Export)' template](#about-merge-events-into-sessions-ga4-bigquery-export-template)
- [How to create Transformation from a 'Merge Events into Sessions (GA4 BigQuery Export)' template](#how-to-create-transformation-from-a-merge-events-into-sessions-ga4-bigquery-export-template)
- [Variables list for transformation template 'Merge Events into Sessions (GA4 BigQuery Export)'](#variables-list-for-transformation-template-merge-events-into-sessions-ga4-bigquery-export)
- [Changelog of the 'Merge Events into Sessions (GA4 BigQuery Export)' template.](#changelog-of-the-merge-events-into-sessions-ga4-bigquery-export-template)

## About 'Merge Events into Sessions (GA4 BigQuery Export)' template

### Overview

A 'Merge Events into Sessions (GA4 BigQuery Export)' template is used to create a session table, which is constructed using SQL queries (Operations). These Operations are provided in the template and are designed to be easily customizable by inserting the required variables. The actual SQL code of each Operation is automatically generated when the Transformation Template is set up in your OWOX BI Project.  
  
Data source of this template is the data, received using [BigQuery Export](https://support.google.com/analytics/answer/9358801?hl=en) feature of Google.    
  
This algorithm has little differences with [sessionization based on the OWOX BI webstream data](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md).  
Differences are next: 

-   Different data sources: for 'Merge Events into Sessions (GA4 BigQuery Export)' template it is the "events\_\*" table, and for OWOX BI webstream data it is the "events\_intraday\_\*" table. 
-   There is no gclid parsing in this template because Google gives already parsed data. 
-   Different source / medium parsing: Google could set referral as the event source in some cases, so it should be checked additionally.

> **Note:**  
> Letters at the beginning of the name of each operation define, in all, what this operation does:   
> D (DELETE) - operation with the main task of data deletion;   
> O (OVERWRITE) - operation, the result of which is overwriting of some table;   
> U (UPDATE) - operation, that updates some fields in some table or tables;   
> A (APPEND) - operation, that adds new data to the table.

Below, you'll find a handy list of operations in the transformation template, each briefly described for your convenience. However, if you're eager to get started, feel free [to jump into the "How to start" article](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-ga4-export.md#how-to-create-transformation-from-a-merge-events-into-sessions-ga4-bigquery-export-template).

### O - Create sessions from events

During this stage, we perform the initial selection, transformation, and preparation of data from the \`events\_\*\` table. Additionally, we prepare session parameters such as source, medium, campaign, session start, and session end.

### O - Make aggregated data

#### O - Make aggregated data (initial)

At this stage, we prepare the dimensions of the trafficSource field, taking them from temporary table: trafficSource.source,trafficSource.medium,trafficSource.campaign and other.

**Important:** This step should be chosen, if this is **the** **first run** of transformation. 

#### O - Make aggregated data

At this stage, we select data from the temporary table `{{t1_table_id}}` and combine it with the data from the main table `{{s_table_id}}`. 

### U - Update sessions by LNDC model

Reproducing the Last Non-Direct Click attribution model. Replacing the fields of the previously generated trafficSource object with the fields of the trafficSource object of the first session, counting from the current session, that does not contain (direct) / (none) values in its source/medium fields.

### D - Data cleansing

Clears all the data in the table `{{s_table_id}}`.

### A - Append final data

Transferring data from intermediate tables `{{t1_table_id}}`, `{{t2_table_id}}`to the final table `{{s_table_id}}`.  
  
After this operation, you will get a very convenient table with events, merged into sessions, suitable for further analysis, reporting, and transformations. 🎉

## How to create Transformation from a 'Merge Events into Sessions (GA4 BigQuery Export)' template

In this article, you will find step-by-step instructions about how to create a Transformation from the "Merge Events into Sessions (GA4 BigQuery Export)" template.

> **Important:**  
> Please make sure you meet the [minimum requirements](https://github.com/OWOX/transformations-plugin/blob/main/docs/quick-start.md#introduction) with OWOX BI Transformation functionality.

### Step-by-step setup

**Step 1.** Go to the Workspace page and click the "New..." button in the top panel over the diagram. Choose the “New transformation” option in the popup menu.

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-merge-events-ga4-export/01/public)

**Step 2.** Now you will see the dialog with Templates gallery options. Choose the "Merge Events into Sessions (GA4 BigQuery Export)" template from the list in the sidebar:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-merge-events-ga4-export/02/public)

**Step 3.** Click on the “Create & setup” button. And you will see your new Transformation:  
![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-merge-events-ga4-export/03/public)

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-merge-events-ga4-export/04/public)

### How you can customize the template

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

When you create a Transformation from a template, you can customize the list of Operations and their order, edit the SQL code, add or remove variables ([list of variables for 'Merge Events into Sessions (GA4 BigQuery Export)' template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-ga4-export.md#variables-list-for-transformation-template-merge-events-into-sessions-ga4-bigquery-export)), [set up destinations](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#destination-settings), and [add triggers for autoruns](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab). Best of all, you can use these templates without any limits.

The Transformations created from templates will also be displayed on the Workspace diagram, giving you a clear overview of your data transformation process.

### Run the Transformation and get analytics-ready data

Once you've finished debugging (all variables are set, list of Operations is actual), click on the “Run” button to start the sequential execution of the Operations. Check the status on the [“Run history” tab](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#run-history-tab).

After the successful run, go to your BigQuery account and check the table.

### Automate your data transformation process

Once you've finished debugging and you are sure the Transformation works correctly, you can set up a time trigger. With autoruns, you will get up-to-date data for your reports without headaches. Read more about autorun triggers in [this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab).

> **Important**  
> Please note: we recommend setting time triggers with a gap of five minutes or more for two different transformations, especially if they refer to the same table. This is because two simultaneous requests to the table can cause an error, resulting in the transformation not executing correctly.

### Feedback and support

If you have any feedback or suggestions, please feel free to reach out to us via [bi@owox.com](mailto:bi@owox.com).

## Variables list for transformation template 'Merge Events into Sessions (GA4 BigQuery Export)'

### Period

Specify the period for which you want to perform the transformation.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{start_suffix}}` | STRING | The start variable is responsible for the period's start date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery.<br>In other words, this is the beginning of the period during which the transformation needs to be performed.<br>We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer.<br>Additionally, instead of SQL code, you can specify a specific date in the date format here, for example, `CAST ('20230101' AS STRING)`. | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 3 DAY)) |
| `{{end_suffix}}` | STRING | The end variable is responsible for the period's end date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery. Thus, this transformation would take dates between start\_suffix and end\_suffix.<br>This is the end of the period during which the transformation needs to be performed. We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer. Additionally, instead of SQL code, you can specify an end date in the date format, for example, `` CAST ('20230101' AS STRING)`.` `` | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 1 DAY)) |

### GA4 BigQuery Export table

Specify the parameters of the GA4 events export table. In the Table ID, specify the name before the underscore at the end, and without a suffix — calculated suffixes will be attached to this name in the future.

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{gcp_project_id}}` | STRING | The project ID where the events table is located for which the current transformation is configured. | cute-gbq-project |
| `{{ga4e_dataset_id}}` | STRING | The dataset ID where the events table is located for which the current transformation is configured. | OWOXBI\_GA4\_Streaming |
| `{{ga4e_table_id}}` | STRING | ID of your table with events. Has a standard value: events\_ | events\_ |

### Additional parameters

Specify additional parameters used for merging events into sessions. 

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{s_timeout}}` | STRING | Session timeout is the duration after which one session is interrupted and the next begins. Specified in minutes.<br>The default session expiration time in Google Analytics is 30 minutes. However, you can specify any time depending on your website settings. | 30 |
| `{{c_timeout}}` | STRING | The waiting time for the campaign in days. When preparing the LNDC model, the specified number of days ago will be checked to determine the user's last indirect source. | 90 |
| `{{timezone}}` | STRING | Timezone in which sessions will be collected. Specified for:<br>-   Session interruption at midnight.
-   Correct determination of the time when the session was performed.
<br>[List of timezones](https://cloud.google.com/looker/docs/reference/param-view-timezone-values) | Europe/Kiev |
| `{{r_exclusion_list}}` | STRING | Referral exclusion list.A list of domains that, when transitioned from, will not start a new session and users will not be counted as referral traffic.<br><br>Please, notice, that at the end of the exclusion list must not be any symbols, such as "-", "|" etc.  | yourwebsite.com|<br>onemoreyourwebsite.com|<br>anothersite.com|verygoodsite.com |

### Intermediate tables

Specify the names of the intermediate tables used for merging.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `t1_table_id` | STRING | Intermediate temporary table with sessions data. This table will be created automatically, choose a descriptive name to make sure the purpose of this table is clear in the future. | temp\_ga4\_sessions |
| `t2_table_id` | STRING | Intermediate temporary table with aggregated data. This table will be created automatically, choose a descriptive name to make sure the purpose of this table is clear in the future. | temp\_agg\_sessions |

### Merging results

Specify where to save merged sessions.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{s_dataset_id}}` | STRING | The dataset ID where the session table is located for which the current transformation is configured.<br>Place, in which results of merging events would be saved. | OWOXBI\_GA4\_Streaming |
| `{{s_table_id}}` | STRING | The ID of the table with sessions. Place in which results of merging events would be saved. We recommend a standard value: export\_ga4\_sessions | export\_ga4\_sessions |

## Changelog of the 'Merge Events into Sessions (GA4 BigQuery Export)' template.

### November 01, 2024 - v.2.03

**Improved Session Handling for SPA and Multi-Tab Browsing**: Added logic to handle sessions where users enter via paid ads and stay on the site through SPA or multiple browser tabs. New organic sessions will not be created in such cases, keeping the session defining aligned with the initial traffic source.  
**Removal of session\_start as a Session-Break Trigger**: The session\_start event is no longer a condition for session breaks, preventing unnecessary breaks due to default GA4 timeouts.  
**Break Rule Analysis Field**: Introduced the `break_rule` field in session customDimensions to quickly identify session-creation criteria.  
**LNDC Date Tracking**: Added `lndc_date` in session customDimensions, indicating the date of LNDC model application to help define the appropriate lookback period.  
**Session Break Debugging Tool**: Included debug code for quick session break analysis, intended for internal use by OWOX teams.

### September 17, 2024 - v.2.02

**Product-Level Parsing**: Added customDimensions and customMetrics parsing for product-level data:  `hits.product.customDimensions.key` and `hits.product.customMetrics.key` added.  
**Session Duration**: Introduced the `timeOnSite` field to track session length in seconds.  
**Bounce Session Detection**: Added the `isBounceSession` field, which identifies whether a session was a bounce (1) or not (0) based on page views and interaction types.  
**Exclusion of Non-Consenting Users**: Automatic events from non-consenting users are now excluded from merging into sessions.  
**gclid Parsing Operations**: Added operations for gclid parsing via [DataTransfer](https://cloud.google.com/bigquery/docs/google-ads-transfer) or GoogleAds by OWOX, which are disabled by default.

### April 12, 2024 - v.2.01

**Added cleanup for the android-app source**: this source may occur for users transitioning from a mobile browser. Previously, it was assumed to always be google traffic, but there are cases where these are transitions with email campaign tags. After the recent updates, the source / medium for such transitions will be correctly identified (previously always set to google / cpc if campaign/keyword/adContent were present, or google / organic if no additional tags were present).

### April 01, 2024 - v.2.00

**Replicated logic**: we replicated the merging logic from the [Merge Events into Sessions](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md) template.

**New fields have been added**: we synchronized the data schema by adding trafficSource.fbclid, trafficSource.msclid, and platform fields.   
**New names:** we have renamed template and operations to more accurately reflect their functionality.

### December 12, 2023 - v.1.06

**A new field has beed added**: The new field was added to the result table schema - platform.   
This field by default filled with "WEB" values, if session was created by this template.

### November 14, 2023 - v.1.01

**Introduced a daily event count check for users**: Those surpassing 10,000 events in a day are excluded from the sessionization due to potential bot-like behavior.

**Adjusted the population of parameters hits.transaction.transactionId and hits.transaction.transactionRevenue**: If the transaction format is incorrectly passed (e.g., using INTEGER or FLOAT instead of STRING) and e-commerce is not filled, values are extracted from event\_params for the respective parameters.

### September 19, 2023 - v.1.00

**Added a fresh version of the template.**
