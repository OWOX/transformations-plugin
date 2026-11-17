# Template result: data schemas of the final destination tables

## Overview

You will get several tables for each attribution modeling result, and one, that summarizes all previous attributions in one table.  
  

## Last Non-Direct Click (attributionLNDC table)

| Field name | Type | Description |
| --- | --- | --- |
| `session_date` | STRING | Session date. |
| `sessionId` | STRING | The ID of a session.  |
| `conversion_date` | STRING | Date of conversion. This field is used for partitioning of table. |
| `conversionId` | STRING | The ID of conversion. This could be hitId field for events with page\_view or transactionId for transactions. |
| `value` | STRING | The exact value of a session with some channel, according to the LNDC attribution model. |
| `lndc_session` | STRING | The session with conversion, according to the LNDC attribution model. |

## First Click (attributionFirstClick table)

| Field name | Type | Description |
| --- | --- | --- |
| `session_date` | STRING | Session date. |
| `sessionId` | STRING | The ID of a session.  |
| `conversion_date` | STRING | Date of conversion. This field is used for partitioning of table. |
| `conversionId` | STRING | The ID of conversion. This could be hitId field for events with page\_view or transactionId for transactions. |
| `value` | STRING | The exact value of a session with some channel, according to the First Click attribution model. |
| `lndc_session` | STRING | The session with conversion, according to the LNDC attribution model. |

## Linear (attributionLinear table)

| Field name | Type | Description |
| --- | --- | --- |
| `session_date` | STRING | Session date. |
| `sessionId` | STRING | The ID of a session.  |
| `conversion_date` | STRING | Date of conversion. This field is used for partitioning of table. |
| `conversionId` | STRING | The ID of conversion. This could be hitId field for events with page\_view or transactionId for transactions. |
| `value` | STRING | The exact value of a session with some channel, according to the Linear attribution model. |
| `lndc_session` | STRING | The session with conversion, according to the LNDC attribution model. |

## Position Based (attributionPositionBased table)

| Field name | Type | Description |
| --- | --- | --- |
| `session_date` | STRING | Session date. |
| `sessionId` | STRING | The ID of a session.  |
| `conversion_date` | STRING | Date of conversion. This field is used for partitioning of table. |
| `conversionId` | STRING | The ID of conversion. This could be hitId field for events with page\_view or transactionId for transactions. |
| `value` | STRING | The exact value of a session with some channel, according to the Position Based attribution model. |
| `lndc_session` | STRING | The session with conversion, according to the LNDC attribution model. |

## Time Decay (attributionTimeDecay table)

| Field name | Type | Description |
| --- | --- | --- |
| `session_date` | STRING | Session date. |
| `sessionId` | STRING | The ID of a session.  |
| `conversion_date` | STRING | Date of conversion. This field is used for partitioning of table. |
| `conversionId` | STRING | The ID of conversion. This could be hitId field for events with page\_view or transactionId for transactions. |
| `value` | STRING | The exact value of a session with some channel, according to the Time Decay attribution model. |
| `lndc_session` | STRING | The session with conversion, according to the LNDC attribution model. |

## Attribution (attribution table)

| Field name | Type | Description |
| --- | --- | --- |
| `session_date` | STRING | Session date. |
| `sessionId` | STRING | The ID of a session.  |
| `conversion_date` | STRING | Date of conversion. This field is used for partitioning of table. |
| `conversionId` | STRING | The ID of conversion. This could be hitId field for events with page\_view or transactionId for transactions. |
| `lndc_session` | STRING | The session with conversion, according to the LNDC attribution model. |
| `lndc_value` | STRING | The value, according to the LNDC model |
| `fc_value` | STRING | The value, according to the First Click model |
| `l_value` | STRING | The value, according to the Linear model |
| `pb_value` | STRING | The value, according to the Position Based model |
| `td_value` | STRING | The value, according to the Time Decay model |

## Data Mart (attributionCheck table)

| Field name | Type | Description |
| --- | --- | --- |
| `sessionDate` | DATE | Session date. |
| `dataSource` | STRING | The data source of the visit.  |
| `sessionId` | STRING | The ID of session.  |
| `visitStartTime` | INTEGER | Time of the first visit in timestamp format.  |
| `conversionDate` | DATE | The date of conversion.  |
| `conversionId` | STRING | The ID of conversion. This could be hitId field for events with page\_view or transactionId for transactions. |
| `status` | STRING | Status, if this data matched your CRM data, or not.  |
| `source` | STRING | The source of the session with conversion |
| `medium` | STRING | The medium of the session with conversion |
| `campaign` | STRING | The campaign of the session with conversion |
| `keyword` | STRING | The keyword of the session with conversion |
| `adContent` | STRING | The adContent of the session with conversion |
| `channelGrouping` | STRING | Field for observing changes of standard attribution channels |
| `lndc_value` | FLOAT | The value, according to the LNDC model |
| `fc_value` | FLOAT | The value, according to the First Click model |
| `l_value` | FLOAT | The value, according to the Linear model |
| `td_value` | FLOAT | The value, according to the Time Decay model |
| `pb_value` | FLOAT | The value, according to the Position Based model |
| `fba_value` | INTEGER | The value, according to the [Funnel Based Attribution](https://www.owox.com/blog/articles/funnel-based-attribution-model/) model. Will be added in the future. Right now the value is always 0.  |
