**Unreleased**

* Changed `CommvaultAccessToken` asset config field type from `string` to `password` to prevent plaintext exposure in the UI.
* Added automatic access token lifecycle management: tokens are created via the `/v4/accesstoken` API and renewed via `/v4/accesstoken/renew`, with fallback to the original configured token for backward compatibility with older server versions.
* Added security partner registration on each action invocation via `/V4/Company/{id}/SecurityPartners/Register`.
* Replaced `get_incident_details` (which made additional job and file API calls) with `get_incident_details_v2` that parses incident details directly from the event object, removing unnecessary API calls.
* Expanded supported event codes to include `69:59`, `17:193`, `69:60`, `14:337`, `14:338`, and `7:349`, with severity and anomaly type mappings per event code.
* Added `pagingInfo: 0,10000` header to events API calls to retrieve up to 10,000 events per poll.
* Fixed duplicate action result entries: `check_create_renew_token`, `register`, and `_fetch_anomalous_events` no longer call `add_action_result`, as the action handlers already register their own action results.
* Fixed secret exposure in debug logs: removed logging of request payloads, full token API responses, stored token details, and the initialized auth header containing the access token.
