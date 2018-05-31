## 1.trade-api 请求：GET /v1/trade/orders  
```html 
1.查询条件：时间范围,订单类型（买入，卖出），订单状态（pending，Fully Cancelled，Partial Filled等），币种，币对，userId
``` 
 
## 2.ui-api  请求：GET /ui/users/{userId}/withdraw/requests  
```html  
 1.需要分页
 2.查询条件：币种（或者全部），时间范围，userId
``` 
## 3.ui-api  请求：GET /ui/users/{userId}/deposit/logs
```html 
  1.需要分页
  2.查询条件：币种（或者全部），时间范围,userId
``` 
 ## 4.ui-api  GET /ui/users/{userId}/withdraw/addresses
```html 
  1.需要分页 
``` 

## 5. 全部/充值/提现/买入/卖出/活动红包/系统赠送 这个需要各种类型综合查询还得带分页和查询条件
  
```html 
   1.查询条件：时间范围，币种
   2.分页
``` 