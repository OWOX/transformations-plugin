# Blended AdSpend + GA4 Cost Data Import

- [About 'Blended AdSpend + GA4 Cost Data Import' template](#about-blended-adspend--ga4-cost-data-import-template)
- [How to create Transformation from a "Blended AdSpend" template](#how-to-create-transformation-from-a-blended-adspend-template)
- [Variables list for transformation template 'Blended Adspend + GA4 Cost Data Import'](#variables-list-for-transformation-template-blended-adspend--ga4-cost-data-import)
- [Template result: data schema of the final destination table](#template-result-data-schema-of-the-final-destination-table)
- [Changelog of the 'Blended AdSpend + GA4 Cost Data Import' template](#changelog-of-the-blended-adspend--ga4-cost-data-import-template)

## About 'Blended AdSpend + GA4 Cost Data Import' template

### Overview

A ‘Blended Adspend + GA4 Cost Data Import’ template creates a **BlendedAdSpend** table and a **GA4\_CostData\_Import** table. You’ll get all cost data in an automatically updated, unified, and user-friendly table without unnecessary fields.

This Transformation is available for:

-   OWOX BI fully-managed pipelines from Ad services (Facebook, Bing, Criteo, LinkedIn, Twitter) to Google BigQuery
-   Google Ads data from OWOX BI fully managed pipeline or [Data Transfer](https://github.com/OWOX/streaming-plugin/blob/main/docs/hit-based/web-tracking/setting-up-raw-data-collection-about-google-ads-campaigns-with-auto-tagging.md)
-   custom costs via [OWOX BI BigQuery Reports Extension](OWOX%20BI%20BigQuery%20Reports%20Extension).

All costs received as a result of Blended Adspend are exclusive of taxes. Learn more about taxes in Pipeline in this article.

### Getting started requirements

-   You created a unified dataset **OWOXBI\_BlendedAdSpend** as a destination for pipelines and custom data. [The link](https://www.owox.com/docs/storages/google-bigquery/) provides instructions about creating and sharing datasets with OWOX BI.  
    
    > **Note:**  
    > Otherwise, you must modify the default variables in the transformation template and replace the existing dataset variable names _OWOXBI\_BlendedAdSpend_ with the ones specific to your dataset.
    
-   You created Ad Services — Google BigQuery pipelines in the OWOX BI interface and already have tables with cost data from ad services in your **OWOXBI\_BlendedAdSpend** dataset. Follow these instructions to create fully-managed Ad Services — Google BigQuery pipelines.  

### Transformation process

The transformation process inputs the raw data stored in the OWOX BI pipelines’ tables. The output is a table **BlendedAdSpend** with cost data in the [following structure](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend.md#template-result-data-schema-of-the-final-destination-table) and a table **GA4\_CostData\_Import** which contains prepared data in a specific structure. 

Operations are provided in the template and are designed to be easily customizable by inserting the [required variables](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend.md#variables-list-for-transformation-template-blended-adspend--ga4-cost-data-import). The template has all the essential variables by default, so there is no need to enter all the values from the beginning:

![values.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend/01/public)

The actual SQL code of each Operation is automatically generated when the Transformation Template is set up in your OWOX BI Project.

> **Note:**  
> Letters at the beginning of the name of each operation define, in general, what this operation does:  
> D (DELETE) – an operation with the main task of data deletion;  
> O (OVERWRITE) – an operation the result of which is overwriting of some table;  
> U (UPDATE) – an operation that updates some fields in some table or tables;  
> A (APPEND) – an operation that adds new data to the table.

Below, you'll find a handy list of operations in the transformation template, each briefly described for your convenience. However, if you're eager to get started, feel free [to jump into the "How to start" article](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend.md#how-to-create-transformation-from-a-blended-adspend-template).

### D – Data cleansing

Initial stage – creates a new transformation from the ‘Blended Adspend + GA4 Cost Data Import’’ template in the OWOX BI interface. Then delete the previous `{{table_id_blended}}` table for dates between `{{start_suffix}}` and `{{end_suffix}}`, if it exists.

### A – Facebook

The operation selects data from the table **facebook\_AdCostData** generated in Google BigQuery after setting up Facebook → Google BigQuery pipeline. You can create this pipeline by following the provided instructions.

### A – Bing

The operation selects data from the table **bing\_OWOXAdCostData** generated in Google BigQuery after setting up Bing → Google BigQuery pipeline. You can create this pipeline by following the provided instructions.

### A – Criteo

The operation selects data from the table **criteo\_OWOXAdCostData** generated in Google BigQuery after setting up Criteo → Google BigQuery pipeline. You can create this pipeline by following the provided instructions.

### A – Twitter

The operation selects data from the table **twitter\_OWOXAdCostData** generated in Google BigQuery after setting up Twitter → Google BigQuery pipeline. You can create this pipeline by following the provided instructions.

### A – LinkedIn

The operation selects data from the table **linkedin\_AdCostData** generated in Google BigQuery after setting up LinkedIn → Google BigQuery pipeline. You can create this pipeline by following the provided instructions.  
  

### A – AdRoll

The operation selects data from the table **adroll\_OWOXAdCostData** generated in Google BigQuery after setting up AdRoll → Google BigQuery pipeline. You can create this pipeline by following the provided instructions.  
  

### A – Hotline

The operation selects data from the table **hotline\_OWOXAdCostData** generated in Google BigQuery after setting up Hotline → Google BigQuery pipeline. You can create this pipeline by following the provided instructions.  
  

### A – TikTok

The operation selects data from several tables, made by TikTok → Google BigQuery pipeline and generates a temporary **tiktok\_OWOXAdCostData** table. You can create this pipeline by following the provided instructions.

### A – GoogleAds by OWOX

The operation selects information from tables generated in Google BigQuery after setting the Google Ads → Google BigQuery pipeline. You can create this pipeline by following the provided instructions.

### A – GoogleAds DataTransfer

The operation selects data from tables generated in Google BigQuery after setting up automatic data transfer from Google Ads using BigQuery Data Transfer Service. It’s a native integration.

> **IMPORTANT:**  
> If you are planning to add this type of Google Ads export, please, set [the refresh window](https://cloud.google.com/bigquery/docs/google-ads-transfer#setup-data-transfer)(p. 8-e) with the same value, as the period of Blended AdSpend table refreshing. If there is a refresh window set to 7 days, it should be the same in DataTransfer, to avoid data discrepancies.   
> The default value of the refresh window is set to one(1) day.   
>   

Please, follow [our instructions to import Google Ads Data into Google BigQuery.](https://github.com/OWOX/streaming-plugin/blob/main/docs/hit-based/web-tracking/setting-up-raw-data-collection-about-google-ads-campaigns-with-auto-tagging.md)

> **IMPORTANT:**  
> You'll need to use only one operation of the above for Google Ads Data. If you have both sources from Google Ads, please, turn on 'Ignore for running'  for one of the operations to prevent duplicating the data in the output tables. You can pause or unpause the operation by following the steps in the pictures below: ![google\_ads\_data\_operations.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend/02/public) ![google\_ads\_data\_operations\_.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend/03/public)

### A – Custom

The operation selects data from the custom table generated in Google BigQuery. You can import your own cost data from Google Sheets to the Google BigQuery and use it in ‘Blended Adspend + GA4 Cost Data Import’ template. 

**Step 1.** You can find the Google Sheets template for manual adding costs [by the link](https://docs.google.com/spreadsheets/d/1QJR-cxV_2uPOOvYBkc_mMFzdfF8CqrRZ5ak7yrcVtMw/edit?usp=sharing). Please, copy the template to your Google Drive:

![manual\_costs.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend/04/public)

**Step 2.** Fill the values in the template with your cost data.

Please, note, that date ranges should be filled with date\_start and date\_end values: -   In rows 1-3 of the template, there is an example of filling in data by days.
-   In row 4 of the template, there is an example of filling in data for a month.
-   In row 5 of the template, there is an example of filling in data for 2 months.
-   In row 6 of the template, there is an example of filling in data for 1 week.

**Step 3.** Follow the [instructions](https://www.owox.com/docs/sources/google-sheets/) for using the Google Sheets document as a data source for the BigQuery table. 

**Step 4.** Change the variable `{{table_id_custom}}` in the 'Blended Adspend + GA4 Cost Data Import' transformation template to the table's name. For example, if the table has the name 'cute-gbq-project.OWOXBI\_BlendedAdSpend.custom\_data', specify 'custom\_data' in the variable:

![custom\_data.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend/05/public)

**Step 5**. Don't forget to enable operation **A** **— Custom** in the transformation:

![custom.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend/06/public)

If you have questions about importing custom data to Google BigQuery, you can contact us via email at [bi@owox.com](mailto:bi@owox.com).

### O – GA4 CostData Import

The operation prepares data for import to Google Analytics 4 and creates the table **GA4\_CostData\_Import**. Please, use this table during the setup of the Google BigQuery → Google Analytics 4 (via SFTP) pipeline if you want to import cost data to Google Analytics 4.  
Need help with this? Read Import non-Google costs into Google Analytics 4 solution.

> **IMPORTANT:**  
> Please, disable all unnecessary operations. You must select only operations for existing pipelines in your OWOX BI project. For example, if you have Facebook → Google BigQuery pipeline and LinkedIn → Google BigQuery pipeline, the first run of transformation must look like in the screenshot below: ![operations.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend/07/public)

After the last operation, you will get tables with data ready for further analysis and reporting 🎉

## How to create Transformation from a "Blended AdSpend" template

In this article, you will find step-by-step instructions about how to create a Transformation from the "Blended AdSpend" template.

> **Important:**  
> Please make sure you meet the [minimum requirements](https://github.com/OWOX/transformations-plugin/blob/main/docs/quick-start.md#introduction) with OWOX BI Transformation functionality.

[Watch the video](https://www.youtube.com/watch?v=tu7s4zW29CY)

### Step-by-step setup

**Step 1.** Go to the Workspace page and click the "New..." button in the top panel over the diagram. Choose the “New transformation” option in the popup menu.

![Frame\_2033.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend/08/public)

**Step 2.** Now you will see the dialog with Templates gallery options. Choose the "Blended AdSpend" template from the list in the sidebar:

![Frame\_2031.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend/09/public)

**Step 3.** Click on the “Create & setup” button. And you will see your new Transformation:

![Screenshot\_2023-03-20\_at\_18.41.55.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend/10/public)

### How you can customize the template

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

When you create a Transformation from a template, you can customize the list of Operations and their order, edit the SQL code, add or remove variables, [set up destinations](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#destination-settings), and [add triggers for autoruns](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab). Best of all, you can use these templates without any limits.

The Transformations created from templates will also be displayed on the Workspace diagram, giving you a clear overview of your data transformation process.

### Run the Transformation and get analytics-ready data

Once you've finished debugging (all variables are set, list of Operations is actual), click on the “Run” button to start the sequential execution of the Operations. Check the status on the [“Run history” tab](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#run-history-tab).

After the successful run, go to your BigQuery account and check the table with the [following data schema](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend.md#template-result-data-schema-of-the-final-destination-table).

### Automate your data transformation process

Once you've finished debugging and you are sure the Transformation works correctly, you can set up a time trigger. With autoruns, you will get up-to-date data for your reports without headaches. Read more about autorun triggers in [this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab).

> **Important**  
> Please note: we recommend setting time triggers with a gap of five minutes or more for two different transformations, especially if they refer to the same table. This is because two simultaneous requests to the table can cause an error, resulting in the transformation not executing correctly.

### Feedback and support

If you have any feedback or suggestions, please feel free to reach out to us via [bi@owox.com](mailto:bi@owox.com).

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

## Variables list for transformation template 'Blended Adspend + GA4 Cost Data Import'

> **Note:**  
> The template has all the essential variables by default, so there is no need to enter all the values from the beginning.

### Period

Specify the period for which you want to perform the transformation.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{start_suffix}}` | STRING | The start variable is responsible for the period's start date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery.<br>In other words, this is the beginning of the period during which the transformation needs to be performed.<br>We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer.<br>Additionally, instead of SQL code, you can specify a specific date in the date format here, for example, `CAST ('20230101' AS STRING)`. | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 1 DAY)) |
| `{{end_suffix}}` | STRING | The end variable is responsible for the period's end date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery. Thus, this transformation would take dates between start\_suffix and end\_suffix.<br>This is the end of the period during which the transformation needs to be performed. We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer. Additionally, instead of SQL code, you can specify an end date in the date format, for example, `` CAST ('20230101' AS STRING)`.` `` | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 1 DAY)) |

### Ads Data Pipelines

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

Specify the project, dataset, and table where data from pipelines from ad services to Google BigQuery is located.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{gcp_project_id}}` | STRING | The project ID where the data tables are located for which the current transformation is configured. | cute-gbq-project |
| `{{dataset_id_fb}}` | STRING | The dataset ID where Facebook data is located. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_fb}}` | STRING | The table ID where Facebook data is located. It is constant value for OWOX BI Facebook → Google BigQuery pipeline: facebook\_AdCostData | facebook\_AdCostData |
| `{{dataset_id_criteo}}` | STRING | The dataset ID where Criteo data is located. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_criteo}}` | STRING | The table ID where Criteo data is located. It is constant value for OWOX BI Criteo → Google BigQuery pipeline: criteo\_OWOXAdCostData | criteo\_OWOXAdCostData |
| `{{dataset_id_bing}}` | STRING | The dataset ID where Bing data is located. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_bing}}` | STRING | The table ID where Bing data is located. It is constant value for OWOX BI Bing → Google BigQuery pipeline: bing\_OWOXAdCostData | bing\_OWOXAdCostData |
| `{{dataset_id_twitter}}` | STRING | The dataset ID where Twitter data is located. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_twitter}}` | STRING | The table ID where Twitter data is located. It is constant value for OWOX BI Twitter → Google BigQuery pipeline: twitter\_OWOXAdCostData | twitter\_OWOXAdCostData |
| `{{dataset_id_linkedIn}}` | STRING | The dataset ID where LinkedIn data is located. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_linkedIn}}` | STRING | The table ID where LinkedIn data is located. It is constant value for OWOX BI LinkedIn → Google BigQuery pipeline: linkedin\_AdCostData | linkedin\_AdCostData |
| `{{dataset_id_adroll}}` | STRING | The dataset ID where AdRoll data is located. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_adroll}}` | STRING | The table ID where AdRoll data is located. It is constant value for OWOX BI AdRoll → Google BigQuery pipeline: adroll\_OWOXAdCostData | adroll\_OWOXAdCostData |
| `{{dataset_id_tiktok}}` | STRING | The dataset ID where TikTok data is located. We recommend to create separated dataset, due to the amount of tables in this dataset. | adroll\_OWOXAdCostData |
| `{{dataset_id_hotline}}` | STRING | The dataset ID where Hotline data is located. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_hotline}}` | STRING | The table ID where Hotline data is located. It is constant value for OWOX BI Hotline → Google BigQuery pipeline: hotline\_OWOXAdCostData | hotline\_OWOXAdCostData |
| `{{dataset_id_google}}` | STRING | The dataset ID where Google Ads Data Transfer data is collected. In case of using Google Ads → Google BigQuery pipeline, the value should be a dataset where pipeline data is collected. | GoogleAds |

### Custom Table

Specify the dataset and table with custom cost data.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{dataset_id_custom}}` | STRING | The dataset ID where custom data is located. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_custom}}` | STRING | The table where custom data is located | custom\_data |

### Transformation results

Specify where to save transformation results.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{dataset_id_ga4_import}}` | STRING | The dataset ID where the prepared for import to GA4 table is located. Place, where results of transformation would be saved. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_ga4_import}}` | STRING | The table ID where prepared for import to GA4 data is located. It is constant value: GA4\_CostData\_Import | GA4\_CostData\_Import |
| `{{dataset_id_blended}}` | STRING | The dataset ID where the blended cost data from ad services is located. Place, where results of transformation would be saved. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_blended}}` | STRING | The table ID where where the blended cost data from ad services is located. It is constant value: BlendedAdSpend | BlendedAdSpend |

## Template result: data schema of the final destination table

You will get the data in the table '**BlendedAdSpend**' (with partitioning by `date` field by days) with the schema below:

| Field name | Type |   |
| --- | --- | --- |
| `utmId` | STRING | The main component of schema, that allows Non-Google costs to be matched with website's traffic. <br>[More about utm\_id](https://www.owox.com/blog/use-cases/utm-id/). |
| `source` | STRING | The source of the ad costs. |
| `medium` | STRING | The medium of the ad costs. |
| `campaign` | STRING | The campaign of the ad costs. |
| `keyword` | STRING | The keyword of the ad costs. |
| `adContent` | STRING | The adContent of the ad costs. |
| `adGroup` | STRING | The ad group name of the ad costs. Please note that the field is only applicable for `google / cpc` |
| `date` | DATE | The date is formatted as YYYY-MM-DD. |
| `adCost` | FLOAT | The sum of ad costs. |
| `impressions` | INTEGER | The total number of impressions. |
| `adClicks` | INTEGER | Total number of times users have clicked on an ad to reach the property. |
| `currency` | STRING | The code of a currency. |
| `adAccount` | STRING | Contains info about the source ad account. |
| `changedTime` | INTEGER | Time, when this information was written to table. Can be used for analysis and for some datamarts. |
| `dataSource` | STRING | The source of data. |
| `campaignType` | STRING | The type of ad campaign the costs were spent on. |
| `campaignId` | STRING | The ID of ad campaign the costs were spent on. |
| `campaignName` | STRING | The name of ad campaign the costs were spent on. |
| `adGroupId` | STRING | The ad group ID. |
| `adGroupName` | STRING | The ad group name. |
| `adSource` | STRING | Data source. |
| `pipelineId` | STRING | Internal technical information. |

## Changelog of the 'Blended AdSpend + GA4 Cost Data Import' template

### July 16, 2024 - v.1.0.5

**Renamed Operation**: Renamed Google by Request to GoogleAds by OWOX.  
**Updated Operation Name**: Renamed Google DataTransfer to GoogleAds DataTransfer.  
**Cleaned SQL Code**: Removed "by Request" mentions from the SQL code.

### October 19, 2023 - v.1.0.4

**Supported date ranges for custom expenses:** Adjusted the 'A - Custom' operation code to support date ranges for custom expenses. Clients no longer need to fill in expenses in the custom expense template on a daily basis. They can now specify a start date and an end date, along with the total expenses, clicks, and impressions. These values will be evenly distributed across all the days within the specified date range. If a client sets the start date equal to the end date, it is equivalent to filling in expenses on a daily basis.

**Changes in the [Google Sheets template for custom expenses](https://docs.google.com/spreadsheets/d/1QJR-cxV_2uPOOvYBkc_mMFzdfF8CqrRZ5ak7yrcVtMw/edit#gid=0):**

-   Renamed the 'date' field to 'date\_start.'
-   Added the 'date\_end' field.

Example data entries for daily, monthly, two-month, and one-week expense distributions are provided in rows 1-6.

###   
  
September 29, 2023 - v.1.0.3

**TikTok Data Integration:** We've expanded data acquisition capabilities by introducing TikTok data retrieval into BlendedAdspend through the ByRequest stream (operation A - TikTok).

**Data Schema Enhancement:** Our data schema now includes an INTEGER-type field, `changedTime`; This field captures the timestamp of data row insertion into the table. In the future, it will prove invaluable for researching spending change periods and addressing client inquiries related to expenditures.

### July 25, 2023 - v.1.0.2

**Deprecated Gclid Parsing:** We have removed the operation 'U - GA4 Sessionization (gclids from old DT)' responsible for parsing gclids from the old dataTransfer. This operation was deprecated in April and is no longer functional. It's worth noting that all new clients are now using either the new dataTransfer or the ByRequest stream.

**Streamlined Gclid Parsing:** The operation 'U - GA4 Sessionization (gclids from new DT)' has undergone improvements. It has been renamed to 'U - GA4 Sessionization (gclids from DT)' and enhanced to eliminate the need for specifying 'table\_suffix' in cases where a client configures data extraction from multiple MCC accounts into a single dataset.

**Obsolete Variable Removal:** We've eliminated the variable 'dt\_objects\_suffix' as it is no longer in use.

### June 22, 2023 - v.1.0.1

**Optimization and Streamlining:** We've optimized our code by consolidating operations. Specifically, we merged 'U - GA4 Sessionization Step 4' and 'A - GA4 Sessionization Step 5' into a single operation, now named 'A - GA4 Sessionization Step 4.'

**Improved Data Flow:** To enhance data integrity and minimize issues with data loss and transformation limitations, we've strategically relocated 'D - GA4 Sessionization' closer to the final results appending stage. This ensures that even in scenarios where data may have been deleted, subsequent transformations won't encounter bottlenecks, and new data won't go unrecorded.

### May 02, 2023 - v.1.0.0

**The new template added.**
