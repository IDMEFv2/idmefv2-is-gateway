# idmefv2-is-gateway

This project provides code and testing functionality to deploy a **secure gateway** for **IDMEFv2 transmission**.
It includes both a **Gateway Receiver** and a **Gateway Sender**, each with configuration and test utilities.

---

## 📦 Prerequisites

* Docker and Docker Compose installed
* Access to the project repository
* Example IDMEFv2 JSON file (`test_idmefv2.json`) for local testing

---

## 🚀 Deployment

### 1. Deploy the Gateway Receiver

```bash
docker compose -f ./docker-compose-receiver.yml up
```

**Test the Receiver locally:**

```bash
curl -X POST -sSv http://localhost:10081/topics/my_processed \
     -H "Content-Type: application/json" \
     --data @./test_idmefv2.json
```

---

### 2. Deploy the Gateway Sender

```bash
docker compose -f ./docker-compose-sender.yml up
```

**Test the Sender locally:**

```bash
curl -X POST -sSv http://localhost:10081/topics/my_processed \
     -H "Content-Type: application/json" \
     --data @./test_idmefv2.json
```

---

## ⚙️ Configuration

The configuration files for both the **Gateway Sender** and **Gateway Receiver** are located in is-gateway/config

### Example: Gateway Sender filtering configuration

You can customize the filtering rules. For instance, modify the `OrganisationName` field:

```json
"filterConfig": {
  "OrganisationName": "SOC3",
  "CreateTime": "",
  "StartTime": "",
  "Cause": ""
}
```

---

## 📝 Example Full Configuration

Below is an example configuration file (`sender.properties`):

```json
{
  "provider_reason": "compliance",
  "intended_use": "alert_gathering",
  "data_usage_policies": {
    "use_until": "2024-12-12",
    "use_after": "2024-09-12",
    "share_further": "false"
  },
  "data_sender_SIEM_brand": "Example Company A",
  "data_sender_SIEM_version": "Version 0.1",
  "IDMEFv2_attributes": {
    "attributes_to_transmit": [],
    "attributes_to_neglect": [],
    "attributes_to_anonymize": [],
    "attributes_to_pseudonemize": []
  },
  "sending_mode": "",
  "encryption_requirements": [],
  "authentication_requirements": [],
  "connection_requirements": [],
  "filterConfig": {
    "OrganisationName": "SOC3",
    "CreateTime": "",
    "StartTime": "",
    "Cause": ""
  },
  "enrichmentConfig": {
    "CreateTime": "",
    "StartTime": ""
  }
}
```

---

## 📖 Notes

* The **Gateway Receiver** listens on port `10081` by default.
* The **Gateway Sender** can be configured with filtering and enrichment policies.
* Filtering rules allow you to keep, drop, or override specific IDMEFv2 attributes.
* Enrichment rules let you add or modify metadata before forwarding.

---
