# Variables list for transformation template 'Blended AdSpend + GA4 Cost Import (With Currency Convert)'

> **Note:**  
> The template has most of the essential variables by default, so there is no need to enter all the values from the beginning.

## Period

Specify the period for which you want to perform the transformation.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{start_suffix}}` | STRING | The start variable is responsible for the period's start date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery.<br>In other words, this is the beginning of the period during which the transformation needs to be performed.<br>We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer.<br>Additionally, instead of SQL code, you can specify a specific date in the date format here, for example, `CAST ('20230101' AS STRING)`. | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 1 DAY)) |
| `{{end_suffix}}` | STRING | The end variable is responsible for the period's end date for which transformation should be performed. Example value is an SQL code that takes one day less than the current date and turns it into a string that is understandable for Google BigQuery. Thus, this transformation would take dates between start\_suffix and end\_suffix.<br>This is the end of the period during which the transformation needs to be performed. We recommend using a data refresh interval of 1 day to save resources, but you can use any interval you prefer. Additionally, instead of SQL code, you can specify an end date in the date format, for example, `` CAST ('20230101' AS STRING)`.` `` | FORMAT\_DATE('%Y%m%d',DATE\_SUB(CURRENT\_DATE(), INTERVAL 1 DAY)) |

## Ads Data Pipelines

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

## Custom Table

Specify the dataset and table with custom cost data.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{dataset_id_custom}}` | STRING | The dataset ID where custom data is located. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_custom}}` | STRING | The table where custom data is located | custom\_data |

## OpenExchangeRate table

Specify the dataset and a table with exchange rates data.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{dataset_id_currency}}` | STRING | The dataset ID where the result of Openexchangerate.org → Google BigQuery pipeline is located.  | Openexchangerates |
| `{{table_id_currency}}` | STRING | The table where exchange rates are located. It is a constant value for OWOX BI Openexchangerate.org → Google BigQuery pipeline: exchange\_rates | exchange\_rates |
| `{{convert_currency}}` | STRING | The currency to which all the convertations would be made.  | USD |

## Transformation results

Specify where to save transformation results.

| Variable name | Type | Description | Example of value |
| --- | --- | --- | --- |
| `{{dataset_id_ga4_import}}` | STRING | The dataset ID where the prepared for import to GA4 table is located. Place, where results of transformation would be saved. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_ga4_import}}` | STRING | The table ID where prepared for import to GA4 data is located. It is constant value: GA4\_CostData\_Import | GA4\_CostData\_Import |
| `{{dataset_id_blended}}` | STRING | The dataset ID where the blended cost data from ad services is located. Place, where results of transformation would be saved. We recommend to use unified dataset OWOXBI\_BlendedAdSpend | OWOXBI\_BlendedAdSpend |
| `{{table_id_blended}}` | STRING | The table ID where where the blended cost data from ad services is located. It is constant value: BlendedAdSpend | BlendedAdSpend |
