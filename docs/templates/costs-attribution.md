# Costs Attribution on Sessions

- [About 'Costs Attribution' template](#about-costs-attribution-template)
- [How to create Transformation from a 'Costs Attribution' template](#how-to-create-transformation-from-a-costs-attribution-template)
- [Variables list for transformation template 'Cost Attribution'](#variables-list-for-transformation-template-cost-attribution)
- [Template result: data schema of the table for Data Mart](#template-result-data-schema-of-the-table-for-data-mart)
- [Calculation examples for the adCost and attributedAdCost fields](#calculation-examples-for-the-adcost-and-attributedadcost-fields)
- [Changelog of the 'Costs Attribution' template](#changelog-of-the-costs-attribution-template)

## About 'Costs Attribution' template

### Overview  
  

Previously, this template was a part of the Merge Events into Sessions template. But now it is a standalone template.  
  

> **Note:**  
> For using this template you will need customized [Merge Events into Sessions](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#about-merge-events-into-sessions-template) and [Blended AdSpend + GA4 Cost Data Import template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend.md#about-blended-adspend--ga4-cost-data-import-template). 

Below, you'll find a handy list of operations in the transformation template, each briefly described for your convenience. However, if you're eager to get started, feel free [to jump into the "How to start" article](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/costs-attribution.md#how-to-create-transformation-from-a-costs-attribution-template).

### U - GA4 Sessionization (costs)

The first operation in the template. It calculates the fields attributedAdCost, attributedAdClicks, and attributedAdImpressions with data from the BlendedAdSpend table `{{ba_table_id}}`. The data in the session table is linked to the costs, impressions, and clicks data, and each session receives a certain portion of the cost. More detailed information about the algorithm for filling in these fields can be found in [the article](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/costs-attribution.md#calculation-examples-for-the-adcost-and-attributedadcost-fields), using the example of the attributedAdCost field.  
  

> **Note:**  
> Letters at the beginning of the name of each operation define, in all, what this operation does:   
> D (DELETE) - operation with the main task of data deletion;   
> U (UPDATE) - operation, that updates some fields in some table or tables;   
> A (APPEND) - operation, that adds new data to the table.

### D - Data Cleansing

The operation that is responsible for the preliminary cleansing of data for the Data Mart.   
It is turned off by default. 

### A - Cost Attribution Check

This operation adds data into a [table](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/costs-attribution.md#template-result-data-schema-of-the-table-for-data-mart), that is acceptable for Data Mart. You can copy a [dashboard](https://lookerstudio.google.com/u/0/reporting/30984390-32e2-4663-a9b6-b31ee71bd8d6/page/p_6uscc06cqc/edit) and connect a table to it and see the distribution of costs for sessions. Allows you to understand the level of distribution of costs and whether there are problems with UTMs (for example, when there are costs for certain UTMs, but there are no sessions with such UTM).  
[How to add Google Big Query table as the Data Source in Looker Studio.](https://support.google.com/looker-studio/answer/6295968) 

This operation is turned off by default.

## How to create Transformation from a 'Costs Attribution' template

In this article, you will find step-by-step instructions about how to create a Transformation from the "Costs Attribution" template.

> **Important:**  
> Please make sure you meet the [minimum requirements](https://github.com/OWOX/transformations-plugin/blob/main/docs/quick-start.md#introduction) with OWOX BI Transformation functionality.

### Step-by-step setup

**Step 1.** Go to the Workspace page and click the "New..." button in the top panel over the diagram. Choose the “New transformation” option in the popup menu.

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-costs-attribution/01/public)

**Step 2.** Now you will see the dialog with Templates gallery options. Choose the "Costs Attribution" template from the list in the sidebar:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-costs-attribution/02/public)

**Step 3.** Click on the “Create & setup” button. And you will see your new Transformation:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-costs-attribution/03/public)

### How you can customize the template

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

When you create a Transformation from a template, you can customize the list of Operations and their order, edit the SQL code, add or remove variables ([list of variables for 'Costs Attribution' template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#variables-list-for-transformation-template-merge-events-into-sessions)), [set up destinations](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#destination-settings), and [add triggers for autoruns](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab). Best of all, you can use these templates without any limits.

The Transformations created from templates will also be displayed on the Workspace diagram, giving you a clear overview of your data transformation process.  
  

> **Note:**  
> We do not recommend making changes in this template, because this may lead to incorrect data in the sessions table. But if you did change the template and something went wrong, you can always create a new template.

### Run the Transformation and get analytics-ready data

Once you've finished debugging (all variables are set), click on the “Run” button to start the sequential execution of the Operations. Check the status on the [“Run history” tab](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#run-history-tab).

After the successful run, go to your BigQuery account and check the sessions table.

### Automate your data transformation process

Once you've finished debugging and you are sure the Transformation works correctly, you can set up a time trigger. With autoruns, you will get up-to-date data for your reports without headaches. Read more about autorun triggers in [this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab).

> **Important**  
> Please note: we recommend setting time triggers with a gap of five minutes or more for two different transformations, especially if they refer to the same table. This is because two simultaneous requests to the table can cause an error, resulting in the transformation not executing correctly.

> **Note:**  
> We recommend using a time trigger for this transformation in 5 minutes and more, after the Merge Events into Sessions and Blended AdSpend transformations end their job. Thus, you will get the freshest data about the cost of session(s).

### Feedback and support

If you have any feedback or suggestions, please feel free to reach out to us via [bi@owox.com](mailto:bi@owox.com).

## Variables list for transformation template 'Cost Attribution'

### Period

Specify the period for which you want to perform the transformation.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{start_suffix}}` | STRING | The start variable is responsible for the period's start date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery.<br>In other words, this is the beginning of the period during which the transformation needs to be performed.<br>We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer.<br>Additionally, instead of SQL code, you can specify a specific date in the date format here, for example, `CAST ('20230101' AS STRING)`. | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 7 DAY)) |
| `{{end_suffix}}` | STRING | The end variable is responsible for the period's end date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery. Thus, this transformation would take dates between start\_suffix and end\_suffix.<br>This is the end of the period during which the transformation needs to be performed. We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer. Additionally, instead of SQL code, you can specify an end date in the date format, for example, `` CAST ('20230101' AS STRING)`.` `` | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 1 DAY)) |

### BlendedAdSpend Data

Specify the parameters of the OWOX Blended AdSpend table. In the Table ID, specify the name before the underscore at the end and without a suffix - calculated suffixes will be attached to this name in the future.

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{gcp_project_id}}` | STRING | The ID of your project in Google Big Query, where the BlendedAdSpend table is stored. | cute-gbq-project |
| `{{ba_dataset_id}}` | STRING | The ID of your dataset in Google Big Query, where the BlendedAdSpend table is stored. | OWOXBI\_GA4\_Streaming |
| `{{ba_table_id}}` | STRING | ID of the BlendedAdSpend table. Has a standard value: BlendedAdSpend | BlendedAdSpend |

### Path to merging events results

Specify the path to the merging events table. 

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{s_dataset_id}}` | STRING | The dataset ID where the session table is located for which the current transformation is configured.<br>Place, in which results of cost, clicks and impressions attribution would be saved. | OWOXBI\_GA4\_Streaming |
| `{{s_table_id}}` | STRING | The ID of the table with sessions. Place in which results of cost, clicks and impressions attribution would be saved. | owoxbi\_ga4\_sessions |

## Template result: data schema of the table for Data Mart

### Overview

This is a schema for the final table, that can be used for Data Mart, it is perfect for seeing the distribution of costs for sessions.  
  

### CostAttributionCheck table  
  

| Field name | Type | Description |
| --- | --- | --- |
| `Date` | DATE | Session date. |
| `DataSource` | STRING | The data source of the visit. |
| `SessionID` | STRING | ID of the session. |
| `Sessions` | INTEGER | Amount of sessions in this source/medium.  |
| `Source` | STRING | Source of the session.  |
| `Medium` | STRING | Medium of the session.  |
| `Campaign` | STRING | Campaign of the session.  |
| `Keyword` | STRING | Keyword of the session.  |
| `AdContent` | STRING | AdContent of the session.  |
| `Impressions` | FLOAT | Amount of impressions. |
| `Clicks` | FLOAT | Amount of clicks. |
| `AdCost` | FLOAT | Amount of costs. |
| `CostM5` | FLOAT | Amount of attributed costs, where all five markups match.  |
| `CostM4` | FLOAT | Amount of attributed costs, where four markups match. |
| `CostM3` | FLOAT | Amount of attributed costs, where three markups match. |
| `CostM2` | FLOAT | Amount of attributed costs, where only two markups (source and medium) match. |
| `AttributedAdCost` | FLOAT | Amount of attributed ad cost to one session. |
| `AdGroup` | STRING | AdGroup of the session.  |
| `AdAccount` | STRING | Number of the account, from which data comes.  |
| `DataSourceCode` | STRING | Source, from which data originated. |
| `CampaignType` | STRING | Type of campaign, if specified.  |
| `CampaignId` | STRING | Id of the campaign, if specified.  |
| `CampaignName` | STRING | Name of campaign, if specified.  |
| `AdGroupId` | STRING | Id of advertisement group, if specified.  |
| `AdGroupName` | STRING | Name of advertisement group, if specified.  |
| `AdSource` | STRING | Source of advertisement.  |
| `PipelineId` | STRING | Id of the pipeline, from which data was taken.  |

## Calculation examples for the adCost and attributedAdCost fields

OWOX BI allows assessing the effectiveness of your ad channels based on the calculated session cost. The total session cost is attributed evenly between sessions according to the UTM tags 'source', 'medium', 'campaign', 'keyword', and 'content' and written to the field `attributedAdCost`.

### Calculation logic for the **attributedAdCost** field

When one or more tags are unknown, the cost is attributed evenly between the sessions according to the known tags and written to the `attributedAdCost` field.

**Processed cases:**

1.  No 'utm\_content' tag — costs are attributed accordingly to 'utm\_source', 'utm\_medium', 'utm\_campaign', 'utm\_term'.
2.  No 'utm\_term' and 'utm\_content' tags — costs are attributed accordingly to 'utm\_source', 'utm\_medium', 'utm\_campaign' and 'utm\_term'.
3.  Only the 'utm\_source' and 'utm\_medium' tags are known — costs are attributed accordingly to these known tags.

> **Note:**  
> To distribute the attributed ad cost to a session, the presence of the 'source' and 'medium' tags is required. If even one of these tags is absent, then costs won't be attributed.

### Examples

We know we've spent 100$ (`adCost` = 100) on sessions with the following tags:

-   'utm\_source' = `'google'`
-   'utm\_medium' = `'cpc'`
-   'utm\_campaign' = `'spring_sale'`
-   'utm\_term' = `'running+shoes'`
-   'utm\_content' = `'logolink'`

We also know had 5 sessions total with the same values of the tags 'utm\_source', 'utm\_medium', utm\_campaign', 'utm\_term', and 'utm\_content'.

Since all the tags perfectly match in all sessions, the field `adCost` will get the value calculated as 100$ / 5 sessions = 20$.

In this case, the costs are calculated for the `attributedAdCost` field in the same way:

| 'utm\_source' | 'utm\_medium' | 'utm\_campaign' | 'utm\_term' | 'utm\_content' | 'attributedAdCost' | 'adCost' |
| --- | --- | --- | --- | --- | --- | --- |
| `'google'` | `'cpc'` | `'spring_sale'` | `'running+shoes'` | `'logolink'` | `20` | `20` |

Another case: Google Analytics has cost data for 100$ _more_ with this set of tags:

-   'utm\_source' = `'google'`
-   'utm\_medium' = `'cpc'`
-   'utm\_campaign' = `**'sale'**`
-   'utm\_term' = `'running+shoes'`
-   'utm\_content' = `'logolink'`

However, Google Analytics didn't have data on sessions with this set of tags. In this case, the sum of 'google / cpc / sale' costs will be attributed to all 'google / cpc' sources as (100$ + 100$) / 5 sessions = 40$. But the value in the `adCost` field won't change, since this time we don't give a perfect match by tags:

|  'utm\_source' |  'utm\_medium' |  'utm\_campaign' |  'utm\_term' |  'utm\_content' |  'attributedAdCost' |  'adCost' |
| --- | --- | --- | --- | --- | --- | --- |
| `'google'` | `'cpc'` | `'spring_sale'` | `'running+shoes'` | `'logolink'` | `**40**` | `20` |

## Changelog of the 'Costs Attribution' template

### June 22, 2023 - v.1.0.1

**Default Streaming Dataset Update:** We've updated the default value of the variable `s_dataset_id` for streaming to the current and relevant 'OWOXBI\_GA4\_Streaming' dataset

### June 16, 2023 - v.1.0.0

**New template was added.**
