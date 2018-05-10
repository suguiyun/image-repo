# ui-api-controller    
 ## 1.GET /ui/deposit/{currency}/rules    
    
## 2.GET /ui/orders/{orderId}/refund    
  
## 3.POST /ui/users 省略..........    
 
## 4.GET /ui/users/{userId}   
 1.返回的实体类   
```html  
public class Users {

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
 2.调用过程（其中100003是用户变量ID）
```html 
 Users result = restClient.get(Users.class, "/ui/users/100003",null);
``` 
 ## 5.POST /ui/users/{userId}     
 1.返回的实体类   
```html  
public class Users {

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
 2.调用过程（其中100003是用户变量ID）
```html 
 	Users users = new Users();
 	users.setCanSignin(false);
 	users.setCanTrade(false);
 	users.setCanWithdraw(false);
 	Users result = restClient.post(Users.class, "/ui/users/100003",users);
``` 
## 6.GET /ui/users/{userId}/accounts    
 1.返回的实体类   
```html  
public class SpotAccountBean {
		public String currency;
		public String type;
		public BigDecimal balance;
	}
	static TypeReference<Map<String, List<SpotAccountBean>>> TYPE_SPOT_ACCOUNT_MAP = new TypeReference<Map<String, List<SpotAccountBean>>>() {
    	};
```  
 2.调用过程（其中id是用户变量,BTC是币种）
```html 
 	Map<String, List<SpotAccountBean>> result = restClient.get(TYPE_SPOT_ACCOUNT_MAP, "/ui/users/"+ id +"/accounts",
    				MapUtil.of("currency", "BTC"));
``` 
## 7.GET /ui/users/{userId}/apiKeys   
 1.返回的实体类   
```html  
public class ApiAuthKeyBean {

		public long id;

		public long createdAt;

		public long userId;

		public String apiKey;

		public String apiSecret;

		public String description;

		public int netAddress;

		public int netmask;

		public boolean canTrade;

		public boolean canWithdraw;

		public boolean enabled;

		public String getIpRestriction() {
			return IpUtil.getIPRestriction(this.netAddress, this.netmask);
		}
	}
```  
 2.调用过程（其中id是用户变量）
```html 
 	Map<String, List<ApiAuthKeyBean>> result = restClient.get(new TypeReference<Map<String, List<ApiAuthKeyBean>>>() {
    		}, "/ui/users/"+ id +"/apiKeys",null);
``` 

## 8.POST /ui/users/{userId}/apiKeys   
 1.返回的实体类   
```html  
public class AddApiKeyBean {
		public String description;
		public String ip;
		public boolean canTrade;
		public boolean canWithdraw;
		public AuthType authType;
		public String code;
	}
```  
 2.调用过程（其中id是用户变量,bean是前端传过来的变量）
```html 
 	AddApiKeyBean bean = new AddApiKeyBean();
    ApiAuthKeyBean apiKey = restClient.post(ApiAuthKeyBean.class, "/ui/users/" + id + "/apiKeys",
    				bean);
``` 

## 9.POST /ui/users/{userId}/apiKeys/{apiKey}/delete   
 1.调用过程（其中userId是用户变量,apiKey是变量）
```html 
 	restClient.post(new TypeReference<Map<String, Boolean>>() {
    			}, String.format("/ui/users/%s/apiKeys/%s/delete", userId, apiKey), null);
``` 
## 10.POST /ui/users/{userId}/apiKeys/{apiKey}/disable   
 1.调用过程（其中id是用户变量,AAAAAYajkw49S2wE6WmjpTVuhbl0DD7n是变量）
```html 
 	boolean result = restClient.post(boolean.class, "/ui/users/" + id + "/apiKeys/AAAAAYajkw49S2wE6WmjpTVuhbl0DD7n/disable",null);
``` 

## 11.POST /ui/users/{userId}/apiKeys/{apiKey}/enable   
 1.调用过程（其中id是用户变量,AAAAAYajkw49S2wE6WmjpTVuhbl0DD7n是变量）
```html 
 	boolean result = restClient.post(boolean.class, "/ui/users/" + id + "/apiKeys/AAAAAYajkw49S2wE6WmjpTVuhbl0DD7n/enable",null);
``` 

## 12.GET /ui/users/{userId}/deposit/logs 
 1.返回的实体类   
```html  
public class DepositLogBean {

		public long id;

		public String currency;

		public String toAddress;

		public String uniqueId;

		public BigDecimal amount;

		public int confirms;
		public int minimumConfirms;

		public boolean depositOk;
		public boolean depositCancelled;

		public long createdAt;
	}
	
	static TypeReference<Map<String, List<DepositLogBean>>> TYPE_DEPOSIT_MAP = new TypeReference<Map<String, List<DepositLogBean>>>() {
    	};
```  
 2.调用过程（其中id是用户变量,BTC是变量）
```html 
 	Map<String, List<DepositLogBean>> result = restClient.get(TYPE_DEPOSIT_MAP, "/ui/users/"+id+"/deposit/logs",
    				MapUtil.of("currency", "BTC"));
``` 

## 13.GET /ui/users/{userId}/deposit/{currency}/address 
 1.返回的实体类   
```html  
	public class AddressBean {
		public long id;
		public String currency;
		public String address;
		public String description;
		public long createdAt;
	}
```  
 2.调用过程（其中id是用户变量,BTC是变量）
```html 
 	AddressBean result = restClient.get(AddressBean.class, "/ui/users/"+id+"/deposit/BTC/address", null);
``` 