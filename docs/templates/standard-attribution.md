# Standard Attribution Models

- [About 'Standard Attribution models' template](#about-standard-attribution-models-template)
- [How to create Transformation from a 'Standard Attribution models' template](#how-to-create-transformation-from-a-standard-attribution-models-template)
- [Variables list for the 'Standard Attribution models' template](#variables-list-for-the-standard-attribution-models-template)
- [Changelog of the 'Standard Attribution models' template.](#changelog-of-the-standard-attribution-models-template)

## About 'Standard Attribution models' template

### Overview 

A standard attribution model template is used to create one or several tables with the most popular attribution models. In other words, the template allocates conversion value between several interaction channels, saving results separately for each model and saving results in one, combined table.   
  
This transformation uses the data stored in the owoxbi\_ga4\_sessions table, which is a result of the [Sessionization - OWOX BI Events Streaming template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md) work. The output is several tables: one for each attribution model, and one, that joins them all.   
  

> **Note:**  
> Letters at the beginning of the name of each operation define, in all, what this operation does:   
> D (DELETE) - operation with the main task of data deletion;   
> A (APPEND) - operation, that adds new data to the table.

Below, you'll find a handy list of operations in the transformation template, each briefly described for your convenience. However, if you're eager to get started, feel free [to jump into the "How to start" article](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/standard-attribution.md#how-to-create-transformation-from-a-standard-attribution-models-template).

### D - LNDCAttribution

This operation deletes data in the attributionLNDC table for the period of data refresh, between `{{start_suffix}}` and `{{end_suffix}}`, if it exists.

### A - LNDCAttribution

Adds data to the [attributionLNDC table](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/standard-attribution/template-result-data-schemas-of-the-final-destination-tables.md) for the specified period. In this attribution model, all value allocates to the last non-direct click channel. 

### D - FirstClickAttribution

This operation deletes data in the attributionFirstClick table for the period of data refresh, between `{{start_suffix}}` and `{{end_suffix}}`, if it exists.

### A - FirstClickAttribution

Adds data to the [attributionFirstClick table](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/standard-attribution/template-result-data-schemas-of-the-final-destination-tables.md) for the specified period. In this attribution model, all value allocates to the first non-direct click channel. 

### D - LinearAttribution

This operation deletes data in the attributionLinear table for the period of data refresh, between `{{start_suffix}}` and `{{end_suffix}}`, if it exists.

### A - LinearAttribution

Adds data to the [attributionLinear table](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/standard-attribution/template-result-data-schemas-of-the-final-destination-tables.md) for the specified period. In this attribution model, all value allocates between all channels equally. 

### D - PositionBasedAttribution

This operation deletes data in the attributionPositionBased table for the period of data refresh, between `{{start_suffix}}` and `{{end_suffix}}`, if it exists.

### A - PositionBasedAttribution

Adds data to the [attributionPositionBased table](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/standard-attribution/template-result-data-schemas-of-the-final-destination-tables.md) for the specified period. In this attribution model, value is distributed between channels as follows: 40% on the most first channel before conversion, 40% on the last channel before conversion. The remaining 20% is distributed equally to all channels, between the first and last channels.

### D - TimeDecayAttribution

This operation deletes data in the attributionTimeDecay table for the period of data refresh, between `{{start_suffix}}` and `{{end_suffix}}`, if it exists.

### A - TimeDecayAttribution

Adds data to the [attributionTimeDecay table](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/standard-attribution/template-result-data-schemas-of-the-final-destination-tables.md) for the specified period. In this attribution model, value assigned to each channel gradually diminishes (decays) as the interaction with that channel occurred further back in time.

### D - Attribution

This operation deletes data in the attribution table for the period of data refresh, between `{{start_suffix}}` and `{{end_suffix}}`, if it exists.

### A - Attribution

The operation, that [unions all previous tables into one](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/standard-attribution/template-result-data-schemas-of-the-final-destination-tables.md), in which you could compare the results of each model of attribution. After this operation ends, you will get all attribution models in one table, in convenient for further analysis, flat structure. 🎉

### D - Data Cleansing

The operation that is responsible for the preliminary cleansing of data for the Data Mart.   
It is turned off by default. 

### A - Attribution Check

This operation adds data into a [table](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/standard-attribution/template-result-data-schemas-of-the-final-destination-tables.md), that is acceptable for Data Mart. You can copy a [dashboard](https://lookerstudio.google.com/reporting/f9fd0f03-335c-4b71-a5f2-07a21edd4897/page/kWHKD/edit) and connect a table to it and see the distribution of value across different attribution models per session. The dashboard allows you to better understand how different attribution models work and how value is distributed.  
[How to add Google Big Query table as the Data Source in Looker Studio.](https://support.google.com/looker-studio/answer/6295968)   
  
This operation is turned off by default.

## How to create Transformation from a 'Standard Attribution models' template

In this article, you will find step-by-step instructions about how to create a Transformation from the 'Standard Attribution models' template.

> **Important:**  
> Please make sure you meet the [minimum requirements](https://github.com/OWOX/transformations-plugin/blob/main/docs/quick-start.md#introduction) with OWOX BI Transformation functionality.  
>   

### Step-by-step setup

**Step 1.** Go to the Workspace page and click the "New..." button in the top panel over the diagram. Choose the "Transformation” option in the popup menu:   
![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-standard-attribution/01/public)  
  
**Step 2.** Now you will see the dialog with Templates gallery options. Choose the "Standard Attribution Models" template from the list in the sidebar:

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-standard-attribution/02/public)

**Step 3.** Click on the “Create & setup” button. And you will see your new Transformation:  
![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-standard-attribution/03/public)

### How you can customize the template

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

When you create a Transformation from a template, you can customize the list of Operations and their order, edit the SQL code, add or remove variables ([list of variables for 'Standard Attribution models' template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/standard-attribution.md#variables-list-for-the-standard-attribution-models-template)), [set up destinations](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#destination-settings), and [add triggers for autoruns](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab). Best of all, you can use these templates without any limits.

The Transformations created from templates will also be displayed on the Workspace diagram, giving you a clear overview of your data transformation process.

### Run the Transformation and get analytics-ready data

Once you've finished debugging (all variables are set, list of Operations is actual), click on the “Run” button to start the sequential execution of the Operations. Check the status on the [“Run history” tab](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#run-history-tab).

After the successful run, go to your BigQuery account and check the table.

### Automate your data transformation process

Once you've finished debugging and you are sure the Transformation works correctly, you can set up a time trigger. With autoruns, you will get up-to-date data for your reports without headaches. Read more about autorun triggers in [this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab).

> **Important**  
> Please note: we recommend setting time triggers with a gap of five minutes or more for two different transformations, especially if they refer to the same table. This is because two simultaneous requests to the table can cause an error, resulting in the transformation not executing correctly.

### Feedback and support

If you have any feedback or suggestions, please feel free to reach out to us via [bi@owox.com](mailto:bi@owox.com).

## Variables list for the 'Standard Attribution models' template

### Period

Specify the period for which you want to perform the transformation.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{start_suffix}}` | STRING | The start variable is responsible for the period's start date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery.<br>In other words, this is the beginning of the period during which the transformation needs to be performed.<br>We recommend using a data refresh interval of 7 day to save resources, but you can use any interval you prefer.<br>Additionally, instead of SQL code, you can specify a specific date in the date format here, for example, `CAST ('20230101' AS STRING)`. | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 7 DAY)) |
| `{{end_suffix}}` | STRING | The end variable is responsible for the period's end date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery. Thus, this transformation would take dates between start\_suffix and end\_suffix.<br>This is the end of the period during which the transformation needs to be performed. We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer. Additionally, instead of SQL code, you can specify an end date in the date format, for example, `CAST ('20230101' AS STRING).` | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 1 DAY)) |

### Sessions, as initial data

Specify where to get data about sessions, with which the current transformation will work.

> **Important:**  
> Using this template assumes that all your data is located within one GCP (Google Cloud Platform) project.  
> If you store data in more than one project, please contact us via email at [bi@owox.com](bi@owox.com) before proceeding with the setup.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{gcp_project_id}}` | STRING | ID of your project in Google Big Query, where the session table is located for which the current transformation is configured.<br>Place, in which which the whole results of attribution calculations would be saved.  | cute-gbq-project |
| `{{s_dataset_id}}` | STRING | The dataset ID where the session table is located for which the current transformation is configured. | OWOXBI\_GA4\_Streaming |
| `{{s_table_id}}` | STRING | The ID of the table with sessions. Place, in which initial data for the current transformation is saved. Has a standard value: owoxbi\_ga4\_sessions\_ | owoxbi\_ga4\_sessions |

### Additional parameters

Specify additional parameters used for models of attribution

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{c_window}}` | STRING | Specify the Conversion window. <br>It is a number of days before conversion. Only sessions that happened within the conversion window will get value. By default, this parameter is set to 7 days. The length of a conversion window depends greatly on the type of your business.<br><br>In case of changing the conversion window, on the already calculated data, you need to recalculate for the entire period, or delete the tables with the calculation and perform the calculation for the required period. | 7 |
| `{{c_event}}` | STRING | Conversion event - allows you to set the name of the conversion event.<br>For transactions, you must use the standard name purchase, for page views - name of event, like registration\_complete. | purchase **OR** registration\_complete |
| `{{c_url}}` | STRING | Conversion URL - allows you to set the URL where the conversion event occurs (by default it is set as the entire site). | %% - this value stands for whole site. <br>%/conversion% - for the specified conversion page |

### Attribution results

Specify where to save the results of the current transformation.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{r_dataset_id}}` | STRING | The dataset ID where tables, as a result of the current transformation, would be saved. | OWOXBI\_Reports |

## Changelog of the 'Standard Attribution models' template.

### January 10, 2024 - v.1.0.3

**Viewing Attribution Model Changes Without Additional Mergers**: Added the 'channelGrouping' field to the data schema of attributionCheck in the results of attribution model comparison. Now, changes across standard channel groups for various attribution models can be observed without the need for any additional merges.

### October 03, 2023 - v.1.0.2

**Conversion Action Handling:** We've improved how we handle conversion actions submitted without webpage data (via Measurement Protocol). Now, these conversions are properly counted in our analytics.

###   
July 28, 2023 - v.1.0.0

**Added a fresh version of the template.**
