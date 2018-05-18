# manager-api-controller    
## 1.POST /manage/accounts/transfer   
 1.返回的实体类   
```html  
public class SpotAccount {
    private long id;

	private long userId;

	private String currency;

	private AccountType type;

	private BigDecimal balance;

	private long createdAt;

	private long updatedAt;

	private long version;

}
```  
 2.调用过程（其中100003是变量fromUserId,100004是变量toUserId，BTC是变量currency，FlowType.ASSET_REWARD是变量flowType，10是变量amount）
```html 
    Map<String, Object> data = MapUtil.of("fromUserId", "100003", "toUserId", "100004", "currency", "BTC",
            "flowType", FlowType.ASSET_REWARD, "amount", 10);
    Map<String, SpotAccount> result = restClient.post(new TypeReference<Map<String, SpotAccount>>() {
    }, "/manage/accounts/transfer", data);
``` 
 ## 2.POST /manage/deposits/{currency}/rules   问题：如果amount不是0会报异常信息：{"error":"PARAMETER_INVALID","data":"rules","message":"Must define a rule which amount is zero."}    
 1.返回的实体类   
```html  
    public class ConfirmRulesBean {

		public List<ConfirmRuleBean> rules;
	}

	public class ConfirmRuleBean {

		public BigDecimal amount;

		public int confirms;
	}
```  
 2.调用过程（其中rules是前台传过来的对象）
```html 
    ConfirmRulesBean rules = new ConfirmRulesBean();
    List<ConfirmRuleBean> list = new ArrayList<>();
    ConfirmRuleBean bean = new ConfirmRuleBean();
    bean.amount=new BigDecimal(0);
    bean.confirms=8;
    list.add(bean);
    rules.rules = list;
    Map<String, Integer> result = restClient.post(new TypeReference<Map<String, Integer>>() {
    }, "/manage/deposits/"+"BTC"+"/rules", rules);
``` 
## 3.POST /manage/deposits/{id}/audit/{approved}  调不通    
 
## 4.GET /manage/feeRates/default   
 1.返回的实体类   
```html  
    public class LevelFeeRates{
		public BigDecimal makerFeeRate;
		public BigDecimal takerFeeRate;
	}
```  
 2.调用过程
```html 
 	LevelFeeRates result = restClient.get(LevelFeeRates.class, "/manage/feeRates/default", null);
``` 

## 5.GET /manage/feeRates/level  有值的但是没有查出东西？===={"makerFeeRate":null,"takerFeeRate":null}   
 1.返回的实体类   
```html  
    public class LevelFeeRates{
		public BigDecimal makerFeeRate;
		public BigDecimal takerFeeRate;
	}
```  
 2.调用过程
```html 
 	LevelFeeRates result = restClient.get(LevelFeeRates.class, "/manage/feeRates/level", null);
``` 

## 6.POST /manage/feeRates/level  开始时间必须大于20min？TakerFeeRate大于0.1抛异常Fee rate 0.1499 is greater than allowed maximum fee: 0.1。MakerFeeRate大于0.1抛异常：Fee rate 0.1499 is greater than allowed maximum fee: 0.1  
 1.返回的实体类   
```html  
   public class FeeRates{
   		public Long id;
   		public int level;
   		public Long startTime;
   		public Long createdAt;
   		public BigDecimal makerFeeRate;
   		public BigDecimal takerFeeRate;
   	}
```  
 2.调用过程(其中feeRates是前端传过来的参数对象)
```html 
 	FeeRates feeRates = new FeeRates();
    feeRates.setLevel(8);
    feeRates.setStartTime(15266321211113L);  //2019-05-18 16:28:41
    feeRates.setMakerFeeRate(new BigDecimal(0.1));
    feeRates.setTakerFeeRate(new BigDecimal(0.1));
    FeeRates result = restClient.post(FeeRates.class, "/manage/feeRates/level", feeRates);
``` 
## 7.POST /manage/feeRates/level/{id}/delete   
 1.调用过程（其中100004是feeRates的ID）
```html 
 	Map<String, Boolean> result = restClient.post(new TypeReference<Map<String, Boolean>>() {}, "/manage/feeRates/level/"+100004+"/delete", null);
``` 

## 8.GET /manage/feeRates/symbol   有值的但是没有查出东西？ {"createdAt":null,"id":null,"makerFeeRate":null,"startTime":null,"symbol":null,"takerFeeRate":null}  
1.返回的实体类   
```html  
 public class SymbolFeeRates{
    private Long createdAt;
    private Long id;
    private BigDecimal makerFeeRate;
    private Long startTime;
    private String symbol;
    private BigDecimal takerFeeRate;
 	}
```  
 2.调用过程(其中feeRates是前端传过来的参数对象)
```html 
 	SymbolFeeRates result = restClient.get(SymbolFeeRates.class, "/manage/feeRates/symbol", null);
``` 

## 9.POST /manage/feeRates/symbol 开始时间必须大于20min？TakerFeeRate大于0.1抛异常Fee rate 0.1499 is greater than allowed maximum fee: 0.1。MakerFeeRate大于0.1抛异常：Fee rate 0.1499 is greater than allowed maximum fee: 0.1 
 1.返回的实体类   
```html  
参考8的返回对象
```  
 2.调用过程（其中feeRates是前端传来的参数对象）
```html 
 	SymbolFeeRates feeRates = new SymbolFeeRates();
    feeRates.setSymbol("BTC_USD");
    feeRates.setStartTime(15266321211113L);  //2019-05-18 16:28:41
    feeRates.setMakerFeeRate(new BigDecimal(0.1));
    feeRates.setTakerFeeRate(new BigDecimal(0.1));
    SymbolFeeRates result = restClient.post(SymbolFeeRates.class, "/manage/feeRates/symbol", feeRates);
``` 

## 10.POST /manage/feeRates/symbol/{id}/delete
 1.调用过程（其中100000是symbolfeeRates的ID）
```html 
 	Map<String, Boolean> result = restClient.post(new TypeReference<Map<String, Boolean>>() {}, "/manage/feeRates/symbol/"+100000+"/delete", null);
``` 

## 11.GET /manage/feeRates/user 有值的但是没有查出东西？{"id":null,"createdAt":null,"makerFeeRate":null,"startTime":null,"takerFeeRate":null,"userId":null}
 1.返回的实体类   
```html  
	public class UserFeeRates{
        private Long id ;
        private Long createdAt;
        private BigDecimal makerFeeRate;
        private Long startTime;
        private BigDecimal takerFeeRate;
        private Long userId;
    	}
```  
 2.调用过程
```html 
 	UserFeeRates result = restClient.get(UserFeeRates.class, "/manage/feeRates/user", null);
``` 

## 12.POST /manage/feeRates/user 开始时间必须大于20min？TakerFeeRate大于0.1抛异常Fee rate 0.1499 is greater than allowed maximum fee: 0.1。MakerFeeRate大于0.1抛异常：Fee rate 0.1499 is greater than allowed maximum fee: 0.1
 1.返回的实体类   
```html  
返回对象参考11
```  
 2.调用过程（其中feeRates是前端返回的对象）
```html 
 	UserFeeRates feeRates = new UserFeeRates();
    feeRates.setUserId(100003L);
    feeRates.setStartTime(15266321211113L);  //2019-05-18 16:28:41
    feeRates.setMakerFeeRate(new BigDecimal(0.1));
    feeRates.setTakerFeeRate(new BigDecimal(0.1));
    UserFeeRates result = restClient.post(UserFeeRates.class, "/manage/feeRates/user", feeRates);
``` 

## 13.POST /manage/feeRates/user/{id}/delete
 1.调用过程(其中100000是userfeeRates的ID)
```html 
 	Map<String, Boolean> result = restClient.post(new TypeReference<Map<String, Boolean>>() {}, "/manage/feeRates/user/"+100000+"/delete", null);
``` 

## 14.POST /manage/orders/{orderId}/cancel
 1.返回的实体类   
```html  
public class MatchOrders
	{
		private BigDecimal amount;
		private Long createdAt;
		private int features;
		private BigDecimal fee;
		private BigDecimal filledAmount;
		private Long id;
		private BigDecimal price;
		private Long refOrderId;
		private Long refSeqId;
		private Long seqId;
		private String status;
		private String symbol;
		private BigDecimal triggerOn;
		private String type;
		private Long updatedAt;
		private Long userId;
		private Long version;
	}

```  
 2.调用过程（其中100071是orderId）
```html 
 	MatchOrders result = restClient.post(MatchOrders.class, "/manage/orders/" + 100071 + "/cancel", null);
``` 


## 15.POST /manage/users/enable
 1.返回的实体类   
```html  
public class Users {
     private Long userId;
     private boolean canSignin;
     private boolean canTrade;
     private boolean canWithdraw;
     private Long createdAt;
     private Long id;
     private Integer level;
     private String type;
     private Long updatedAt;
}
```  
 2.调用过程（其中users是前端返回的对象）
```html 
    Users users = new Users();
    users.setCanSignin(true);
    users.setCanTrade(true);
    users.setCanWithdraw(true);
    users.setUserId(100004L);
    Users result = restClient.post(Users.class, "/manage/users/enable",users);
``` 

## 16.POST /manage/users/{userId}/{currency}/frozen/fix 接口调不通

## 17.GET /manage/{currency}/deposit/rules
 1.返回的实体类   
```html  
public class ConfirmRuleBean {

		public BigDecimal amount;

		public int confirms;
	}
```  
 2.调用过程(其中BTC是参数)
```html 
ConfirmRuleBean result = restClient.get(ConfirmRuleBean.class, "/manage/" + "BTC" + "/deposit/rules", null);
``` 

## 18.POST /manage/{currency}/withdraw/rules
 1.返回的实体类   
```html  
public class WithdrawRule
	{
        private Long createdAt;
        private String currency;
        private BigDecimal feeRate;
        private Long id;
        private BigDecimal maximumFee;
        private BigDecimal minimumAmount;
        private BigDecimal minimumFee;
        private boolean withdrawDisabled;
	}
```  
 2.调用过程(其中BTC是参数,withdrawRule也是参数)
```html 
    WithdrawRule withdra .,  wRule = new WithdrawRule();
    withdrawRule.setFeeRate(new BigDecimal(0.1));
    withdrawRule.setMaximumFee(new BigDecimal(10));
    withdrawRule.setMinimumAmount(new BigDecimal(10));
    withdrawRule.setMinimumFee(new BigDecimal(8));
    withdrawRule.setWithdrawDisabled(true);
    WithdrawRule result = restClient.post(WithdrawRule.class, "/manage/" + "BTC" + "/withdraw/rules", withdrawRule);
``` 