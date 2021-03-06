# manager-api-controller   

## 1.POST /manage/accounts/freeze   
 1.返回的实体类   
```html  
public class AccountsFreeze
	{
		private BigDecimal amount;
		private String currency;
		private String flowType;
		private Long userId;
	}
```  
 2.调用过程（其中AccountsFreeze是前端传过来的参数对象）
```html 
    AccountsFreeze accountsFreeze = new AccountsFreeze();
    accountsFreeze.setAmount(new BigDecimal(5));
    accountsFreeze.setCurrency("BTC");
    accountsFreeze.setFlowType("TRADE_FREEZE");
    accountsFreeze.setUserId(100003L);
    Map<String, BigDecimal> result = restClient.post(new TypeReference<Map<String, BigDecimal>>() {
           }, "/manage/accounts/freeze", accountsFreeze);
``` 
## 2.POST /manage/accounts/transfer   
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
## 3.POST /manage/accounts/unfreeze   
 1.返回的实体类   
```html  
public class AccountsFreeze
	{
		private BigDecimal amount;
		private String currency;
		private String flowType;
		private Long userId;
	}
```  
 2.调用过程（其中AccountsFreeze是前端传过来的参数对象）
```html 
   		AccountsFreeze accountsFreeze = new AccountsFreeze();
   		accountsFreeze.setAmount(new BigDecimal(3));
   		accountsFreeze.setCurrency("BTC");
   		accountsFreeze.setFlowType("TRADE_UNFREEZE");
   		accountsFreeze.setUserId(100003L);
   		Map<String, BigDecimal> result = restClient.post(new TypeReference<Map<String, SpotAccount>>() {
                }, "/manage/accounts/unfreeze", accountsFreeze);
``` 
 ## 4.POST /manage/deposits/{currency}/rules     
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
## 5.POST /manage/deposits/{id}/audit/{approved}  充值相关   
 
## 6.GET /manage/exists
 1.调用过程（其中uniqueId是前台传过来的参数）
```html 
    Map<String, String> query = new HashMap<>();
    query.put("uniqueId","0000000000640e87ecc00611456fa97c949b93ed326e");
    Boolean result = restClient.get(Boolean.class, "/manage/exists", query);
``` 
## 7.GET /manage/feeRates/default   
 1.返回的实体类   
```html  
    public class FeeRates{
		public BigDecimal makerFeeRate;
		public BigDecimal takerFeeRate;
	}
```  
 2.调用过程
```html 
 	FeeRates result = restClient.get(FeeRates.class, "/manage/feeRates/default", null);
``` 

## 8.GET /manage/feeRates/level  
 1.返回的实体类   
```html  
    public class LevelFeeRates{
		public Long id;
        public int level;
        public Long startTime;
        public Long createdAt;
        public BigDecimal makerFeeRate;
        public BigDecimal takerFeeRate;
	}
```  
 2.调用过程
```html 
 	Map<String, List<LevelFeeRates>> result = restClient.get(new TypeReference<Map<String, List<LevelFeeRates>>>() {
                                                             		}, "/manage/feeRates/level", null);
``` 

## 9.POST /manage/feeRates/level    
 1.返回的实体类   
```html  
   public class LevelFeeRates{
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
 	LevelFeeRates feeRates = new LevelFeeRates();
    feeRates.setLevel(8);
    feeRates.setStartTime(15266321211113L);  //2019-05-18 16:28:41
    feeRates.setMakerFeeRate(new BigDecimal(0.1));
    feeRates.setTakerFeeRate(new BigDecimal(0.1));
    LevelFeeRates result = restClient.post(LevelFeeRates.class, "/manage/feeRates/level", feeRates);
``` 
## 10.POST /manage/feeRates/level/{id}/delete   
 1.调用过程（其中100004是feeRates的ID）
```html 
 	Map<String, Boolean> result = restClient.post(new TypeReference<Map<String, Boolean>>() {}, "/manage/feeRates/level/"+100004+"/delete", null);
``` 

## 11.GET /manage/feeRates/symbol   
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
 	Map<String, List<SymbolFeeRates>> result = restClient.get(new TypeReference<Map<String, List<SymbolFeeRates>>>() {
 	}, "/manage/feeRates/symbol", null);
``` 

## 12.POST /manage/feeRates/symbol  
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

## 13.POST /manage/feeRates/symbol/{id}/delete
 1.调用过程（其中100000是symbolfeeRates的ID）
```html 
 	Map<String, Boolean> result = restClient.post(new TypeReference<Map<String, Boolean>>() {}, "/manage/feeRates/symbol/"+100000+"/delete", null);
``` 

## 14.GET /manage/feeRates/user 
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
 	Map<String, List<UserFeeRates>> result = restClient.get(new TypeReference<Map<String, List<UserFeeRates>>>() {
 	}, "/manage/feeRates/user", null);
``` 

## 15.POST /manage/feeRates/user 
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

## 16.POST /manage/feeRates/user/{id}/delete
 1.调用过程(其中100000是userfeeRates的ID)
```html 
 	Map<String, Boolean> result = restClient.post(new TypeReference<Map<String, Boolean>>() {}, "/manage/feeRates/user/"+100000+"/delete", null);
``` 

## 17.POST /manage/orders/{orderId}/cancel
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

## 18.POST /manage/users/enable
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

## 19.GET /manage/{currency}/deposit/rules
 1.返回的实体类   
```html  
public class ConfirmRuleBean {

		public BigDecimal amount;

		public int confirms;
	}
```  
 2.调用过程(其中BTC是参数)
```html 
Map<String, List<ConfirmRuleBean>> result = restClient.get(new TypeReference<Map<String, List<ConfirmRuleBean>>>() {}, "/manage/" + "BTC" + "/deposit/rules", null);
``` 

## 20.POST /manage/{currency}/withdraw/rules
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
    WithdrawRule withdrawRule = new WithdrawRule();
    withdrawRule.setFeeRate(new BigDecimal(0.1));
    withdrawRule.setMaximumFee(new BigDecimal(10));
    withdrawRule.setMinimumAmount(new BigDecimal(10));
    withdrawRule.setMinimumFee(new BigDecimal(8));
    withdrawRule.setWithdrawDisabled(true);
    WithdrawRule result = restClient.post(WithdrawRule.class, "/manage/" + "BTC" + "/withdraw/rules", withdrawRule);
``` 

## 21.GET /manage/users/{userId}/accounts/{currency}
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
 2.调用过程(其中100003是参数用户ID，BTC是参数)
```html 
    Map<String, List<SpotAccount>> result = restClient.get(new TypeReference<Map<String, List<SpotAccount>>>() {
    		},"/manage/users/100003/accounts/BTC", null);
``` 