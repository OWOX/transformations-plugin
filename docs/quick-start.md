# Quick start

## Introduction

Welcome to the OWOX BI Transformation guide, which helps you set up all features and get analytics-ready data for your reports.

![\_\_\_\_01.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/01/public)

OWOX BI Transformation is a self-service analytics tool to automate routine tasks of preparing and updating data for reporting. Use [prebuilt SQL transformations](https://github.com/OWOX/transformations-plugin/tree/main/docs/templates) or create your own to achieve any kind of analytics challenges.

### Use cases

Data analysts can use the OWOX BI Transformation to:

-   [Blend cost data](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/blended-adspend.md#about-blended-adspend--ga4-cost-data-import-template) across all channels;
-   [Get merged session](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#about-merge-events-into-sessions-template) from raw data (hits or events);
-   Build a single cross-device user profile;
-   Get user type (new or returning);
-   [Attribute ad cost to a session](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/costs-attribution.md#about-costs-attribution-template);
-   [Calculate attribution models](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/standard-attribution.md#about-standard-attribution-models-template) such as Last-click, Fist-click, U-shape, the algorithmic Funnel Based, and custom models;
-   And more…

Why you should build your solution with OWOX BI Transformation:

-   Write your [SQL-based Transformations](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#creating-a-new-transformation).
-   Split multi-line SQL code [into separate Operations](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#creating-a-new-operation) and reduce the complexity of your data preparation process.
-   [Use variables](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#dynamic-variables) for date ranges, project/dataset/table names, etc. This will speed up your efficiency.
-   Get up-to-date data for your reports without headaches by [using the auto-run triggers](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab): by time or by dependency.
-   Clear and helpful [history log](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#run-history-tab). You can monitor data processing at any time.
-   Track how data moves and transforms in analyst-friendly UI ([OWOX BI Workspace](https://www.owox.com/docs/getting-started/)).
-   [Templates gallery](https://github.com/OWOX/transformations-plugin/tree/main/docs/templates) with pre-build Transformations.

### Getting started requirements

-   You are using the Google Cloud Platform and have an active project ([how to set up GCP](https://www.owox.com/docs/storages/google-bigquery/)).
-   The data you will work with is stored in Google BigQuery.
-   You have access to this data as **BigQuery Admin** or **BigQuery Data Owner**, and you can share access to the OWOX BI service account ([how to share access](https://www.owox.com/docs/storages/google-bigquery/)).
-   Your plan includes OWOX BI Transformation. If you don't see it in the OWOX BI interface, contact your OWOX manager ([bi@owox.com](bi@owox.com)).

### Transformations and Operations

In the OWOX BI interface, you can create Transformations and Operations (inside of Transformation).

A Transformation is a set of one or more Operations grouped by common logic. You can run a Transformation manually or set up triggers for autoruns. Running a Transformation executes the Operation code in the order you specify.

An Operation is an SQL code snippet saved in the editor. This SQL code executes with the Google BigQuery API when the Transformation runs. The query result will be saved to a new or existing table in Google BigQuery. Read more in the article [Create and run transformations](https://github.com/OWOX/transformations-plugin/blob/main/docs/quick-start.md#create-and-run-transformations-step-by-step-instructions).

### Terms of Usage

Read the terms of use in [this article with examples](https://www.owox.com/docs/getting-started/consumption-units/).

## Create and run transformations: step-by-step instructions

In this article, you will find step-by-step instructions about how to create a Transformation with a set of Operations and how to run it in the OWOX BI interface.

> **Important:**  
> Please make sure you meet the [minimum requirements](https://github.com/OWOX/transformations-plugin/blob/main/docs/quick-start.md#introduction) with OWOX BI Transformation functionality.

### Step 1. Create a new Transformation

1.1. Go to the [Workspace page](https://bi.owox.com/ui/app/none/workspace). While you do not have any Pipeline, Streaming, or Transformation yet, then you will see the Welcome screen. Click on the “**New transformation**” button.  
![Frame\_2025.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/02/public)

1.2. Otherwise, click the "**\+ New...**" button in the top panel over the diagram if you have one or more Pipeline, Streaming, or Transformation. Click on the “Transformation” menu item.

![\_\_\_\_create-transfrom.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/03/public)

1.3. Create a **new blank** or **template-based** Transformation. Choose one option from the list in the sidebar:

![1120.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/04/public)

While browsing the [Templates gallery](https://github.com/OWOX/transformations-plugin/tree/main/docs/templates), you can read the detailed template description and see a list of Operations.

After selecting an option, click on the “**Create & Setup**” button.

### Step 2. Create Operations

2.1. On the Transformation page, go to the **Code Editor** tab. You will see that the new Transformation already has the first Operation with the SQL code `"SELECT 1;"`.

![\_\_\_04.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/05/public)

**How to configure a Transformation template**

If you have created a Transformation from a template, you need to enter the correct values for the variables according to the instructions provided. You can find these instructions [in the section that describes the templates](https://github.com/OWOX/transformations-plugin/tree/main/docs/templates).

2.2. Write your custom SQL code in the editor. And [create multiple Operations](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#creating-a-new-operation) in one Transformation. It will help break down the data transformation process into several logical steps. You can easily change the order of the Operations in the Transformation.

![\_\_\_05.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/06/public)

2.3. Validate your code. The entered SQL code undergoes validation to ensure that the query can be executed when the Transformation is run. If there are any errors during the validation process, you will see them in the top toolbar above the code. [In this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#validations-and-estimations), you can see some examples of common errors that can occur during SQL query validation. 

When the code validation is successfully passed, you will see a green mark that says "Valid SQL code". You can proceed to the next step of this instruction.

2.4. (Optional) Specify a destination table for the Operation.

![\_\_\_08.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/07/public)

When you run the Transformation, the OWOX BI algorithm will save the result of executing SQL code into the table in Google BigQuery. You can learn more about setting up a destination table in [this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#destination-settings). 

2.5. (Optional) Add variables to the Transformation and use them in the SQL code.

![\_\_\_09.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/08/public)

Variables allow you to set values applied in multiple Operations without changing the SQL code before each Transformation run. Using variables greatly speeds up routine work. Read more about using variables in [this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#dynamic-variables).

2.6. Preview your code. Go to the '**Preview**' tab to see the compiled SQL query that will be executed when the Transformation is run. Read more about the 'Preview' tab in [this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#preview-tab).

![\_02.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/09/public)

2.7. **Save** your changes.

![\_03.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/10/public)

### Step 3. Share used datasets with OWOX BI

3.1. Go to the '**Used datasets**' tab to view the list of used datasets.

![02.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/11/public)

3.2. If a Transformation uses data from BigQuery datasets that are not accessible to OWOX BI, the Transformation cannot be successfully executed. To run the Transformation and obtain the execution results for each Operation, you need to grant access to all the used datasets. To do this, click on the '**Share used datasets**' button. You can read more details in [this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#used-datasets-tab).

3.3. (Optional) If you use a BigQuery table with data from Google Sheet documents then check [this article](https://www.owox.com/docs/sources/google-sheets/).

### Step 4. Run the Transformation manually

Click on the “**Run**” button to start the sequential execution of the Operations in the Transformation.

![\_\_\_12.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/12/public)

> **Important:**  
> Run is only available for Transformations that have no unsaved changes. If you have changed the code or made other changes to the Transformation, be sure to save those changes.

> Also, you can stop running Transformation during execution. It's useful when you have multiple Operations and want to save resources by preventing additional query executions. [Read more here](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#how-to-stop-transformation-run-during-execution).

### Step 5. Viewing run history

After running the Transformation, the “Run history” tab opens. Here you find details about the execution of each Operation.

![\_\_\_13.png](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/quick-start/13/public)

Read more about the Run history tab in [this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#run-history-tab).

### Step 6. Debugging

Write, edit SQL code, and run the Transformation until you solve your task and get the necessary data structure in Google BigQuery.

### Step 7. Autoruns with triggers

Once you've finished debugging and you are sure the Transformation works correctly, you can set up a time trigger. With autoruns, you will get up-to-date data for your reports without headaches. Read more about autorun triggers in [this article](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#triggers-tab).

### Step 8 (optional). Describe your Transformation and Operations

You can specify an 'Owner name', 'Email', and 'Description' fields for your Transformation in the ['**Info**' tab](https://github.com/OWOX/transformations-plugin/blob/main/docs/transformation-settings.md#info-tab). And also you can [add a description for each Operation](https://github.com/OWOX/transformations-plugin/blob/main/docs/operation-settings.md#info-tab).
