# Merge Events into Sessions (OWOX BI Web Streaming)

- [About 'Merge Events into Sessions' template](#about-merge-events-into-sessions-template)
- [How to create Transformation from a 'Merge Events into Sessions' template](#how-to-create-transformation-from-a-merge-events-into-sessions-template)
- [Variables list for transformation template 'Merge Events into Sessions'](#variables-list-for-transformation-template-merge-events-into-sessions)

## About 'Merge Events into Sessions' template

### Overview

A 'Merge Events into Sessions' template is used to create a session table, which is constructed using SQL queries (Operations). These Operations are provided in the template and are designed to be easily customizable by inserting the required variables. The actual SQL code of each Operation is automatically generated when the Transformation Template is set up in your OWOX BI Project.  
  
This template takes data from the 'events\_intraday\_' table of the [OWOX BI GA4 events-based web streaming](https://github.com/OWOX/streaming-plugin/tree/main/docs/ga4-events-based) and transforms it into sessions based on the logic that was used in the GA UA. 

> **Note:**  
> Letters at the beginning of the name of each operation define, in all, what this operation does:   
> D (DELETE) - operation with the main task of data deletion;   
> O (OVERWRITE) - operation, the result of which is overwriting of some table;   
> U (UPDATE) - operation, that updates some fields in some table or tables;   
> A (APPEND) - operation, that adds new data to the table.

Below, you'll find a handy list of operations in the transformation template, each briefly described for your convenience. However, if you're eager to get started, feel free [to jump into the "How to start" article](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#how-to-create-transformation-from-a-merge-events-into-sessions-template).  
  

### How does this template create a session from events? 

The algorithm of session creation is very similar to the [old Universal Analytics algorithm](https://support.google.com/analytics/answer/2731565?hl=en).   
Here are the main points of session creation: 

**First event in a day**: If an event occurs for the first time within the current day (time determined by the data view's time zone), it initiates the start of a new session.

**Interval between events exceeds 30 minutes**: If more than 30 minutes (or another specified time period) elapse between two consecutive events on the website, it is considered the end of the current session and the start of a new one.

**Change in click markup (gclid, dclid, fbclid, msclid)**: If there is a change in click markup, such as when transitioning from a Google Ads advertisement (gclid), Display Network (dclid), Facebook (fbclid), or Microsoft Advertising (msclid), it initiates a new session.

**Change in UTM markup (source, medium, campaign, keyword, adContent)**: If there is a change in UTM tags in the URL, such as source, medium, campaign, keyword, or adContent, it is also considered the start of a new session.

**Change in Referrer not included in the exclusion list**: If there is a change in the referral source (Referrer) that is not included in the referral exclusion list, it will be interpreted as the start of a new session.  
  

### O - Create sessions from events

During this stage, we perform the initial selection, transformation, and preparation of data from the \`events\_intraday\_\*\` table. Additionally, we prepare session parameters such as source, medium, campaign, session start, and session end.  
Also, session markup is being defined and other data converting is being made.   
  
At this step, bot-like users and user\_engagement events that may generate unnecessary sessions without being interactive are removed from the sessions data.

### O - Make aggregated data

#### O - Make aggregated data (initial)

At this stage, we prepare the dimensions of the trafficSource field, taking them from temporary table: trafficSource.source,trafficSource.medium,trafficSource.campaign and other.

**Important:** This step should be chosen, if this is **the** **first run** of transformation. 

#### O - Make aggregated data

At this stage, we select data from the temporary table `{{t1_table_id}}` and combine it with the data from the main table `{{s_table_id}}`. 

### U - Parse Gclids from dataTransfer

Autotagging priority contains two values. 0 — manual tagging is given priority when collecting session data. 1 — auto-tagging (gclid) is given priority when collecting session data. You must have the value of the variable `{{autotag_priority}}`set to 1.

  
If you are using **Data Transfer** files, at this stage, previously tagged sessions for paid traffic with source/medium "google/cpc" are edited. In this case, [the new Data Transfer tables that store information from Google Ads](https://github.com/OWOX/streaming-plugin/blob/main/docs/hit-based/web-tracking/setting-up-raw-data-collection-about-google-ads-campaigns-with-auto-tagging.md) would be used as source date. 

> **Note:**  
> We recommend running only one instance of Step 2 to optimize the use of credits. In this case, the first processing of gclid data will be performed correctly, and the second processing will not change anything.

#### Alternative: U - Parse Gclids from Google Ads by OWOX

This operation is disabled by default.  
When using Google Ads auto-tagging, you need to use additional data saved in the "gclid" field in events (check [our article on auto-tagging](https://github.com/OWOX/streaming-plugin/blob/main/docs/hit-based/faq.md#which-values-will-be-recorded-to-the-hit-and-session-data-tables-when-gclid-auto-tagging-and-manual-utm-tagging-data-overlap-in-google-ads) for more details).  
  
Autotagging priority contains two values. 0 — manual tagging is given priority when collecting session data. 1 — auto-tagging (gclid) is given priority when collecting session data. In this case, you must have the value of the variable `{{autotag_priority}}`set to 1. 

If you are using the **OWOX BI Google Ads** -> Google BigQuery pipeline, at this stage, previously tagged sessions for paid traffic with source/medium "google/cpc" are edited. In this case, the Google Ads -> Google BigQuery pipeline table is used as the source data.  
  

> **Note:**  
> We recommend running only one instance of Step 2 to optimize the use of credits. In this case, the first processing of gclid data will be performed correctly, and the second processing will not change anything.

### U - Update sessions by LNDC model

Reproducing the Last Non-Direct Click attribution model. Replacing the fields of the previously generated trafficSource object with the fields of the trafficSource object of the first session, counting from the current session, that does not contain (direct) / (none) values in its source/medium fields.

### D - Data cleansing

Clears all the data in the  table `{{s_table_id}}` for the defined period.

### A - Append final data

Transferring data from intermediate tables `{{t1_table_id}}`, `{{t2_table_id}}`to the final table `{{s_table_id}}`.  
  
After this operation, you will get a very convenient table with sessions, created from events, suitable for further analysis, reporting, and transformations. 🎉

## How to create Transformation from a 'Merge Events into Sessions' template

In this article, you will find step-by-step instructions about how to create a Transformation from the "Merge Events into Sessions" template.

> **Important:**  
> Please make sure you meet the [minimum requirements](https://github.com/OWOX/transformations-plugin/blob/main/docs/quick-start.md#introduction) with OWOX BI Transformation functionality.

### Step-by-step setup

**Step 1.** Go to the Workspace page and click the "New..." button in the top panel over the diagram or list. Choose the “New transformation” option in the popup menu.

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-merge-events-web-streaming/01/public)

**Step 2.** Now you will see the dialog with Templates gallery options. Choose the "Merge Events into Sessions" template from the list in the sidebar:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-merge-events-web-streaming/02/public)

**Step 3.** Click on the “Create & setup” button. And you will see your new Transformation:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-merge-events-web-streaming/03/public)

### How you can customize the template

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

When you create a Transformation from a template, you can customize the list of Operations and their order, edit the SQL code, add or remove variables ([list of variables for 'Merge Events into Sessions' template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#variables-list-for-transformation-template-merge-events-into-sessions)), [set up destinations](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#destination-settings), and [add triggers for autoruns](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab). Best of all, you can use these templates without any limits.

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

## Variables list for transformation template 'Merge Events into Sessions'

### Period

Specify the period for which you want to perform the transformation.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{start_suffix}}` | STRING | The start variable is responsible for the period's start date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery.<br>In other words, this is the beginning of the period during which the transformation needs to be performed.<br>We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer.<br>Additionally, instead of SQL code, you can specify a specific date in the date format here, for example, `CAST ('20230101' AS STRING)`. | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 3 DAY)) |
| `{{end_suffix}}` | STRING | The end variable is responsible for the period's end date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery. Thus, this transformation would take dates between start\_suffix and end\_suffix.<br>This is the end of the period during which the transformation needs to be performed. We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer. Additionally, instead of SQL code, you can specify an end date in the date format, for example, `` CAST ('20230101' AS STRING)`.` `` | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 1 DAY)) |

### OWOX GA4 streaming table

Specify the parameters of the OWOX GA4 streaming table. In the Table ID, specify the name before the underscore at the end, and without a suffix — calculated suffixes will be attached to this name in the future.

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{gcp_project_id}}` | STRING | The project ID where the events table is located for which the current transformation is configured. | cute-gbq-project |
| `{{ga4s_dataset_id}}` | STRING | The dataset ID where the events table is located for which the current transformation is configured. | OWOXBI\_GA4\_Streaming |
| `{{ga4s_table_id}}` | STRING | ID of your table with events. Has a standard value: events\_intraday\_ | events\_intraday\_ |

### Additional parameters

Specify additional parameters used for merging events into the sessions. 

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{s_timeout}}` | STRING | Session timeout is the duration after which one session is interrupted and the next begins. Specified in minutes.<br>The default session expiration time in Google Analytics is 30 minutes. However, you can specify any time depending on your website settings. | 30 |
| `{{c_timeout}}` | STRING | The waiting time for the campaign in days. When preparing the LNDC model, the specified number of days ago will be checked to determine the user's last indirect source. | 90 |
| `{{timezone}}` | STRING | Timezone in which sessions will be collected. Specified for:<br>-   Session interruption at midnight.
-   Correct determination of the time when the session was performed.
<br>[List of timezones](https://cloud.google.com/looker/docs/reference/param-view-timezone-values) | Europe/Kiev |
| `{{autotag_priority}}` | STRING | Autotagging priority. Contains two values. 0 - manual tagging is given priority when collecting session data. 1 - autotagging (gclid) is given priority when collecting session data.<br>More details about this parameter can be found [in our article on auto-tagging](https://github.com/OWOX/streaming-plugin/blob/main/docs/hit-based/faq.md#which-values-will-be-recorded-to-the-hit-and-session-data-tables-when-gclid-auto-tagging-and-manual-utm-tagging-data-overlap-in-google-ads). | 1 |
| `{{r_exclusion_list}}` | STRING | Referral exclusion list.A list of domains that, when transitioned from, will not start a new session and users will not be counted as referral traffic.<br><br>Please, notice, that at the end of the exclusion list must not be any symbols, such as "-", "|" etc.  | yourwebsite.com|<br>onemoreyourwebsite.com|<br>anothersite.com|verygoodsite.com |
| `{{pr_identity}}` | STRING | User ID of the website visitor. It can take one of two values:<br>-   user\_pseudo\_id — a [generated by GA4](https://support.google.com/firebase/answer/7029846?hl=en#zippy=%2Cuser) alias identifier intended for the user, such as an application instance identifier.
-   owox.user\_id — more details in our [article](https://github.com/OWOX/streaming-plugin/blob/main/docs/hit-based/how-data-is-collected.md#collecting-owox-user-id). | user\_pseudo\_id |
| `{{gclid_window}}` | STRING | This refers to how many days ago the operation searched for gclid in Data Transfer tables / By Request pipeline.<br><br>There are cases where a user clicks on an advertisement and saves the link. Then, after a few days, he revisit by the saved link. However, since the visit is technically through the link and not through the advertisement, the corresponding gclid is not present in dataTransfer, and it needs to be searched for in the history. | 7 |

### DataTransfer table

Specify the parameters of the DataTransfer table for parsing gclid. In the Table ID, specify the identifier present at the end of the names of all tables in the DataTransfer dataset.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{dt_dataset_id}}` | STRING | ID of dataset, in which Adwords Data Transfer data is collected.<br><br>This path is good for both new and old Data Transfer. In case of using Google Ads -> Google Big Query pipeline, the value should be a dataset where pipeline data is collected.  | AdwordsTransfer |

### Intermediate tables

Specify the names of the intermediate tables used for merging events into the sessions.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `t1_table_id` | STRING | Intermediate temporary table with event data. This table will be created automatically, choose a descriptive name to make sure the purpose of this table is clear in the future. | temporary\_events |
| `t2_table_id` | STRING | Intermediate temporary table with event data. This table will be created automatically, choose a descriptive name to make sure the purpose of this table is clear in the future. | temporary\_ga4\_sessions |

###    
Results of merging events

Specify where to save merging results.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{s_dataset_id}}` | STRING | The dataset ID where the session table is located for which the current transformation is configured.<br>Place, in which results of merging events would be saved. | OWOXBI\_GA4\_Streaming |
| `{{s_table_id}}` | STRING | The ID of the table with sessions. Place in which results of merging events would be saved. We recommend a standard value: owoxbi\_ga4\_sessions\_ | owoxbi\_ga4\_sessions |
