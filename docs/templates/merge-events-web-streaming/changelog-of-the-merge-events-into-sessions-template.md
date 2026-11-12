# Changelog of the 'Merge Events into Sessions' template.

## November 01, 2024 - v.2.06

**Improved Session Handling for SPA and Multi-Tab Browsing**: Added logic to handle sessions where users enter via paid ads and stay on the site through SPA or multiple browser tabs. New organic sessions will not be created in such cases, keeping the session defining aligned with the initial traffic source.  
**Removal of session\_start as a Session-Break Trigger**: The session\_start event is no longer a condition for session breaks, preventing unnecessary breaks due to default GA4 timeouts.  
**Break Rule Analysis Field**: Introduced the `break_rule` field in session customDimensions to quickly identify session-creation criteria.  
**LNDC Date Tracking**: Added `lndc_date` in session customDimensions, indicating the date of LNDC model application to help define the appropriate lookback period.  
**Session Break Debugging Tool**: Included debug code for quick session break analysis, intended for internal use by OWOX teams.

## September 17, 2024 - v.2.05

**Product-Level Parsing**: Added customDimensions and customMetrics parsing for product-level data:  `hits.product.customDimensions.key` and `hits.product.customMetrics.key` added.  
**Session Duration**: Introduced the `timeOnSite` field to track session length in seconds.  
**Bounce Session Detection**: Added the `isBounceSession` field, which identifies whether a session was a bounce (1) or not (0) based on page views and interaction types.  
**Exclusion of Non-Consenting Users**: Automatic events from non-consenting users are now excluded from merging into sessions.

## April 12, 2024 - v.2.04

**Added cleanup for the android-app source**: this source may occur for users transitioning from a mobile browser. Previously, it was assumed to always be google traffic, but there are cases where these are transitions with email campaign tags. After the recent updates, the source / medium for such transitions will be correctly identified (previously always set to google / cpc if campaign/keyword/adContent were present, or google / organic if no additional tags were present).

## April 1, 2024 - v.2.03

**Better gclid defining**: we have fixed the code so that gclid is considered even if the referrer is empty.

**Improved gclid date defining**: in the gclid parsing operation for dataTransfer and GoogleAds by OWOX, we now account for cases where different time zones may cause gclid in the advertising account and user behavior data to fall on different dates. To address this, a +/-1 day offset is applied to the gclid search date.

**New names:** we have renamed template and operations to more accurately reflect their functionality.

## March 13, 2024 - v.2.02

**visitStartTime field has been reverted**: We have reverted the visitStartTime field to the standard format, now using UNIX\_SECONDS (10 characters). In versions v2.00-2.01, this field used UNIX\_MICROS (16 characters), which could cause issues with queries if they were used in subsequent reports.

## March 07, 2024 - v.2.01

**Improvements in traffic determination for AMP pages**: We have made changes to the traffic determination logic for AMP pages to ensure more accurate attribution. Previously, all AMP pages were automatically classified as google / organic. Now, if at least one of the parameters campaign, keyword, or adContent is filled, they will be classified as google / cpc. Otherwise, they will be classified as google / organic.

**Enhancements in handling empty values:** We have made adjustments to the handling of empty values for the campaign, keyword, and adContent parameters. Previously, when using the LNDC model, if the parameter was not filled, the value could be pulled as null. Now, if the parameter is empty, the value (not set) will be used. This allows for more accurate reflection of data states and prevents distortions due to incomplete data.

## February 28, 2024 - v.2.00

**Streamlining data processing**. We've optimized our data processing workflow by consolidating "O - GA4 Sessionization Step 1" and "O - GA4 Sessionization Step 2." This consolidation has resulted in a reduction of intermediate tables by 1, thereby minimizing data extraction and processing, consequently reducing the number of Operation Runs required.

**Enhanced gclid determination logic**. We've refined the logic for identifying genuine Gclid instances. Now, a Gclid is considered valid only if the referrer contains "google," effectively excluding cases where users copy Gclids within URLs, ensuring more accurate attribution. Under the new logic, such instances are marked as (direct) / (none), with any associated markup subtracted. Additionally, only genuine gclids (clicks from Google) are recorded in the trafficSource.gclid field, while all gclids are captured in the hits.customDimensions field.

**Improved gclid parsing**. Our gclid parsing mechanism now retrieves the actual campaign name for a specific date, facilitating precise attribution even during campaign name transitions. For example, if a campaign named "campaign\_1" on 01.01.2024 is renamed "campaign\_2" on 15.01.2024, sessions collected from 01.01.2024 retain the name "campaign\_1" until 15.01.2024 when they are updated to "campaign\_2."

**Enhanced tagging prioritization**. We've refined the prioritization of manual and auto-tagging methods to prevent data inconsistencies. Whether manual or auto-tagging is prioritized, if at least one of the fields (source, medium, campaign, keyword, adContent, adGroup) is filled, other fields are not overwritten. This prevents inadvertent mixing of manual and auto-tagging.

**Improved Merging Operation**. Our "U - Sessionization (LNDC)" operation now considers referral exclusion lists. This ensures that newly added sources are not retrospectiively pulled from previous days, maintaining data integrity.

**Enhanced Tracking Insights**. The hits.dataSource field now provides information on whether events were sent via the Measurement Protocol (MP) or Client Side (WEB), offering greater visibility into event origins and tracking methods.

## December 12, 2023 - v.1.06

**A new field was added.** The new field was added to the result table schema - platform.   
This field by default filled with "WEB" values, if session was created by this template.

## November 14, 2023 - v.1.05

**Revised the logic for determining the source with disabled auto-tagging, closely aligning it with GA UA merging hits into events.** When you prioritize manual tagging, the system checks for gclid in the session. If present, it then verifies the presence of utm parameters, extracting their values. If utm\_source and utm\_medium are empty, the default value becomes google/cpc.

**Implemented a check for the number of events per user per day.** Users with over 10,000 events in a day are excluded from the merging due to potential bot-like behavior.

**Adjusted the population of parameters hits.transaction.transactionId and hits.transaction.transactionRevenue.** Now, if the transaction format is incorrectly passed (e.g., using INTEGER or FLOAT instead of STRING), and ecommerce is not filled, values are extracted from event\_params for the respective parameters.

## September 19, 2023 - v.1.04

**Renamed "Sessionization" to "Sessionization - OWOX BI Events Streaming"** to prevent confusion between sessionization on OWOX GA4 streaming data and sessionization on GA4 Export data.  
**Implemented proper handling of session breaks** when a user switches from "google / cpc" to "google / organic." Previously, sessions were not interrupted due to the source being labeled as "google / organic" for such events in the "events\_intraday\_" table. As a result, source changes were not recorded, and new sessions were not initiated.  
**Adjusted handling of sessions originating from "android:app//google.com."** Previously, such sessions were categorized as "android:app / referral," but they are now categorized as "google / organic." **Introduced population of the "trafficSource.channelGrouping"** field following old GA UA logic. **Removed "GA4"** from operation names for clarity.

## July 28, 2023 - v.1.02

**Removal of operation U - GA4 Sessionization (gclids from old DT):** One of the significant changes was the removal of an operation related to parsing gclids from the old dataTransfer. This update was crucial as the operation was deprecated in April and had ceased to function.  
**Adjustment of operation U - GA4 Sessionization (gclids from new DT)**: This operation was renamed to U - GA4 Sessionization (gclids from DT) and was enhanced. Now, there is no need to specify table\_suffix when a client sets up data extraction from multiple MCC accounts into a single dataset.  
**Deletion of the variable dt\_objects\_suffix**: This variable is no longer used and has been removed.

## June 22, 2023 - v.1.01

**Code optimization and operation merging**: Two operations, U - GA4 Sessionization Step 4 and A - GA4 Sessionization Step 5, were combined into a single operation named A - GA4 Sessionization Step 4.  
**Relocation of operation D - GA4 Sessionization**: The operation was moved closer to appending final results, minimizing cases where data deletion was followed by a transformation that hit limits and couldn't write new data.

## June 16, 2023 - v.1.00

**Addition of manual tagging handling**: In this update, the capability to handle manual tagging in conjunction with Bing and Facebook auto-tagging was added.  
**Exclusion of certain fields from hits.customDimensions storage**: Fields like source, medium, campaign, term, content, and others were excluded from storage in hits.customDimensions.

## June 09, 2023

**Correction of parsing logic for product labels**: This update focused on correcting the parsing logic for product labels, especially when gclid is present in page\_location.  
**Addition of source/medium determination at transformation level**: Now, if mscklid is present in the markup, the field `trafficSource.mscklid` is added to the data schema.  
**Introduction of the user.user\_pseudo\_id field**: This field was introduced to keep track of the user identifier when forming sessions.

## May 20, 2023

**Preservation of user\_pseudo\_id**: User\_pseudo\_id is now preserved in the user.user\_pseudo\_id field. Previously, this field wasn't saved during sessionization based on owox\_user\_id.  
**Filling "(not set)" for campaign, keyword, adContent fields**: If campaign, keyword, or adContent values are undefined, "(not set)" is now assigned instead of null.  
**Enhancement of gclid parsing for by-request stream**: Logic for parsing gclid from the ByRequest pipeline was improved to consider adGroup and offer the option to select based on table\_suffix.

## May 08, 2023

**Correction of code**: In this update, corrections were made to the code. The "D - GA4 Sessionization" step is now enabled by default and doesn't lead to errors when the owoxbi\_ga4\_sessions table is absent. Additionally, the logic for the adContent value was adjusted to be sourced from the appropriate field. The events first\_visit and session\_start are now categorized as non-interactive events. Parsing of adGroup was added for both new and old dataTransfer, with plans to add it for the by-request pipeline when a client with that setup appears.

## March 31, 2023

**Correction of code**: In this update, corrections were applied to the code. In cases where a source is present in the referral exclusion list, a session with source / medium = (direct) / (none) is now created, as opposed to the previous (direct) / (not set).

## March 17, 2023

**Correction of code**: To handle a large volume of data, optimization was carried out on the code. The process was divided into several steps using temporary tables, which helped avoid errors due to memory consumption limits and optimized data processing.

## February 28, 2023

**Addition of identifier selection**: This update introduced the ability to choose an identifier. This parameter can be set on the "GA4 Sessionization Inputs" sheet in the Primary Identifier field. Two options were added: user\_pseudo\_id and owox.user\_id.  
**Change in referral exclusion list check**: The check is now based on inclusion in the list, rather than exact matching. To specify the referral exclusion list, a "|" separator is now used instead of ",".

## January 23, 2023

**Exclusion of profiling code**: This update involved excluding profiling code. This change was due to the fact that profiling is now done during the modeling stage rather than during sessionization.  
**Division of code into stages**: Sessionization was divided into two stages - profiling and sessionization. This ensured proper handling of large data volumes and prevented errors related to memory limits

## January 09, 2023

**Correction of profiling code and handling of identifiers**: In this update, corrections were made to the profiling code and handling of cases where clients provide identifiers '0', '-', '', 'null'. This prevented the creation of a single large "superuser" and avoided errors in queries.  
**Division of code into stages**: Sessionization was divided into multiple stages to avoid errors due to memory consumption limits. The stages include extracting event data, preparing session and hit-level parameters, preparing a temporary table for changing labels, applying the model to data, and appending data to the final table.
