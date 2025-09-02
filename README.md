# idmefv2-is-gateway
This project provides code and testing functionality to create a secure gateway for idmefv2 transmission

Test receiver locally

```
curl -X POST -sSv http://localhost:10081/topics/my_processed -H "Content-Type: application/json" --data @./test_idmefv2.json 

```

Test sender locally
```
curl -X POST -sSv http://localhost:10082/topics/my_processed -H "Content-Type: application/json" --data @./test_idmefv2.json 

```
