# Transformation templates

- [Getting started with OWOX BI Transformation templates](#getting-started-with-owox-bi-transformation-templates)
- [How to customize a template in 3 simple steps](#how-to-customize-a-template-in-3-simple-steps)
- [How to import data from the Storage to GBQ](#how-to-import-data-from-the-storage-to-gbq)

## Getting started with OWOX BI Transformation templates

OWOX BI Transformation is a powerful tool that allows you to create and run your data transformations using SQL queries in BigQuery. But you don't have to start from scratch with all your Transformations because we have ready-made Transformation templates for you. These templates have been developed by OWOX analysts, who have gathered years of experience in preparing data for marketing reports. Now, all the best practices in marketing analytics are available to you in just a few clicks.

In this article, we will guide you on where to find and explore the full list of available Transformation templates.

### Templates gallery in the Help Center

![\_\_\_109.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-readme/01/public)

All the templates are organized in the "[Templates gallery](https://github.com/OWOX/transformations-plugin/tree/main/docs/templates)" category of our Help Center. Here, you can find detailed descriptions for each template, from its configuration to the data schema in the final BigQuery table.

### List of available templates in the OWOX BI interface

To access the templates from the product interface, go to the [Workspace page](https://bi.owox.com/ui/app/none/workspace), click on "**New**", and then select "**Transformation**".

![\_\_\_110.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-readme/02/public)

On the next screen, you will see a full list of available Transformation templates.  
![\_\_\_111.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-readme/03/public)

On the right side of the list, you will find a description of each template, along with a list of Operations and their descriptions.  
![\_\_\_112.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-readme/04/public)

### Creating new Transformations in your OWOX BI project

You can start using the templates by creating new Transformations in your OWOX BI project. Simply choose the template you want to use, configure it according to your needs, and then run the data Transformation. Once completed, you can use this data in your marketing reports.

### Need Help?

If you have any questions about how to use a specific template or encounter any issues, don't hesitate to reach out to our support team at [support@owox.com](mailto:support@owox.com). We are here to help you make the most of OWOX BI Transformation templates and achieve your marketing analytics goals with ease.

Happy analyzing!

## How to customize a template in 3 simple steps

After successfully creating a Transformation based on a template configuration, you will have a list of variables and Operations with all the necessary settings. Now, you need to customize a few parameters to ensure that each SQL request runs successfully. In this article, we will describe the general steps to configure any Transformation template.

### Step 1. Replace the 'YOUR\_VALUE' text in the variables

![\_\_\_\_01.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-readme/05/public)

As the Transformation template is designed for multiple copies and reuse, it contains a list of variables. Some of these variables already have values that do not need to be changed.

However, in each template, there will be one or more variables to which you need to manually add your custom values. These variables are highlighted with a red background and have a value of "**YOUR\_VALUE**".

For example, each template has variables to indicate the GCP project ID. Note that the accuracy of the dataset path on the 'Used datasets' tab depends on the value of this variable.

You can find the full list of variables for each template in the "[Templates gallery](https://github.com/OWOX/transformations-plugin/tree/main/docs/templates)" section.

###   
Step 2. Enable or disable Operations that you need

![\_\_\_\_02.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-readme/06/public)

Some templates are so versatile that before running the Transformation, you need to review the list of Operations and disable some of them if you don't have the required BigQuery tables for the SQL query.

For instance, the "[Blended Adspend + GA4 Cost Data Import](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend.md)" template has 12 Operations, including data processing from advertising services (Facebook, Twitter, LinkedIn, Criteo, Bing, etc.). If you don't have ad costs in services like Criteo and Bing, you can simply disable these Operations to prevent them from executing during the Transformation run. Read more about this [in the article](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#how-to-ignoreenable-an-operation-for-running).

### Step 3. Share access to used datasets

On the **Used datasets** tab, you can see a list of datasets specified in the SQL queries of this Transformation. If the service account OWOX BI doesn't have access to a dataset, you will see a red text saying "No access."

![\_\_\_\_03.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-readme/07/public)

Check the **GCP project ID** and **Dataset ID**. If you see here the text 'YOUR\_VALUE', then go to step 1 and update variables with correct names.

If the GCP Project ID and Dataset ID are correct, click the "**Share dataset**" button to grant access to this dataset. Please note that only users with BigQuery Admin or BigQuery Data Owner privileges can provide access. Read more about this [in the article](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#used-datasets-tab).

By following these three simple steps, you can easily customize any Transformation template according to your specific needs and ensure the successful execution of your requests. If you have any questions or need further assistance, don't hesitate to reach out to our support team. Happy transforming!

## How to import data from the Storage to GBQ

### Solution Overview

To facilitate convenient data import from any data source: like databases such as MySQL, PostgreSQL, and others, or Adjust, AppsFlyer, or Mixpanel, we offer a solution that allows data to be uploaded to Google BigQuery without requiring access to the database.

### Key Steps in the Process

1.  **Uploading Data to Cloud Storage**  
    You can export data from any data source in CSV format and upload it to a chosen cloud storage service, such as Google Cloud Storage, Amazon S3, or Google Drive.
    
2.  **Granting Access to Storage**  
    Then, it [grants our Service Account access](https://www.owox.com/docs/owox-extension/) to this Storage where the data is stored.
    
3.  **Script Development and Setup**  
    We develop a custom script for data processing in Transformation, which automatically loads the data into Google BigQuery from Storage.
    
4.  **Materializing data in GBQ  
    **After running the Transformations, the data will appear in your GBQ.
    

![owox\_import\_data\_scheme.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-readme/08/public)

### Conclusion

Our solution enables secure and efficient data import from databases to Google BigQuery, ensuring flexibility and protection of the client’s data.
