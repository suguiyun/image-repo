# user-api-controller   

## 1.GET /v1/user/accounts   
 1.返回的实体类   
```html  
{
"accounts": [
{
"id": 100002,
"createdAt": 1527044984368,
"updatedAt": 1527510747645,
"userId": 100003,
"currency": "BTC",
"type": "SPOT_AVAILABLE",
"balance": -3.9257600000000000
},
{
"id": 100007,
"createdAt": 1527045391162,
"updatedAt": 1527510747645,
"userId": 100003,
"currency": "BTC",
"type": "SPOT_FROZEN",
"balance": 3.9100000000000000
},
{
"id": 100005,
"createdAt": 1527045008755,
"updatedAt": 1527576877831,
"userId": 100003,
"currency": "USD",
"type": "SPOT_AVAILABLE",
"balance": 0.9279000000000000
},
{
"id": 100006,
"createdAt": 1527045387214,
"updatedAt": 1527576877831,
"userId": 100003,
"currency": "USD",
"type": "SPOT_FROZEN",
"balance": 18.9800000000000000
}
]
}
```  
 2.调用过程
```html 
    httpResponse = proxyClient.request2(auth == null ? null : auth.authorization, ip,
    	request.getMethod(), "/v1/user/accounts", request.getQueryString(), body);
```  