## Overview

This use case demonstrates how Splunk can be used to analyze DNS logs
in order to identify internal hosts generating a high volume of DNS queries.

## Objective

Detect abnormal behavior such as:

- Overactive internal hosts
- Automated activity
- Potential DNS beaconing

## Data Source

- DNS logs (JSON format)
- Splunk Enterprise

## SPL Query

```spl
source="dns_logs.json" host="DESKTOP-INIT9SK" sourcetype="_json"
| stats count by id.orig_h
| sort -count
| head 10
```
