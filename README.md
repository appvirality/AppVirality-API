# AppVirality-API

AppVirality provides API feature to pull the reward details and redeem the rewards. AppVirality shall take care of reward distribution in case if the reward type is coupons (provided coupon availability in AppVirality dashboard), other than coupon case (i.e In-store Credits or Other) App owner has to take care of reward distribution and in such cases AppVirality shall provide the reward details and available balance for each referrer/friend.

AppVirality API is accessed via the https://api.appvirality.com domain. 
<br/><br/>
NOTE: All dates provided in API calls are in UTC±00 Time zone.

INDEX
----------------------
1. [Get Referrer Rewards](https://github.com/appvirality/AppVirality-API#1-get-referrer-rewards)
2. [Get Friend Rewards](https://github.com/appvirality/AppVirality-API#2-get-friend-rewards)
3. [Redeem Referrer Rewards](https://github.com/appvirality/AppVirality-API#3-redeem-referrer-rewards)
4. [Change Reward Status] (https://github.com/appvirality/AppVirality-API#4-change-reward-status)
5. [Redeem Friend Rewards] (https://github.com/appvirality/AppVirality-API#5-redeem-friend-rewards)
6. [Get Referrer/Friend Balance] (https://github.com/appvirality/AppVirality-API#6-get-referrerfriend-balance)
7. [Register Conversion Event] (https://github.com/appvirality/AppVirality-API#7-register-conversion-event)
8. [Update User details] (https://github.com/appvirality/AppVirality-API#8-update-user-details)
9. [Approve Dynamic Coupon] (https://github.com/appvirality/AppVirality-API#9-approve-dynamic-coupon)
10. [Check Reward Status] (https://github.com/appvirality/AppVirality-API#10-check-reward-status)
11. [Get AppUser Details] (https://github.com/appvirality/AppVirality-API#11-get-appuser-details)
12. [Get Campaign] (https://github.com/appvirality/AppVirality-API#12-get-campaign)
13. [Add Test Device] (https://github.com/appvirality/AppVirality-API#13-add-test-device)
14. [Reset Test Device] (https://github.com/appvirality/AppVirality-API#14-reset-test-device)


1. Get Referrer Rewards
----------------------

 Get the list of Referrer rewards

<b>Route</b>
<pre><code>POST /v1/getreferrerrewards

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>pagenum</b> — Number of the Page. 50 records per page.
* <b>fromdate</b> — Start date. Date format should be <b>d-MMM-yyyy H:m</b>, Timezone UTC±00 (Eg. 2-Feb-2015 2:13).
* <b>todate</b> — End date to filter rewards (Eg. 2-Feb-2015 14:3).
* <b>status</b> — This can be used to filter the Rewards. You can use "EligibleForReward" / "Rewarded" / "All" / "Suspicious" / "Rejected" / "Approved" / "UnderReview".

<b>Status:</b>

<b>UnderReview</b> — Rewards which does not met the review period.

<b>EligibleForReward</b> — Referrers list with Approved Rewards (i.e met with review period and redemption cap).

<b>Rewarded</b> — Rewards which are dispatched i.e. with the status "Rewarded".

<b>Suspicious</b> — Rewards marked as Suspicious i.e detected by fraud detection system.

<b>Rejected</b> — Rejected rewards i.e Suspicious rewards can be rejected.

<b>Approved</b> — Rewards Approved but not yet Rewarded.

<b>All</b> — Rewards with all the above status.

#####<b>Sample Input:</b>
```json
{
"apikey":"763502957c434314b613d42400ac7a7f",
"privatekey":"8a433343ee8241a10419212415496579",
"pagenum":"1",
"fromdate":null,
"todate":"2-Feb-2015 2:13",
"status":"EligibleForReward"
}
```  

#####<b>Response Parameters:</b>

* <b>participantid</b> —  Campaign Participant ID
* <b>emailid</b> — Email of the Referrer
* <b>name</b> — Name of the Referrer
* <b>userkey</b> — Unique key to identify App User
* <b>storeuserid</b> — This is the ID with which you recognize the user uniquely in your store.
* <b>campaignid</b> — Unique Campaign ID
* <b>campaignname</b> — Name of the Campaign
* <b>rewardid</b> — Reward ID, to Track the Reward and Distribution
* <b>reward_type</b> — Type of Reward (Coupon, InstoreCredits,Other)
* <b>rewarded_date</b> — Reward Initiated Date
* <b>amount</b> — amount of money to reward (null when non-monetary incentive is used)
* <b>reward_unit</b> — Currency Unit of the Reward
* <b>couponcode</b> — Coupon code dispatched to Referrer, as a reward. Only when the Reward type is coupon.
* <b>expires</b> — Coupon expiry date.
* <b>rewarddetails</b> — Rewards break down 
  * <b>rewarddtlid</b> — Reward detail ID
  * <b>amount</b> — amount of money to reward (null when non-monetary incentive is used)
  * <b>rewarded_date</b> — Reward Initiated Date
  * <b>status</b> — Status mentioned in the Query
  * <b>eventname</b> —  Install, Signup, Transaction & Any defined Custom Events
  * <b>friendEmail</b> —  Friend Email 
  * <b>friendStoreId</b> —  This is unique store user ID of friend
  * <b>extrainfo</b> —  Info provided during the Conversion Event. Data will be Uri encoded.
  * <b>status</b> —  Status of the reward.
* <b>totalrecords</b> —  The total number of records(individual rewards) available in the given date time range.

#####<b>Sample Response:</b>
```json
{
	"rewards": [{
		"participantid": "93700",
		"emailid": "refr4@gmail.com",
		"name": "refr4name",
		"userkey": "a4953b1e65744732b999d1af1815bf7e",
		"storeuserid": null,
		"campaignid": "216",
		"campaignname": "MySample",
		"eventname": null,
		"rewardid": "3325",
		"reward_type": "Coupon",
		"rewarded_date": "2-Mar-2015 0:2:29",
		"status": "All",
		"amount": "20",
		"reward_unit": "%24",
		"couponcode": "REFERRER10",
		"expires": "31-Mar-2015",
		"rewarddetails": [{
			"rewarddtlid": "790",
			"amount": "10",
			"rewarded_date": "1-Mar-2015 10:25:13",
			"eventname": "Install",
			"friendEmail": "frnd1@gmail.com",
			"friendStoreId": null,
			"extrainfo": null,
			"status": "UnderReview"
		}, {
			"rewarddtlid": "788",
			"amount": "10",
			"rewarded_date": "1-Mar-2015 8:13:34",
			"eventname": "Install",
			"friendEmail": "frnd2@gmail.com",
			"friendStoreId": null,
			"extrainfo": null,
			"status": "UnderReview"
		}]
	}, {
		"participantid": "93701",
		"emailid": "refr2@gmail.com",
		"name": "refr2name",
		"userkey": "114589373a2f458198bc617fc3d1f434",
		"storeuserid": null,
		"campaignid": "216",
		"campaignname": "MySample",
		"eventname": null,
		"rewardid": "0",
		"reward_type": "Coupon",
		"rewarded_date": null,
		"status": "All",
		"amount": "10",
		"reward_unit": "%24",
		"couponcode": null,
		"expires": null,
		"rewarddetails": [{
			"rewarddtlid": "789",
			"amount": "10",
			"rewarded_date": "1-Mar-2015 10:18:49",
			"eventname": "Install",
			"friendEmail": "frnd3@gmail.com",
			"friendStoreId": null,
			"extrainfo": null,
			"status": "UnderReview"
		}]
	}],
	"totalrecords": "2",
	"pagenum": "1"
}
```


2. Get Friend Rewards
----------------------

 Get the list of Friend rewards

<b>Route</b>
<pre><code>POST /v1/getfriendrewards

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>pagenum</b> — Number of the Page. 50 records per page.
* <b>fromdate</b> — Start date. Date format should be <b>d-MMM-yyyy H:m</b>, Timezone UTC±00 (Eg. 2-Feb-2015 2:13).
* <b>todate</b> — End date to filter rewards (Eg. 2-Feb-2015 14:3).
* <b>status</b> — This can be used to filter the Rewards. You can use "Rewarded" / "All" / "Suspicious" / "Rejected" / "Approved" / "UnderReview".

<b>Status:</b>

<b>UnderReview</b> — Rewards which does not met the review period.

<b>Rewarded</b> — Rewards which are dispatched i.e. with the status "Rewarded".

<b>Suspicious</b> — Rewards marked as Suspicious i.e detected by fraud detection system.

<b>Rejected</b> — Rejected rewards i.e Suspicious rewards can be rejected.

<b>Approved</b> — Rewards Approved but not yet Rewarded.

<b>All</b> — Rewards with all the above status.
#####<b>Sample Input:</b>
```json
{
"apikey":"763502957c434314b613d42400ac7a7f",
"privatekey":"8a433343ee8241a10419212415496579",
"pagenum":"1",
"fromdate":null,
"todate":"2-Feb-2015 2:13",
"status":"Approved"
}
```

#####<b>Response Parameters:</b>

* <b>participantid</b> —  Campaign Participant ID
* <b>emailid</b> — Email of the Friend
* <b>name</b> — Name of the Frined
* <b>userkey</b> — Unique key to identify App User
* <b>storeuserid</b> — This is the ID with which you recognize the user uniquely in your store.
* <b>campaignid</b> — Unique Campaign ID
* <b>campaignname</b> — Name of the Campaign
* <b>eventname</b> —  Install, Signup, Transaction & Any defined Custom Events
* <b>rewardid</b> — Reward ID , to Track the Reward and Distribution
* <b>reward_type</b> — Type of Reward (Coupon, InstoreCredits,Other)
* <b>rewarded_date</b> — Reward Initiated Date
* <b>status</b> — Rewarded / Suspicious / Approved / UnderReview / Rejected, lets you know state of reward.
* <b>amount</b> — amount of money to reward (null when non-monetary incentive is used)
* <b>reward_unit</b> — Currency Unit of the Reward
* <b>couponcode</b> — Coupon code dispatched to Friend as a reward. Only when the Reward type is coupon.
* <b>expires</b> — Coupon expiry date.
* <b>totalrecords</b> —  The total number of records(individual rewards) available in the given date time range.

#####<b>Sample Response:</b>
```json
{
"rewards":[
{
"participantid":"93705",
"emailid":"frnd1@gmail.com",
"name":"frnd1name",
"userkey":"114589373a2f458198bc617fc3d1f434",
"storeuserid":null,
"campaignid":"216",
"campaignname":"MySample",
"eventname":"Signup",
"rewardid":"3324",
"reward_type":"Coupon",
"rewarded_date":"1-Mar-2015 10:25:24",
"status":"Rewarded",
"amount":"5",
"reward_unit":"$",
"couponcode":"FRIEND5",
"expires":"31-Mar-2015",
"rewarddetails":null
},
{
"participantid":"93704",
"emailid":"frnd2@gmail.com",
"name":"frnd2name",
"userkey":"6eee2f4a10204423ac940f3e20b4f7db",
"storeuserid":null,
"campaignid":"216",
"campaignname":"MySample",
"eventname":"Signup",
"rewardid":"3323",
"reward_type":"Coupon",
"rewarded_date":"1-Mar-2015 10:19:30",
"status":"Approved",
"amount":"5",
"reward_unit":"$",
"couponcode":null,
"expires":null,
"rewarddetails":null
}
],
"totalrecords":"2",
"pagenum":"1"
}
```


3. Redeem Referrer Rewards
----------------------

This service call helps to redeem the referrer rewards in case of "In-store Credits" or "Other" type of rewards. No need to call this method if the reward type is coupon since AppVirality system will be distributing the coupons automatically. 

You can redeem the referrer reward by sending amount to be redeemed or you can send the list of "rewarddtlid" to redeem. The same amount will be deducted from referrer balance.

<b>Route</b>
<pre><code>POST /v1/redeemrewards

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>rewards</b> — Rewards List
 * <b>participantid</b> — Campaign Participant ID.
 * <b>amount</b> — amount of money to reward (null when non-monetary incentive is used).<br/>
(OR)
 * <b>participantid</b> — Campaign Participant ID.
  * <b>rewarddetails</b> — List of Reward Details
   * <b>rewarddtlid</b> — Reward detail ID, this will be generated on successful conversion(Install/Singup/Transaction..etc).

#####<b>Sample Input 1:</b>

Use this to redeem specific amount for a particular referrer, using _participantid_.
```json
{
    "apikey": "763502957c424314b613d42400ac7a7e",
    "privatekey": "8a433343ee6241a10419212415496559",
    "rewards":[{
	  "participantid": "23234",
	  "amount": "200"            
    }]
}
```
#####<b>Sample Response:</b>
```json
{
"success":true,
"message":""
}
```
#####<b>Sample Input 2:</b>

Use this to redeem rewards earned on a specific conversion event, using _rewarddtlid_.
```json
{
"apikey":"763502957c424314b613d42400ac7a7e",
"privatekey":"8a433343ee6241a10419212415496559",
"rewards":[
{
"participantid":"34216",
"rewarddetails":[
{"rewarddtlid":"43442"
},
{
"rewarddtlid":"43432"
},
{
"rewarddtlid":"43542"
}
]} 
]}

```
#####<b>Sample Response:</b>
```json
{
"success":true,
"message":""
}
```
4. Change Reward Status
----------------------

Status of the reward can be changed from server side by calling the end point "changerewardstatus".

<b>Route</b>
<pre><code>POST /v1/changerewardstatus

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>rewardslist</b> — Rewards List
 * <b>rewarddtlid</b> — Reward Detail ID.
 * <b>reward_status</b> — Reward status can be <b>Approved/Rejected/Suspicious/UnderReview</b>.

#####<b>Sample Input:</b>
```json
{
"apikey":"7ffdda00fd5c4338a9c1a44e00663648",
"privatekey":"d1e881dc60fa4856be34a44f00d96c9a",
"rewardslist":[
{
"rewarddtlid":"797",
"reward_status":"Approved"
}
]
}
```
#####<b>Sample Response:</b>
```json
{
"success":true,
"message":""
}
```
5. Redeem Friend Rewards
----------------------

Use this call to approve Friend rewards in case of In-Store credits.

<b>Route</b>
<pre><code>POST /v1/approvereward

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>rewards</b> — Rewards List
 * <b>rewardid</b> — Reward Detail ID.
 * <b>reward_type</b> — Reward type can be <b>Coupon/InstoreCredits/Other</b>.
 * <b>status</b> — Status can be <b>Distribute/Reject</b>.

#####<b>Sample Input:</b>
```json
{
"apikey":"7ffdda00fd5c4338a9c1a44e00663648",
"privatekey":"d1e881dc60fa4856be34a44f00d96c9a",
"rewards":[
{
"rewardid":"797",
"reward_type":"Coupon",
"status":"Distribute"
}
]
}
```
#####<b>Sample Response:</b>
```json
{
"success":true,
"message":""
}
```
6. Get Referrer/Friend Balance
----------------------

Use this call to check the referrer available balance and under review credits. If the referrer participated in multiple campaigns, it returns multiple records with reward details for each campaign.

<b>Route</b>
<pre><code>POST /v1/getuserdata

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>userkey</b> —  User key for the App
* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings

#####<b>Sample Input:</b>
```json
{
"userkey":"588d87d8d9e89ac5d710caf68910ac5d",
"apikey":"7ffdda00fd5c4338a9c1a44e00663648",
"privatekey":"d1e881dc60fa4856be34a44f00d96c9a",
}
```
#####<b>Response Parameters:</b>

* <b>success</b> —  Response status
* <b>message</b> — message if there is any for that referrer
* <b>userpoints</b> — List of points
 * <b>campaignid</b> — Unique Campaign ID
 * <b>participantid</b> — Campaign Participant ID
 * <b>total</b> — Total Rewards for that Campaign
 * <b>claimed</b> — Rewards claimed for that Campaign
 * <b>redeemable_balance</b> — Redeemable Balance i.e. rewards which met the review period and redemption cap. 
 * <b>underreview</b> — Rewards under review for that Campaign
 * <b>rewardunit</b> — Reward unit
 * <b>redemptionthreshold</b> — Redemption cap, it helps to let you know when to distribute the referrer reward.

#####<b>Sample Response:</b>
```json
{
"success":true,
"message":null,
"userpoints":[
{
"campaignid":34,
"participantid":"93719",
"total":"10",
"claimed":"10",
"redeemable_balance":"0",
"underreview":"0",
"rewardunit":"$",
"redemptionthreshold":"0"
}
]
}
```
7. Register Conversion Event
----------------------

Conversion events can also be registered from server side. This helps if you don't want to send the conversion event from your App. You have to use the private key and App userkey to make this call. 

<b>Route</b>
<pre><code>POST /v1/registerconversionevent

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>userkey</b> —  User key for the App
* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>eventName</b> —   Install, Signup, Transaction & Any defined Custom Events
* <b>transactionValue</b> —  Transaction amount
* <b>transactionUnit</b> —  Transaction currency unit
* <b>extrainfo</b> —  Custom Info which is stored across the event and will be provided on query of rewards. It is generally used to save transaction information which can be used to cross check later while rewarding. Extra Info is expected in encoded Uri format.
* <b>tskey</b> — Unique Integer for an Event to avoid duplicate rewards on retry. (Eg: Unix Timestamp 1453300397)

#####<b>Sample Input:</b>
```json
{
	"userkey": "588d87d8d9e89ac5d710caf68910ac5d",
	"apikey": "7ffdda00fd5c4338a9c1a44e00663648",
	"privatekey": "d1e881dc60fa4856be34a44f00d96c9a",
	"eventName": "Transaction",
	"transactionValue": "250.00",
	"transactionUnit": "$",
	"extrainfo": "%7B%22OrderID%22%3A%22465%22%2C%22Ordernote%22%3A%22CashonDelivery%22%7D",
	"tskey": 1453300397
}
```
#####<b>Response Parameters:</b>

* <b>success</b> —  returns true on successful conversion(i.e. Referrer/Frined got rewarded).
* <b>message</b> — Conversion event message if any.

#####<b>Sample Response:</b>
```json
{
"success":true,
"message":null
}
```

8. Update User details
----------------------

This API call helps in updating App User details from server side calls. If you want to send the user details from server and not the app, generally used in case of signup using third-party credentials (Eg. Facebook, Twitter, Google etc). It is required to send private key and App userkey along with user details in order to call the update. 

<b>Route</b>
<pre><code>POST /v1/updateuserinfo

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>userkey</b> —  User key for the App
* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>EmailId</b> — Email of the user.
* <b>AppUserName</b> — First Name of the user, required to personalize the referral messages.
* <b>ProfileImage</b> — User profile picture URL, required to personalize the referral messages.
* <b>UserIdInstore</b> — ID of the user in your App(helps to identify users on dashboard as you do in your app).
* <b>city</b> — City of the User Location.
* <b>country</b> — Country of the User Location.
* <b>state</b> — State of the User Location.
* <b>Phone</b> — User phone number.
* <b>isExistingUser</b> — Set this as True, if you identify the user as existing user(this is useful if you don't want to reward existing users).

#####<b>Sample Input:</b>
```json
{
"userkey":"588d87d8d9e89ac5d710caf68910ac5d",
"apikey":"7ffdda00fd5c4338a9c1a44e00663648",
"privatekey":"d1e881dc60fa4856be34a44f00d96c9a",
"EmailId":"test@test.com",
"AppUserName":"MYT",
"ProfileImage":"",
"UserIdInstore":"167",
"isExistingUser":"false",
"city":"HYD",
"state":"TS",
"country":"IND",
"Phone":""
}
```
#####<b>Response Parameters:</b>

* <b>success</b> —  returns true on successful update.
* <b>message</b> — message if any.

#####<b>Sample Response:</b>
```json
{
"success":true,
"message":null
}
```

9. Approve Dynamic Coupon
----------------------

Use this call to approve Dynamic Coupon and send notification to user.

<b>Route</b>
<pre><code>POST /v1/approvereward

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>rewards</b> — Rewards List
 * <b>rewardid</b> — Reward Detail ID.
 * <b>reward_type</b> — Reward type can be <b>Coupon/InstoreCredits/Other</b>.
 * <b>status</b> — Status can be <b>Distribute/Reject</b>.

#####<b>Sample Input:</b>
```json
{
"apikey":"7ffdda00fd5c4338a9c1a44e00663648",
"privatekey":"d1e881dc60fa4856be34a44f00d96c9a",
"rewards":[
{
"rewardid":"797",
"reward_type":"Coupon",
"status":"Distribute"
}
]
}
```
#####<b>Sample Response:</b>
```json
{
"success":true,
"message":""
}
```

10. Check Reward Status
----------------------

This call helps to get the current status of the Reward.

<b>Route</b>
<pre><code>POST /v1/checkrewardstatus

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>rewarddtlid</b> — Reward Detail ID.

#####<b>Sample Input:</b>
```json
{
"apikey":"7ffdda00fd5c4338a9c1a44e00663648",
"privatekey":"d1e881dc60fa4856be34a44f00d96c9a",
"rewarddtlid":"797"
}
```
#####<b>Response Parameters:</b>

* <b>success</b> —  Call Success Response (<b>true/false</b>)
* <b>rewarddtlid</b> — Reward Detail ID
* <b>reward_status</b> — Reward status can be <b>Approved/Rejected/Suspicious/UnderReview/Rewarded</b>.
* <b>comment</b> — Information regarding the status change if any.

#####<b>Sample Response:</b>
```json
{
"success":true,
"rewarddtlid":"797",
"reward_status":"Suspicious",
"comment":"Friend has No Email / Invalid Hardware ID"
}
```

11. Get AppUser Details
----------------------

Get the details of App User.

<b>Route</b>
<pre><code>POST /v1/getappuserdetails

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>userkey</b> — User key for the App.

#####<b>Sample Input:</b>
```json
{
"userkey":"588d87d8d9e89ac5d710caf68910ac5d",
"apikey":"7ffdda00fd5c4338a9c1a44e00663648",
"privatekey":"d1e881dc60fa4856be34a44f00d96c9a",
}
```
#####<b>Response Parameters:</b>

* <b>success</b> —  Call Success Response (<b>true/false</b>)
* <b>message</b> — Information regarding the status change if any.
* <b>userkey</b> — Unique key to identify App User
* <b>deviceId</b> — Unique Id assigned to the device.
* <b>EmailId</b> — Email of the user.
* <b>DeviceAdvertisingId</b> — Advertising Id assigned to Device by Google/Apple.
* <b>AppUserName</b> — Name of the user.
* <b>FriendReferralCode</b> — Friend's Referral Code (By whom the User is referred).
* <b>ReferralCode</b> — User Referral Code.
* <b>UserIdInstore</b> — ID of the user in your App(helps to identify users on dashboard as you do in your app).

#####<b>Sample Response:</b>
```json
{
  "userkey": "588d87d8d9e89ac5d710caf68910ac5d",
  "deviceId": "00test0576890325442",
  "EmailId": null,
  "DeviceAdvertisingId": "7ebddcbf-50f0-4bd7-a271-b106648117b8",
  "AppUserName": "test210752name",
  "FriendReferralCode": "2def",
  "ReferralCode": "2der",
  "UserIdInstore": null,
  "success": true,
  "message": null
}
```

12. Get Campaign
----------------------

Get the campaign details of App based on growth hack.

<b>Route</b>
<pre><code>POST /v1/getcampaign

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>growthhack</b> — Growth Hack Type ("Word_of_Mouth").
* <b>campaignid</b> — Unique ID of a campaign generated by AppVirality.

#####<b>Sample Input:</b>
```json
{
"apikey":"7b808b1f934448db8463a4c60091c49b",
"privatekey":"097262223465191eda4ec006d601b",
"growthhack":"Word_of_Mouth",
"campaignid":null
}
```
#####<b>Response Parameters:</b>

#####<b>Sample Response:</b>
```json
{
    "AppCampaignsDetails": [
        {
            "AppID": 637,
            "CampaignID": 283,
            "CampaignName": "mom+grocery",
            "OfferTitle": "refer+your+friend+and+get+%3cbr%3e10+points+bla+bla",
            "OfferDescription": "get+10+Rs+if+your+friend+installs%2csignup+and+transaction",
            "CampaignStartDate": "Jul 06, 2015 12:00:00 AM",
            "CampaignTerms": "terms",
            "LaunchMessage": "text+message",
            "GrowthHackName": "Word_of_Mouth",
            "SocialActions": [
                {
                    "socialActionId": 1,
                    "socialActionName": "Facebook",
                    "sharetitle": "Referrer+link",
                    "ShareMessage": "Just+found+a+great+app!+I%27m+sure+you+will+like+it+too%3a+SHARE_URL.+Use+my+referral+code+SHARE_CODE",
                    "ShareImageURL": "",
                    "ShareURL": "",
                    "displayorder": null
                },
                {
                    "socialActionId": 3,
                    "socialActionName": "WhatsApp",
                    "sharetitle": "refer+your+friend+and+get+%3cbr%3e10+points+bla+bla",
                    "ShareMessage": "Just+found+a+great+app!+I%27m+sure+you+will+like+it+too%3a+SHARE_URL.+Use+my+referral+code+SHARE_CODE",
                    "ShareImageURL": "1growthcampaign064728-09242015e2e92.png",
                    "ShareURL": "",
                    "displayorder": null
                },
                {
                    "socialActionId": 5,
                    "socialActionName": "Mail",
                    "sharetitle": "RL",
                    "ShareMessage": "Just+found+a+great+app!+I%27m+sure+you+will+like+it+too%3a+SHARE_URL.+Use+my+referral+code+SHARE_CODE",
                    "ShareImageURL": "",
                    "ShareURL": "",
                    "displayorder": null
                },
                {
                    "socialActionId": 10,
                    "socialActionName": "Pinterest",
                    "sharetitle": "",
                    "ShareMessage": "Just+found+a+great+app!+I%27m+sure+you+will+like+it+too%3a+SHARE_URL.+Use+my+referral+code+SHARE_CODE",
                    "ShareImageURL": "http://www.planwallpaper.com/static/images/Winter-Tiger-Wild-Cat-Images.jpg",
                    "ShareURL": "",
                    "displayorder": null
                },
                {
                    "socialActionId": 14,
                    "socialActionName": "CustomLink",
                    "sharetitle": "refer+your+friend+and+get+%3cbr%3e10+points+bla+bla",
                    "ShareMessage": "customlink",
                    "ShareImageURL": "1growthcampaign064728-09242015e2e92.png",
                    "ShareURL": "",
                    "displayorder": null
                }
            ],
            "RewardRules": [
                {
                    "CampaignId": 283,
                    "RewardUserType": "Friend",
                    "EventName": "Signup",
                    "Reward": "10",
                    "RewardUnit": "points",
                    "RewardFrequency": "1",
                    "MinTranValue": "",
                    "MaxRewardAmount": ""
                },
                {
                    "CampaignId": 283,
                    "RewardUserType": "Referrer",
                    "EventName": "Signup",
                    "Reward": "10",
                    "RewardUnit": "points",
                    "RewardFrequency": "1",
                    "MinTranValue": "",
                    "MaxRewardAmount": ""
                },
                {
                    "CampaignId": 283,
                    "RewardUserType": "Referrer",
                    "EventName": "Transaction",
                    "Reward": "10",
                    "RewardUnit": "points",
                    "RewardFrequency": "0",
                    "MinTranValue": "100",
                    "MaxRewardAmount": ""
                }
            ]
        }
    ]
}
```

13. Add Test Device
----------------------

It helps to Add Test Device.To add test device, please click on "Add Test Device" button in AV Dashboard > Test Devices page. After clicking on button within 30 sec execute the following API.

<b>Route</b>
<pre><code>POST /v1/addtestdevice

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>DeviceID</b> — Device ID of the Mobile.

#####<b>Sample Input:</b>
```json
{
"apikey":"7b808b1f934448db8463a4c60091c49b",
"privatekey":"097262223465191eda4ec006d601b",
"deviceid":"d3e7190ac98140faa9932e89f2ba84e3"
}
```
#####<b>Response Parameters:</b>

* <b>success</b> —  Call Success Response (<b>true/false</b>)
* <b>message</b> — Information regarding the status change if any.

#####<b>Sample Response:</b>
```json
{
  "success": true,
  "message": null
}
```

14. Reset Test Device
----------------------

It helps to Reset Test Device.

<b>Route</b>
<pre><code>POST /v1/resettestdevice

Content-Type application/json
</code></pre>

#####<b>Input Parameters:</b>

* <b>apikey</b> —  API Key of the App, get this from Dashboard > App Details
* <b>privatekey</b> — Private key for API requests, get this from Dashboard > App Details > Change Settings > Advanced Settings
* <b>DeviceID</b> — Device ID of the Mobile.

#####<b>Sample Input:</b>
```json
{
"apikey":"7b808b1f934448db8463a4c60091c49b",
"privatekey":"097262223465191eda4ec006d601b",
"deviceid":"d3e7190ac98140faa9932e89f2ba84e3"
}
```
#####<b>Response Parameters:</b>

* <b>success</b> —  Call Success Response (<b>true/false</b>)
* <b>message</b> — Information regarding the status change if any.

#####<b>Sample Response:</b>
```json
{
  "success": true,
  "message": null
}
```


<H3>Help on other topics:</H3>

Please have a look at our [Wiki page](https://github.com/appvirality/appvirality-sdk-android/wiki)

1. [Getting Started With AppVirality Android SDK Integration](https://github.com/appvirality/appvirality-sdk-android#integrating-appvirality-into-your-app)
2. [AppVirality API for referral Growth Hack](https://github.com/appvirality/AppVirality-API)
3. [How to Add Test Devices & Test Referral Program](https://github.com/appvirality/appvirality-sdk-android/wiki/Testing-Your-Referral-Programs)
4. [Using Custom Domain](https://github.com/appvirality/appvirality-sdk-android/wiki/Using-Custom-Domain)
5. [Init Callback | hasReferrer | getUserKey](https://github.com/appvirality/appvirality-sdk-android/wiki/AppVirality-Init-Callback)
6. [Using Referral Code & Referral Link](https://github.com/appvirality/appvirality-sdk-android/wiki/Referral-program-with-Referral-code-&-Link)
7. [Optional] [Exclude Premium Users](https://github.com/appvirality/appvirality-sdk-android/wiki/Exclude-Premium-Users)
8. [Optional] [Dynamic Share Message](https://github.com/appvirality/appvirality-sdk-android/wiki/Dynamic-Share-Message)
9. [Optional] [Remind Later Settings](https://github.com/appvirality/appvirality-sdk-android/wiki/Remind-Later-Settings)
10. [Optional] [To Whom and When to Show Growth Hack](https://github.com/appvirality/appvirality-sdk-android/wiki/To-Whom-and-When-to-Show-Growth-Hack)
11. [Optional] [Reward Notifications or Web-hook Configuration](https://github.com/appvirality/appvirality-sdk-android/wiki/Reward-Notifications)
12. [Optional] [Android Push Notification Configuration](https://github.com/appvirality/appvirality-sdk-android/wiki/Android-Push-Notification-Configuration)
13. [Optional] [Personalized Welcome Screen](https://github.com/appvirality/appvirality-sdk-android/wiki/Personalized-Welcome-Screen)
14. [Referral Program on Apps having Login and Logout](https://github.com/appvirality/appvirality-sdk-android/wiki/Referral-Program-on-Apps-having-LogOut-&-LogIn)
