# How to update transformation's table, if there is a new field added?

In some cases, like [adding platform data to Merge Events into Sessions template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming/changelog-of-the-merge-events-into-sessions-template.md), we add new fields, to the resulting table of some template.   
  
In this case, you need to update your resulting table manually, and that is how it can be done:   
  

> **Note:**  
> If you are not very familiar with Google BigQuery or SQL, please, contact our Support Team on chat or by mail: [bi@owox.com](mailto:bi@owox.com)

### Option 1: Editing the schema with Google Cloud Interface

You can use [an algorithm offered by Google Cloud's official instructions](https://cloud.google.com/bigquery/docs/managing-table-schemas#add_an_empty_column). 

### Option 2: Using an SQL

**Note:** These methods use a lot of resources, so please consult our support department for an approximate cost estimate before using this approach.  
Also, we **strongly recommend** making a copy of your table before adding a field: thus you can restore data, if something goes wrong.

#### 2.1 Example of adding a field at the end of the schema

> **Note:**  
> If you are struggling with getting the whole schema into the SQL query, [ask our SQL Copilot](https://www.owox.com/docs/), he will gladly help you write all schema into the query. Here's the phrase you can start with:  `Hi, can you provide me with an SQL query, that includes all the fields from the table, including nested fields?`

SELECT  
\*,  
CAST(null AS STRING) AS newField  
FROM  
\`project\_id.dataset\_id.owoxbi\_ga4\_sessions\`  
  
#Example of adding field at the beggining of schema  
SELECT  
CAST(null AS STRING) AS newField,  
\*  
FROM  
\`project\_id.dataset\_id.owoxbi\_ga4\_sessions\`

#### 2.2 Example of adding field in the middle of the schema

> **Note:**  
> If you are struggling with getting the whole schema into the SQL query, [ask our SQL Copilot](https://www.owox.com/docs/), he will gladly help you write all schema into the query. Here's the phrase you can start with:  `Hi, can you provide me with an SQL query, that includes all the fields from the table, including nested fields?`

SELECT  
user,  
clientId,  
date,  
sessionId,  
visitNumber,  
newVisits,  
landingPage,  
device,  
geoNetwork,  
trafficSource,  
totals,  
totalsStreaming,  
customDimensions,  
hits,  
CAST(null AS STRING) AS newField,  
privacyInfo,  
visitStartTime,  
platform  
FROM  
\`project\_id.dataset\_id.owoxbi\_ga4\_sessions\`

#### 2.3 Example of adding a field in struct datatype

> **Note:**  
> If you are struggling with getting the whole schema into the SQL query, [ask our SQL Copilot](https://www.owox.com/docs/), he will gladly help you write all schema into the query. Here's the phrase you can start with:  `Hi, can you provide me with an SQL query, that includes all the fields from the table, including nested fields?`

SELECT  
user,  
clientId,  
date,  
sessionId,  
visitNumber,  
newVisits,  
landingPage,  
device,  
geoNetwork,  
trafficSource,  
STRUCT(   
   totals.hits,  
   totals.events,  
   totals.transactions,  
   totals.pageviews,  
   totals.screenviews,  
   totals.isInteraction,  
   totals.visits,  
   CAST(null AS INTEGER) AS newFieldName  
   ) AS totals,  
totalsStreaming,  
customDimensions,  
hits,   
privacyInfo,  
visitStartTime,  
platform  
FROM  
\`project\_id.dataset\_id.owoxbi\_ga4\_sessions\`

#### 2.4 Example of adding a field in repeated record datatype

> **Note:**  
> If you are struggling with getting the whole schema into the SQL query, [ask our SQL Copilot](https://www.owox.com/docs/), he will gladly help you write all schema into the query. Here's the phrase you can start with:  `Hi, can you provide me with an SQL query, that includes all the fields from the table, including nested fields?`

l gladly help you write all schema into the query. 

SELECT  
user,  
clientId,  
date,  
sessionId,  
visitNumber,  
newVisits,  
landingPage,  
device,  
geoNetwork,  
trafficSource,  
totals,  
totalsStreaming,  
customDimensions,  
   ARRAY(  
      SELECT AS STRUCT   
      hits.hitId,  
      hits.isEntrance,  
      hits.isExit,  
      hits.time,  
      hits.timestamp,  
      hits.queueTime,  
      hits.hour,  
      hits.minute,  
      hits.type,  
      hits.isSecure,  
      hits.pagePath,  
      hits.pageType,  
      hits.eCommerceActionType,  
      hits.isInteraction,  
      hits.currency,  
      hits.referer,  
      hits.referralPath,  
      hits.dataSource,  
      hits.device,  
      hits.geo,  
      hits.customGroups,  
      hits.contentGroups,  
      hits.social,  
      hits.page,  
      hits.eCommerceAction,  
      hits.experiment,  
      hits.product,  
      hits.promotion,  
      hits.promotionActionInfo,  
      hits.transaction,  
      hits.contentInfo,  
      hits.appInfo,  
      hits.eventInfo,  
      hits.timingInfo,  
      hits.customDimensions,  
      hits.customMetrics,  
      hits.exceptionInfo,  
      CAST(null AS STRING) AS newField  
      FROM  
      UNNEST(s.hits) AS hits   
      ) AS hits,  
privacyInfo,  
visitStartTime,  
platform  
FROM  
\`project\_id.dataset\_id.owoxbi\_ga4\_sessions\` AS s

#### 2.5 Example of upgrading schema from v2.04 to 2.05

> **Note:**  
> If you are struggling with getting the whole schema into the SQL query, [ask our SQL Copilot](https://www.owox.com/docs/), he will gladly help you write all schema into the query. Here's the phrase you can start with:  `Hi, can you provide me with an SQL query, that includes all the fields from the table, including nested fields?`

SELECT  
platform,  
user,  
clientId,  
date,  
sessionId,  
visitNumber,  
newVisits,  
landingPage,  
device,  
geoNetwork,  
trafficSource,  
totals,  
totalsStreaming,  
customDimensions,  
ARRAY(  
   SELECT AS STRUCT   
      hits.hitId,  
     hits.isEntrance,  
     hits.isExit,  
     hits.time,  
     hits.timestamp,  
     hits.queueTime,  
     hits.hour,  
     hits.minute,  
     hits.type,  
     hits.isSecure,  
     hits.pagePath,  
     hits.pageType,  
     hits.eCommerceActionType,  
     hits.isInteraction,  
     hits.currency,  
     hits.referer,  
     hits.referralPath,  
     hits.dataSource,  
     hits.device,  
     hits.geo,  
     hits.customGroups,  
     hits.contentGroups,  
     hits.social,  
     hits.page,  
     hits.eCommerceAction,  
     hits.experiment,  
     ARRAY(  
          SELECT AS STRUCT  
         product.isImpression,  
         product.impressionList,  
         product.productListName,  
         product.productBrand,  
         product.productSku,  
         product.productVariant,  
         product.productPrice,  
         product.localProductPrice,  
         product.productQuantity,  
         product.productCategory,  
         product.productName,  
         product.position,  
         product.coupon,  
         ARRAY(  
                  SELECT AS STRUCT   
                  cd.index,  
                CAST(null AS STRING) AS key,  
                cd.value  
                FROM  
                UNNEST(product.customDimensions) AS cd  
         ) AS customDimensions,  
         ARRAY(  
                SELECT AS STRUCT   
                cm.index,  
                CAST(null AS STRING) AS key,  
                CAST(null AS FLOAT64) AS value  
                FROM  
                UNNEST(product.customMetrics) AS cm  
         ) AS customMetrics  
FROM  
UNNEST(hits.product) AS product  
) AS product,  
hits.promotion,  
hits.promotionActionInfo,  
hits.transaction,  
hits.contentInfo,  
hits.appInfo,  
hits.eventInfo,  
hits.timingInfo,  
hits.customDimensions,  
hits.customMetrics,  
hits.exceptionInfo  
FROM  
         UNNEST(s.hits) AS hits   
) AS hits,  
privacyInfo,  
visitStartTime,  
(SELECT MAX(h.time)-MIN(h.time) FROM UNNEST(s.hits) AS h) AS timeOnSite,  
(SELECT IF(SUM(IF(h.type IN ('pageview','screenview','screen\_view') OR (h.type='event' AND h.isInteraction=true), 1, 0))<=1, 1, 0) FROM UNNEST(s.hits) AS h) AS isBounceSession  
FROM  
\`project\_id.dataset\_id.owoxbi\_ga4\_sessions\` AS s
