# Whale Sentinel Configuration Design

## Whale Sentinel Service Configuration

### ws-common-attack-detection

| Group | Rule | Value | Type | M/O | Description | 
| ---------- | ---- | ----- | ---- | ----| ----------- |
| | xss_patterns | array | string | M | XSS pattern |
| | sql_patterns | array | string | M | XSS pattern |
| | http_verb_patterns | string | string | M | HTTP Verb Tampering pattern |
| | max_size_request | number | number | M | Max size of request content |
| | patching_patterns | array | string | M | patching pattern for 0day attack |

- Example ws-common-attack-detection configuration

```
{
  "rules": {
    "xss_patterns": [
      "(?:https?://|//)[^\\s/]+\\.js",
      "((%3C)|<)((%2F)|/)*[a-z0-9%]+((%3E)|>)",
      "((\\%3C)|<)((\\%69)|i|(\\%49))((\\%6D)|m|(\\%4D))((\\%67)|g|(\\%47))[^\n]+((\\%3E)|>)"
    ],
    "sql_patterns": [
      "(?:select\\s+.+\\s+from\\s+.+)",
      "(?:insert\\s+.+\\s+into\\s+.+)",
      "..."
    ],
    "http_verb_patterns": "(?i)(HEAD|OPTIONS|TRACE|CONNECT|PROPFIND|PROPPATCH|MKCOL|COPY|MOVE|LOCK|UNLOCK)",
    "max_size_request" : "2048",
    "patching_patterns: [
      "^(?!.*(\\.\\.|\\/\|\\\\)).*$"
    ]
  }
}
```

## Whale Sentinel Agent Configuration

| Group | Rule | Value | Type | M/O | Description | 
| ---------- | ---- | ----- | ---- | ----| ----------- |
| | running_mode | lite/monitor/protect | string | M | Current run mode of agent |
| | last_run_mode | lite/monitor/protect | string | M | Last run mode of agent |
| ws_module_web_attack_detection | enable | true/false | boolean | M | Enable/disable this rule |
| ws_module_web_attack_detection | detect_header | true/false | boolean | M | Default detect only request body & request params |
| ws_module_dga_detection | enable | true/false | boolean | M | Enable/disable this rule |
| ws_module_common_attack_detection | enable | true/false | boolean | M | Enable/disable this rule |
| ws_module_common_attack_detection | detect_cross_site_scripting | true/false | boolean | M | Enable/disable detect cross-site-scription attack |
| ws_module_common_attack_detection | detect_http_large_request | true/false | boolean | M | Enable/disable detect http large request |
| ws_module_common_attack_detection | detect_sql_injection | true/false | boolean | M | Enable/disable detect sql injection attack |
| ws_module_common_attack_detection | detect_http_verb_tampering | true/false | boolean | M | Enable/disable detect http ver tampering attack |
| | lite_mode_data_is_synchronized | true/false | boolean | M | Status of data is synchronize or not |
| | lite_mode_data_synchronize_status | success/progress/fail | string | M | Status of process synchronize is success or not |


- Example Agent Configuration
 
```
{
    "rules": {
        "running_mode": "monitor",
        "last_run_mode": "lite",
        "lite_mode_data_is_synchronized": false,
        "lite_mode_data_synchronize_status: "fail",
        "ws_module_web_attack_detection": {
            "enable": true,
            "detect_header": false
        },
        "ws_module_dga_detection": {
            "enable": true
        },
        "ws_module_common_attack_detection": {
            "enable": true,
            "detect_cross_site_scripting": true,
            "detect_http_large_request": true,
            "detect_sql_injection": true,
            "detect_http_verb_tampering": true
        }
    }
}
```