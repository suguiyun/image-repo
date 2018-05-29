# trade-api-controller   

## 1.GET /v1/trade/orders  
 1.返回的实体类   
```html  
{
"orders": [
{
"id": 100162,
"createdAt": 1527576877832,
"updatedAt": 1527576877837,
"seqId": 163,
"refOrderId": 0,
"refSeqId": 0,
"userId": 100003,
"symbol": "BTC_USD",
"type": "BUY_LIMIT",
"price": 1.0000000000000000,
"amount": 1.0000000000000000,
"filledAmount": 0E-16,
"fee": 0E-16,
"triggerOn": 0E-16,
"features": 0,
"status": "SEQUENCED"
},
{
"id": 100160,
"createdAt": 1527510220458,
"updatedAt": 1527512215841,
"seqId": 161,
"refOrderId": 0,
"refSeqId": 0,
"userId": 100003,
"symbol": "BTC_USD",
"type": "BUY_LIMIT",
"price": 1.0000000000000000,
"amount": 1.0000000000000000,
"filledAmount": 0E-16,
"fee": 0E-16,
"triggerOn": 0E-16,
"features": 0,
"status": "FULLY_CANCELLED"
},
{
"id": 100159,
"createdAt": 1527510215774,
"updatedAt": 1527510215779,
"seqId": 160,
"refOrderId": 0,
"refSeqId": 0,
"userId": 100003,
"symbol": "BTC_USD",
"type": "BUY_LIMIT",
"price": 1.0000000000000000,
"amount": 1.0000000000000000,
"filledAmount": 0E-16,
"fee": 0E-16,
"triggerOn": 0E-16,
"features": 0,
"status": "SEQUENCED"
}
]}
```  
 2.调用过程
```html 
    httpResponse = proxyClient.request2(auth == null ? null : auth.authorization, ip,
    	request.getMethod(), "/v1/trade/orders", request.getQueryString(), body);
``` 
## 3.GET /v1/trade/orders/{orderId}
 1.返回的实体类   
```html  
{
"id": 100162,
"createdAt": 1527576877832,
"updatedAt": 1527576877837,
"seqId": 163,
"refOrderId": 0,
"refSeqId": 0,
"userId": 100003,
"symbol": "BTC_USD",
"type": "BUY_LIMIT",
"price": 1.0000000000000000,
"amount": 1.0000000000000000,
"filledAmount": 0E-16,
"fee": 0E-16,
"triggerOn": 0E-16,
"features": 0,
"status": "SEQUENCED"
}
```  
 2.调用过程（其中100162是orderId）
```html 
    httpResponse = proxyClient.request2(auth == null ? null : auth.authorization, ip,
    						request.getMethod(), "/v1/trade/orders/100162", request.getQueryString(), body);
``` 
## 4.GET /v1/trade/orders/{orderId}/matches  
 1.返回的实体类   
```html  
{
"matches": [
{
"id": 100000,
"createdAt": 1527046182081,
"type": "TAKER",
"price": 1.0000000000000000,
"amount": 0.1000000000000000,
"fee": 0.0001000000000000
}
]
}
```  
 2.调用过程（其中100001是orderId）
```html 
   	httpResponse = proxyClient.request2(auth == null ? null : auth.authorization, ip,
        	request.getMethod(), "/v1/trade/orders/100001/matches", request.getQueryString(), body);
``` 