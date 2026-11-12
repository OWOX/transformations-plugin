# Blended AdSpend + GA4 Cost Import (with currency conversion)

- [About 'Blended AdSpend + GA4 Cost Import (With Currency Convert)' template](#about-blended-adspend--ga4-cost-import-with-currency-convert-template)
- [How to create Transformation from a 'Blended AdSpend' template](#how-to-create-transformation-from-a-blended-adspend-template)
- [Template result: data schema of the final destination table](#template-result-data-schema-of-the-final-destination-table)
- [Changelog of the 'Blended AdSpend + GA4 Cost Import (With Currency Convert)' template](#changelog-of-the-blended-adspend--ga4-cost-import-with-currency-convert-template)

## About 'Blended AdSpend + GA4 Cost Import (With Currency Convert)' template

### Overview

A ‘Blended AdSpend + GA4 Cost Import (With Currency Convert)’ template creates a **BlendedAdSpend** table and a **GA4\_CostData\_Import** table. You’ll get all cost data in an automatically updated, unified, and user-friendly table without unnecessary fields, even if different sources use different currencies. 

This Transformation is available for:

-   OWOX BI fully-managed pipelines from Ad services (Facebook, Bing, Criteo, LinkedIn, Twitter) to Google BigQuery
-   TikTok data from OWOX BI by-request pipeline
-   Google Ads data from OWOX BI fully managed pipeline or [Data Transfer](https://github.com/OWOX/streaming-plugin/blob/main/docs/hit-based/web-tracking/setting-up-raw-data-collection-about-google-ads-campaigns-with-auto-tagging.md)
-   custom costs via [OWOX BI BigQuery Reports Extension](OWOX%20BI%20BigQuery%20Reports%20Extension).

> **Note:**  
> If all of your advertisement systems and calculations use the same currency, please, use the ['Blended AdSpend + GA4 Cost Data Import' template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend.md) for one currency.

All costs received as a result of Blended Adspend are exclusive of taxes. Learn more about taxes in Pipeline in this article.

### Getting started requirements

-   You created a unified dataset **OWOXBI\_BlendedAdSpend** as a destination for pipelines and custom data. [The link](https://www.owox.com/docs/storages/google-bigquery/) provides instructions about creating and sharing datasets with OWOX BI.  
    
    > **Note:**  
    > Otherwise, you must modify the default variables in the transformation template and replace the existing dataset variable names _OWOXBI\_BlendedAdSpend_ with the ones specific to your dataset.
    
-   You created Ad Services — Google BigQuery pipelines in the OWOX BI interface and already have tables with cost data from ad services in your **OWOXBI\_BlendedAdSpend** dataset. Follow these instructions to create fully-managed Ad Services — Google BigQuery pipelines.  
-   You created OpenExchangeRates — Google BigQuery pipeline, and you have a table with currency rates for the needed period. 

### Transformation process

The transformation process inputs the raw data stored in the OWOX BI pipelines’ tables. The output is a table **BlendedAdSpend** with cost data in the [following structure](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend-currency.md#template-result-data-schema-of-the-final-destination-table) and a table **GA4\_CostData\_Import** which contains prepared data in a specific structure. 

Operations are provided in the template and are designed to be easily customizable by inserting the [required variables](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend-currency/variables-list-for-transformation-template-blended-adspend-ga4-cost-import-with-currency-convert.md). The template has most of the essential variables by default, so there is no need to enter all the values from the beginning:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend-currency/01/public)

The actual SQL code of each Operation is automatically generated when the Transformation Template is set up in your OWOX BI Project.

> **Note:**  
> Letters at the beginning of the name of each operation define, in general, what this operation does:  
> D (DELETE) – an operation with the main task of data deletion;  
> O (OVERWRITE) – an operation the result of which is overwriting of some table;  
> A (APPEND) – an operation that adds new data to the table.

Below, you'll find a handy list of operations in the transformation template, each briefly described for your convenience. However, if you're eager to get started, feel free [to jump into the "How to start" article](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend-currency.md#how-to-create-transformation-from-a-blended-adspend-template).

### D – Data cleansing

Initial stage – creates a new transformation from the ‘Blended AdSpend + GA4 Cost Import (With Currency Convert)’’ template in the OWOX BI interface. Then delete the previous `{{table_id_blended}}` table for dates between `{{start_suffix}}` and `{{end_suffix}}`, if it exists.

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
> You'll need to use only one operation of the above for Google Ads Data. If you have both sources from Google Ads, please, turn on 'Ignore for running'  for one of the operations to prevent duplicating the data in the output tables. You can pause or unpause the operation by following the steps in the pictures below: ![google\_ads\_data\_operations.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend-currency/02/public) ![google\_ads\_data\_operations\_.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend-currency/03/public)

### A – Custom

The operation selects data from the custom table generated in Google BigQuery. You can import your own cost data from Google Sheets to the Google BigQuery and use it in ‘Blended AdSpend + GA4 Cost Import (With Currency Convert)’ template. 

**Step 1.** You can find the Google Sheets template for manual adding costs [by the link](https://docs.google.com/spreadsheets/d/1QJR-cxV_2uPOOvYBkc_mMFzdfF8CqrRZ5ak7yrcVtMw/edit?usp=sharing). Please, copy the template to your Google Drive:

![manual\_costs.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend-currency/04/public)

**Step 2.** Fill the values in the template with your cost data.

Please, note, that date ranges should be filled with date\_start and date\_end values: -   In rows 1-3 of the template, there is an example of filling in data by days.
-   In row 4 of the template, there is an example of filling in data for a month.
-   In row 5 of the template, there is an example of filling in data for 2 months.
-   In row 6 of the template, there is an example of filling in data for 1 week.

**Step 3.** Follow the [instructions](https://www.owox.com/docs/sources/google-sheets/) for using the Google Sheets document as a data source for the BigQuery table. 

**Step 4.** Change the variable `{{table_id_custom}}` in the 'Blended Adspend + GA4 Cost Data Import' transformation template to the table's name. For example, if the table has the name 'cute-gbq-project.OWOXBI\_BlendedAdSpend.custom\_data', specify 'custom\_data' in the variable:

![custom\_data.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend-currency/05/public)

**Step 5**. Don't forget to enable operation **A** **— Custom** in the transformation:

![custom.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend-currency/06/public)

If you have questions about importing custom data to Google BigQuery, you can contact us via email at [bi@owox.com](mailto:bi@owox.com).

### O – GA4 CostData Import

The operation prepares data for import to Google Analytics 4 and creates the table **GA4\_CostData\_Import**. Please, use this table during the setup of the Google BigQuery → Google Analytics 4 (via SFTP) pipeline if you want to import cost data to Google Analytics 4.  
Need help with this? Read Import non-Google costs into Google Analytics 4 solution.

> **IMPORTANT:**  
> Please, disable all unnecessary operations. You must select only operations for existing pipelines in your OWOX BI project. For example, if you have Facebook → Google BigQuery pipeline and LinkedIn → Google BigQuery pipeline, the first run of transformation must look like in the screenshot below: ![operations.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend-currency/07/public)

After the last operation, you will get tables with data ready for further analysis and reporting 🎉

## How to create Transformation from a 'Blended AdSpend' template

In this article, you will find step-by-step instructions about how to create a Transformation from the 'Blended AdSpend + GA4 Cost Import (With Currency Convert)' template.

> **Important:**  
> Please make sure you meet the [minimum requirements](https://github.com/OWOX/transformations-plugin/blob/main/docs/quick-start.md#introduction) with OWOX BI Transformation functionality.

### Step-by-step setup

**Step 1.** Go to the Workspace page and click the "New..." button in the top panel over the diagram. Choose the “Transformation” option in the popup menu.

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend-currency/08/public)

**Step 2.** Now you will see the dialog with Templates gallery options. Choose the 'Blended AdSpend + GA4 Cost Import (With Currency Convert)' template from the list in the sidebar:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend-currency/09/public)

**Step 3.** Click on the “Create & setup” button. And you will see your new Transformation:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-blended-adspend-currency/10/public)

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

## Changelog of the 'Blended AdSpend + GA4 Cost Import (With Currency Convert)' template

### July 16, 2024 - v.1.0.5

**Renamed Operation**: Renamed Google by Request to GoogleAds by OWOX.  
**Updated Operation Name**: Renamed Google DataTransfer to GoogleAds DataTransfer.  
**Cleaned SQL Code**: Removed "by Request" mentions from the SQL code.

### February 10, 2024 - v.1.0.0

Added a fresh version of the template.
