---
nav_title: "GET: Campaign Analytics"
page_order: 4

layout: api_page

page_type: reference
platform: API
tool: Segments
description: "This article outlines details about the Campaign Analytics endpoint."
---
{% api %}
# Campaign Analytics Endpoint
{% apimethod get %}
/campaigns/data_series
{% endapimethod %}

This endpoint allows you to retrieve a daily series of various stats for a campaign over time.

{% apiref swagger %}https://www.braze.com/docs/api/interactive/#/Export/Campaign%20export%20%20analytics%20example {% endapiref %}
{% apiref postman %}https://documenter.getpostman.com/view/4689407/SVYrsdsG?version=latest#c07b5ebd-0246-471e-b154-416d63ae28a1 {% endapiref %}


## Request Parameter Details

| Parameter | Required | Data Type | Description |
| --------- | -------- | --------- | ----------- |
| `api_key` | Yes | String | App Group REST API Key |
| `campaign_id` | Yes | String | Campaign API Identifier |
| `length` | Yes | Integer | Max number of days before ending_at to include in the returned series - must be between 1 and 100 inclusive |
| `ending_at` | No | DateTime (ISO 8601 string) | Date on which the data series should end - defaults to time of the request |
{: .reset-td-br-1 .reset-td-br-2 .reset-td-br-3  .reset-td-br-4}

{% alert tip %}
The `campaign_id` for API campaigns can be found on the Developer Console page and the campaign details page within your dashboard; or you can use the [Campaign List Endpoint](#campaign-list-endpoint).
{% endalert %}

### Example URL
`https://rest.iad-01.braze.com/campaigns/data_series?api_key=75480f9a-4db8-4057-8b7e-4d59bfd73709&campaign_id=3bbc4555-8fa0-4c9b-a5c0-4505edf3e064&length=7&ending_at=2014-12-10T23:59:59-05:00`

### Responses

#### Multi-Channel Response

```json
Content-Type: application/json
{
    "message": (required, string) the status of the export, returns 'success' when completed without errors,
    "data" : [
        {
            "time" : (string) date as ISO 8601 date,
            "messages" : {
                "ios_push" : [
                    {
                      "variation_name": "iOS_Push",
                      "sent" : (int),
                      "direct_opens" : (int),
                      "total_opens" : (int),
                      "bounces" : (int),
                      "body_clicks" : (int)
                      "revenue": 0,
                      "unique_recipients": 1,
                      "conversions": 0,
                      "conversions_by_send_time": 0,
                      "conversions1": 0,
                      "conversions1_by_send_time": 0,
                      "conversions2": 0,
                      "conversions2_by_send_time": 0,
                      "conversions3": 0,
                      "conversions3_by_send_time": 0,
                      "carousel_slide_[NUM]_[TITLE]_click": (optional, int),
                      "notif_button_[NUM]_[TITLE]_click": (optional, int)
                    }
                ],
                "android_push" : [
                    {
                      "sent" : (int),
                      "direct_opens" : (int),
                      "total_opens" : (int),
                      "bounces" : (int),
                      "body_clicks" : (int)
                    }
                ],
                "webhook": [
                    {
                      "sent": (int),
                      "errors": (int)
                    }
                ],
                "email" : [
                    {
                      "sent": (int),
                      "opens": (int),
                      "unique_opens": (int),
                      "clicks": (int),
                      "unique_clicks": (int),
                      "unsubscribes": (int),
                      "bounces": (int),
                      "delivered": (int),
                      "reported_spam": (int)
                    }
                ],
                "sms" : [
                  {
                    "sent": (int),
                    "delivered": (int),
                    "undelivered": (int),
                    "delivery_failed": (int)
                  }
                ]
              },
           "conversions_by_send_time": (optional, int),
           "conversions1_by_send_time": (optional, int),
           "conversions2_by_send_time": (optional, int),
           "conversions3_by_send_time": (optional, int),
           "conversions": (int),
           "conversions1": (optional, int),
           "conversions2": (optional, int),
           "conversions3": (optional, int),
           "unique_recipients": (int),
           "revenue": (optional, float)
        },
        ...
    ],
    ...
}
```

#### Multivariate Response

```json
Content-Type: application/json
{
    "data" : [
        {
            "time" : (string) date as ISO 8601 date,
            "conversions" : (int),
            "revenue": (float),
            "conversions_by_send_time": (int),
            "messages" : {
               "trigger_in_app_message": [{
      				"variation_name": (optional, string),
      				"impressions": (int),
      				"clicks": (int),
      				"first_button_clicks": (int),
      				"second_button_clicks": (int),
      				"revenue": (optional, float),,
      				"unique_recipients": (int),
      				"conversions": (optional, int),
      				"conversions_by_send_time": (optional, int),
      				"conversions1": (optional, int),
      				"conversions1_by_send_time": (optional, int),
      				"conversions2": (optional, int),
      				"conversions2_by_send_time": (optional, int),
      				"conversions3": (optional, int),
      				"conversions3_by_send_time": (optional, int)
      			}, {
      				"variation_name": (optional, string),
      				"impressions": (int),
      				"clicks": (int),
      				"first_button_clicks": (int),
      				"second_button_clicks": (int),
      				"revenue": (optional, float),,
      				"unique_recipients": (int),
      				"conversions": (optional, int),
      				"conversions_by_send_time": (optional, int),
      				"conversions1": (optional, int),
      				"conversions1_by_send_time": (optional, int),
      				"conversions2": (optional, int),
      				"conversions2_by_send_time": (optional, int),
      				"conversions3": (optional, int).
      				"conversions3_by_send_time": (optional, int)
      			}, {
      				"variation_name": (optional, string),
      				"revenue": (optional, float),,
      				"unique_recipients": (int),
      				"conversions": (optional, int),
      				"conversions_by_send_time": (optional, int),
      				"conversions1": (optional, int),
      				"conversions1_by_send_time": (optional, int),
      				"conversions2": (optional, int),
      				"conversions2_by_send_time": (optional, int),
      				"conversions3": (optional, int),
      				"conversions3_by_send_time": (optional, int),
      				"enrolled": (optional, int)
      			}]
      		},
      		"conversions_by_send_time": (optional, int),
      		"conversions1_by_send_time": (optional, int),
      		"conversions2_by_send_time": (optional, int),
      		"conversions3_by_send_time": (optional, int),
      		"conversions": (optional, int,
      		"conversions1": (optional, int),
      		"conversions2": (optional, int),
      		"conversions3": (optional, int),
      		"unique_recipients": (int),
      		"revenue": (optional, float)
         }],
         ...
}
```

Possible message types are `email`, `in_app_message`, `webhook`, `android_push`, `apple_push`, `kindle_push`, `web_push`, `windows_phone8_push`, and `windows_universal_push`. All push message types will have the same statistics shown for `android_push` above.

{% endapi %}
