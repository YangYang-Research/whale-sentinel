# Whale Sentinel Profile Specification

## Whale Sentinel Service Profile

### ws-common-attack-detection

| Group   | Configuration         | Value(s)      | Type    | M/O | Description                                                         |
|---------|------------------------|----------------|---------|-----|---------------------------------------------------------------------|
| –       | `xss_patterns`         | array of regex | string  | M   | List of regular expressions to match potential XSS attack patterns. |
| –       | `sql_patterns`         | array of regex | string  | M   | List of regular expressions to detect SQL Injection attempts.       |
| –       | `http_verb_patterns`   | regex string   | string  | M   | Pattern to match uncommon or manipulated HTTP methods.              |
| –       | `max_size_request`     | number         | number  | M   | Maximum allowed request content size (in bytes).                    |
| –       | `patching_patterns`    | array of regex | string  | M   | Regular expressions for detecting potential 0-day patching attempts.|

## Notes

- **Group**: Indicates the functional scope of each pattern. A blank `Group` implies general pattern configuration.
- **M/O**:  
  - `M` = Mandatory  
  - `O` = Optional  
- **Type**:
  - `string`: single text value or regex pattern  
  - `array`: list of strings  
  - `number`: numerical threshold or limit

- Example ws-common-attack-detection profile

```
{
  "profile": {
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

## Whale Sentinel Agent Profile

| Group                               | Configuration                       | Value(s)                                     | Type    | M/O | Description                                                                 |
|------------------------------------|-------------------------------------|----------------------------------------------|---------|-----|-----------------------------------------------------------------------------|
| –                                  | `running_mode`                      | `lite` / `monitor` / `protect`               | string  | M   | Current execution mode of the agent.                                        |
| –                                  | `last_run_mode`                     | `lite` / `monitor` / `protect`               | string  | M   | The previous execution mode before the current session.                    |
| `ws_module_web_attack_detection`   | `enable`                            | `true` / `false`                             | boolean | M   | Enable or disable the Web Attack Detection module.                          |
| `ws_module_web_attack_detection`   | `detect_header`                     | `true` / `false`                             | boolean | M   | Include request headers in detection (default is body and parameters only). |
| `ws_module_web_attack_detection`   | `threshold`                         | `number`                                     | number | M   | Acceptance threshold of prediction |
| `ws_module_dga_detection`          | `enable`                            | `true` / `false`                             | boolean | M   | Enable or disable the DGA (Domain Generation Algorithm) detection module.   |
| `ws_module_dga_detection`          | `enable`                            | `true` / `false`                             | boolean | M   | Enable or disable the DGA (Domain Generation Algorithm) detection module.   |
| `ws_module_common_attack_detection`| `enable`                            | `number`                                     | boolean | M   | Acceptance threshold of prediction.                       |
| `ws_module_common_attack_detection`| `detect_cross_site_scripting`       | `true` / `false`                             | boolean | M   | Enable detection of Cross-Site Scripting (XSS) attacks.                     |
| `ws_module_common_attack_detection`| `detect_http_large_request`         | `true` / `false`                             | boolean | M   | Enable detection of HTTP requests with abnormal large payloads.             |
| `ws_module_common_attack_detection`| `detect_sql_injection`              | `true` / `false`                             | boolean | M   | Enable detection of SQL Injection attacks.                                  |
| `ws_module_common_attack_detection`| `detect_http_verb_tampering`        | `true` / `false`                             | boolean | M   | Enable detection of non-standard or manipulated HTTP methods.               |
| –                                  | `lite_mode_data_is_synchronized`    | `true` / `false`                             | boolean | M   | Indicates whether data in lite mode is currently synchronized.              |
| –                                  | `lite_mode_data_synchronize_status` | `success` / `progress` / `fail`              | string  | M   | Synchronization progress status for lite mode data.                         |
| `secure_response_headers`           | `enable`                            | `true` / `false`                             | boolean | M   | Enable or disable automatic secure HTTP response header injection.          |
| `secure_response_headers`           | `headers`                           | key-value object                             | object  | M   | Full configuration of secure response headers to be applied dynamically.    |

## Notes

- **Group**: Identifies which module or section the configuration belongs to. A blank `Group` indicates general agent-level configuration.
- **M/O**:  
  - `M` = Mandatory  
  - `O` = Optional  
- **Type**: Standard JSON types.

- Example Agent Profile
 
```
{
  "profile": {
    "running_mode": "monitor",
    "last_run_mode": "lite",
    "lite_mode_data_is_synchronized": false,
    "lite_mode_data_synchronize_status": "fail",
    "ws_module_web_attack_detection": {
      "enable": true,
      "detect_header": false,
      "threshold": 80
    },
    "ws_module_dga_detection": {
      "enable": true,
      "threshold": 80
    },
    "ws_module_common_attack_detection": {
      "enable": true,
      "detect_cross_site_scripting": true,
      "detect_http_large_request": true,
      "detect_sql_injection": true,
      "detect_http_verb_tampering": true
    },
    "secure_response_headers": {
      "enable": true,
      "headers": {
        "Server": "Whale Sentinel",
        "X-Whale-Sentinel": "1",
        "Referrer-Policy": "no-referrer-when-downgrade",
        "X-Content-Type-Options": "nosniff",
        "X-XSS-Protection": "1; mode=block",
        "X-Frame-Options": "SAMEORIGIN",
        "Strict-Transport-Security": "max-age=31536000; includeSubDomains; preload",
        "X-Permitted-Cross-Domain-Policies": "none",
        "Expect-CT": "enforce; max-age=31536000",
        "Feature-Policy": "fullscreen 'self'",
        "Cache-Control": "no-cache, no-store, must-revalidate",
        "Pragma": "no-cache",
        "Expires": "0",
        "X-UA-Compatible": "IE=Edge,chrome=1",
        "X-Gemini-HTTP-Allow": "GET, POST",
        "Access-Control-Allow-Origin": "*",
        "Access-Control-Allow-Methods": "GET, POST",
        "Access-Control-Allow-Credentials": "true",
        "Access-Control-Allow-Headers": "Content-Type, Authorization"
      }
    }
  }
}
```