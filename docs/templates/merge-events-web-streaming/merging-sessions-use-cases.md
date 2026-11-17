# Merging sessions: use cases

## Use case: Consent Mode

When the website visitor declines consent mode, in the case of using [OWOX BI Streaming](https://github.com/OWOX/streaming-plugin/tree/main/docs/ga4-events-based), any user's personal information (clientId, owox.user\_id, etc.) will not be saved in Google BigQuery or anywhere else: this information would be excluded at the moment of the event parsing.   
  
If there is an event, that has been received with the parameter `'analytics_storage = granted’`, a session will be formed due to expected logic: sessions are created on the primary user identifier that you have selected in [variables of the Merge Events into Sessions template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#variables-list-for-transformation-template-merge-events-into-sessions) , `user_pseudo_id` or `owox.user_id`  
 

If the parameter `'analytics_storage = denied'` is present, indicating that the website visitor did not give consent, the merging process would follow this logic:

-   events with empty `user_pseudo_id` will not be discarded. They would form short single-event sessions, based on a random identifier (`cross_id`), that is generated for them at the SQL code level;
-   these sessions would save their UTM markup if the events have it.

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-merge-events-web-streaming-merging-sessions-use-cases/01/public)  
  

> **Note:**  
> If you want to know more about Consent Mode in OWOX BI Streaming, please, [proceed to this article](https://github.com/OWOX/streaming-plugin/blob/main/docs/ga4-events-based/faq.md#how-ga4-event-based-web-streaming-works-with-google-consent-mode).

## Use case: Session breakup and new session

The algorithm of session creation is very similar to the [old Universal Analytics algorithm](https://support.google.com/analytics/answer/2731565?hl=en).   
Here are the main points of session creation: 

**First event in a day**: If an event occurs for the first time within the current day (time determined by the template time zone in [variables](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#variables-list-for-transformation-template-merge-events-into-sessions)), it initiates the start of a new session.

_Example_: a website visitor came to the website at 23:48 (by the timezone of the website), and looked through several pages. The last page\_view event came at 23:59. But at 00:00 he finally found the stuff he needed, added it to the basket, and bought it at 00:05  
Therefore, in the sessions table, you will see two sessions: one will consist of events from 23:48 to 23:59 and the second - consist of events from 00:00 to 00:05.  

**The interval between events exceeds 30 minutes**: If more than 30 minutes (or another specified period) elapse between two consecutive events, from the same website visitor, on the website, it is considered the end of the current session and the start of a new one. Definitely, this parameter can be changed in [variables of Merge Events into Sessions template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#variables-list-for-transformation-template-merge-events-into-sessions) (`s_timeout` variable), and you can define the session's length on your own. 

_Example_: a website visitor came to the website at 14:11, and looked through several pages. The last page\_view event came at 14:19. After that, the website visitor moved away from the computer, to get some coffee and talk with his colleagues. He returned in 32 minutes, at 14:51, and continued browsing on the website.   
Therefore, in the sessions table, you will see two sessions: one will consist of events from 14:11 to 14:19 and the second - consist of events from 14:51 to the moment, when the website visitor left the website.   

**Change in click markup (gclid, dclid, fbclid, msclid)**: If there is a change in click markup, such as when transitioning from a Google Ads advertisement (gclid), Display Network (dclid), Facebook (fbclid), or Microsoft Advertising (msclid), it initiates a new session.

_Example_: a website visitor searching the web for a good coffee for his coffee machine. Finally, Google advertises your ad, and the website visitor reaches your website. When he clicks on the ad, he receives the parameter 'gclid=12345'. The website visitor looks at that great coffee with doubt: it looks good, but the price is a bit higher than he used to buy. The website visitor sighed and closed your website. And opens Facebook, where he immediately sees the advertisement with the same coffee he looked at. He thinks, that this is fate, and he clicks this Facebook advertisement. And receives the parameter 'fbclid=67890'. At this moment, the previous session is broken, and the new one has started.  
Finally, in the session table, you will see two sessions: one that connected with gclid, and another, that connected with fbclid.

**Change in UTM markup (source, medium, campaign, keyword, adContent)**: If there is a change in UTM tags in the URL, such as source, medium, campaign, keyword, or adContent, it is also considered the start of a new session.

_Example_: a website visitor searching the web for a good coffee for his coffee machine. Through the search, he finds your website and clicks on it. He now receives the source / medium values 'google / organic'. The website visitor looks at that great coffee with doubt: it looks good, but the price is a bit higher than he used to buy. The website visitor sighed and closed your website. He has a good idea of googling more: maybe he can find the same coffee at a lower price. But Google shows him ads with prices, and he understands that coffee is the cheapest on your website. He clicks on the ad and comes back to your website. At this moment, the old session is broken because of a change of medium, and the new session, with the source / medium values 'google / cpc' (and with the campaign value of 'best\_coffee\_ever') starts.  
Finally, in the session table, you will see two sessions: one that has the source / medium values 'google / organic', and another, that has source / medium values 'google / cpc'.

**Change in Referrer not included in the exclusion list**: If there is a change in the referral source (Referrer) that is not included in the referral exclusion list in [the variables of the Merge Events into Sessions template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#variables-list-for-transformation-template-merge-events-into-sessions) (`r_exclusion_list`), it will be interpreted as the start of a new session.

  
_Example_: a website visitor reads about good sorts of coffee on the web. He found an article on the site "extremelygoodcoffee.com". This site is a partner of your shop. So the website visitor clicks on the link to your shop, and receives a source / medium - 'extremelygoodcoffee / cpc' in the freshly started session. He looks at that coffee of his dreams, adds it to the basket, and pays for it. But when he paid, he was forced to the website of the payment system, 'payforalleasily.com'. After successful payment, he is redirected back. However, the website of the payment system was not added to the [referral exclusion list](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#variables-list-for-transformation-template-merge-events-into-sessions) in the template. So, the new session was started.   
Therefore, in the session table, you will see two sessions: one that has the source / medium values 'extremelygoodcoffee / cpc' and another, that has source / medium values 'payforalleasily.com / cpc'. To avoid such situations  
  

## Use case: Auto-tagging and manual tagging

### Manual tagging option

When the  **“Manual tagging”** [option is selected](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#variables-list-for-transformation-template-merge-events-into-sessions), the Merge Events into Sessions algorithm will **first** look at the values in the event\_params.key with event\_params.value.string\_value [pl\_source, ref\_source, rp\_source, source, pl\_medium etc. of the OWOX BI GA4 Streaming table](https://github.com/OWOX/streaming-plugin/blob/main/docs/ga4-events-based/faq.md#how-owox-bi-web-streaming-processes-and-stores-events-with-multiple-sources).   
  
In the model of GA4 tracking could be events with more than one source, medium, campaign, etc. They are called respectively - pl\_source, ref\_source, rp\_source, source, pl\_medium, ref\_medium, etc.   
Based on the Merge Events into Session template logic, by default, the pl\_ group has the highest priority, and this priority can be changed by contacting your CSM.   
More about multiple sources can be found in the [corresponding article](https://github.com/OWOX/streaming-plugin/blob/main/docs/ga4-events-based/faq.md#how-owox-bi-web-streaming-processes-and-stores-events-with-multiple-sources). 

-   If the values of these fields are **not empty**, then they are written changes to the session tables _owoxbi\_sessions_ in the corresponding fields respectively, depending on the chosen values pl\_source, ref\_source, rp\_source, source, pl\_medium, ref\_medium etc. 
-   If the values of these fields are **empty**, then the Merge Events into Sessions algorithm will attempt to find the values of these fields according to the corresponding ‘_gclid_’ [in the table with raw data on Google Ads campaigns](https://github.com/OWOX/streaming-plugin/blob/main/docs/hit-based/web-tracking/setting-up-raw-data-collection-about-google-ads-campaigns-with-auto-tagging.md), if it is [connected to the template](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#variables-list-for-transformation-template-merge-events-into-sessions). 
    -   If data with this ‘_gclid_’ **was found**, then the found values will be written to the session tables _owoxbi\_sessions_. Then, `trafficSource.source` and `trafficSource.medium`will receive google / cpc values. 
    -   The ‘_(not set)_’ value will be written if not found for all, except `trafficSource.source` and `trafficSource.medium` - they will receive direct / (none) values. 

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-merge-events-web-streaming-merging-sessions-use-cases/02/public)

### Auto-tagging option

When the **“Auto-tagging”** option is selected, the Merge Events into Sessions, when generating session data, **first of all**, checks the values of `trafficSource.*`fields for the corresponding ‘_gclid_’ in the [tables with raw data on Google Ads campaigns](https://github.com/OWOX/streaming-plugin/blob/main/docs/hit-based/web-tracking/setting-up-raw-data-collection-about-google-ads-campaigns-with-auto-tagging.md).

-   If the values are **found**, then they are written to the session tables in the`trafficSource.campaign`and`trafficSource.keyword`fields, `trafficSource.source` and `trafficSource.medium`will receive google / cpc values. 
-   If the values are **not found**, then the Merge Events into Sessions algorithm in the next iteration will try to find these data in the event\_params.key with values pl\_source, ref\_source, rp\_source, source, pl\_medium etc. of the OWOX BI GA4 Streaming table.
    -   If data on this ‘_gclid_’ **is found**, then the found value will be written to the session table _owoxbi\_sessions_.
    -   The ‘_(not set)_’ value will be written if not found, except `trafficSource.source` and `trafficSource.medium` - they will receive google / cpc values. 

![](https://imagedelivery.net/zKr-4bdC5CBGL2DuuEmvYw/plugins/transformations/templates-merge-events-web-streaming-merging-sessions-use-cases/03/public)

## Use case: GBRAID and WBRAID

Google Ads presented two new types of automatic tagging: [gbraid and wbraid](https://support.google.com/analytics/answer/11367152?hl=en).  
These identifiers were created as a response to privacy restrictions for users with iOS.   
The problem with these gbraid and wbraid parameters is that Google does not provide details about them in Data Transfer tables (or in any other exported tables).

In this case, you should use manual UTM tags alongside automatic tags. Also, you need to change the [auto tag priority](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming.md#variables-list-for-transformation-template-merge-events-into-sessions) and try to get information about source/medium/campaign/adContent from utm tags first. 

In these cases, if the URL has both: utm and gclid/gbraid/wbraid parameters, we'll get values from utm\_parameters. 

If the URL only has UTM parameters, those values will be used in the reporting. 

If the URL has only gclid/gbraid/wbraid, then we'll try to find values for it in Google Ads DataTransfer tables if possible. 

## Use Case: Timestamp Adjustment

There can be more than one event have the same timestamp in the events table because generally events are batched and are sent together by the site. If a lot of user action is happening together rapidly, it could be batched and get the same timestamp here to boost performance.

When grouping events into sessions, we need to ensure that events are in the right order, even if they share the same timestamp. To do this, we employ a small offset with SQL:

t.timestamp + (ROW\_NUMBER() OVER (PARTITION BY t.cross\_id, t.timestamp ORDER BY timeline ASC) \* 1000) AS adjusted\_timestamp

  
This gives 1 second to every event (sorted by their time) to modestly alter timestamps. This provides an ordered events guarantee and enables precise session boundary calculation.

**Why it's important:**  
Without this correction, events with the same timestamp could be out of order or clumped together, which can cause incorrect session data and analytics.

  
Also, you may be interested in our Merge Events into Sessions template's [Changelog article](https://github.com/OWOX/transformations-plugin/blob/main/docs/templates/merge-events-web-streaming/changelog-of-the-merge-events-into-sessions-template.md): full history of research and changes.
