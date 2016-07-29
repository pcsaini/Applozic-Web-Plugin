# Applozic-Web-Plugin


### Overview         

Open source Chat and Messaging SDK that lets you add real time chat and messaging in your mobile (android, iOS) applications and website.

Signup at https://www.applozic.com to get the application key.

<img  align="middle"  src="img/applozic.jpg"/>

<img align="right" src="img/webplugin.jpg" />

Applozic One to One and Group Chat SDK

Documentation: https://www.applozic.com/docs/web-chat-plugin.html

Features:


 One to one and Group Chat
 
 Image capture
 
 Photo sharing
 
 File attachment
 
 Location sharing
 
 Push notifications
 
 In-App notifications
 
 Online presence
 
 Last seen at 
 
 Unread message count
 
 Typing indicator
 
 Message sent, delivery report
 
 Offline messaging
 
 Multi Device sync
 
 Application to user messaging
 
 Customized chat bubble
 
 UI Customization Toolkit
 
 Cross Platform Support (iOS, Android & Web)



### Getting Started       

Applozic messaging jQuery plugin

A jQuery plugin to integrate messaging into your web page for real time communication between users via Applozic messaging platform and also to see your latest conversations and past chat history. Add Applozic messaging plugin into your web application :


### Overview      


Integrate messaging into your mobile apps and website without developing or maintaining any infrastructure. Sign up at https://www.applozic.com         


### Getting Started          


****Applozic messaging jQuery plugin****

Javascript chat and messaging plugin that lets you enable real time chat using websockets in your website without developing or maintaining any infrastructure.


Signup at [Applozic](https://www.applozic.com/signup.html) to get the application key.

#### Step 1: Add the Applozic Chat plugin script before ```</head>``` into your web page            

```
<script type="text/javascript">
   (function(d, m){var s, h;       
   s = document.createElement("script");
   s.type = "text/javascript";
   s.async=true;
   s.src="https://apps.applozic.com/sidebox.app";
   h=document.getElementsByTagName('head')[0];
   h.appendChild(s);
   window.applozic=m;
   m.init=function(t){m._globals=t;}})(document, window.applozic || {});
</script>
```
 
#### Step 2: Initialize Chat Plugin

``` 
<script type="text/javascript">
  window.applozic.init({appId: 'PUT_APPLICATION_KEY_HERE',     // obtained from Step 1 (required)  
                        userId: 'PUT_USERID_HERE',             // loggedIn user Id (required)  
                        userName: 'PUT_USER_DISPLAYNAME_HERE',  // loggedIn user name (optional)  
                        imageLink : 'PUT_USER_IMAGE_LINK_HERE',        // loggedIn user image url (optional)    
                        email: 'PUT_USER_EMAIL_ID_HERE',      // optional
                        contactNumber: 'CONTACT_NUMBER_WITH_INTERNATIONAL_CODE eg: +919535008745', //optional
                        accessToken: 'PUT_USER_AUTHENTICATION_TOKEN_HERE',   // optional
                        authenticationTypeId : 'PUT_AUTHENTICATION_TYPE_ID_HERE',   
                                                        // 1 for password verification from Applozic server  (optional)  
                                                        // 0 for access Token verification from client server (optional)
                        desktopNotification: true or false,           // optional
                        notificationIconLink: 'PUT_LOGO_IMAGE_LINK_HERE',    // required for desktop notification (optional) 
                        maxGroupSize: 'MAX NUMBER OF USERS ALLOWED PER GROUP WHILE CREATING GROUP' // max limit is 100 (optional),
                        contactDisplayName: function(userId) {},   //Function should return USER_DISPLAY_NAME by taking USERID as input parameter (optional).
                        contactDisplayImage: function(userId) {},  // Function should return USER_IMAGE_URL by taking USERID as a input parameter (optional). 
                        onInit : function(response) {},  // Callback function which gets triggered on plugin initialized. You can write your own logic inside this function to execute on plugin initialization (optional).   
                          
                        });
</script>
```    
**Note** : desktopNotification support only for chrome browser, notificationIconLink will be display in desktop notification



#### Step 3: Contacts

Javascript code to load contacts

```
var CONTACT_LIST_JSON = 
          {"contacts": [{"userId": "USER_1", "displayName": "Devashish", 
                          "imageLink": "https://www.applozic.com/resources/images/applozic_icon.png"}, 
                        {"userId": "USER_2", "displayName": "Adarsh", 
                          "imageLink": "https://www.applozic.com/resources/images/applozic_icon.png"}, 
                        {"userId": "USER_3", "displayName": "Shanki",
                          "imageLink": "https://www.applozic.com/resources/images/applozic_icon.png"}
                        ]
         };  //Replace this with contacts json from your application
         

$applozic.fn.applozic('loadContacts', CONTACT_LIST_JSON);

```

**NOTE**- Call **loadContacts** function only after plugin initailize callback (see Step 3 for reference).


#### Step 4: Chat screen

Javascript to open main chat box containing list of contacts

```
 $applozic.fn.applozic('loadTab', '');  
 ``` 
 
Javascript to open chat with User

```
 $applozic.fn.applozic('loadTab', 'PUT_OTHER_USERID_HERE');  // user Id of other person with whom you want to open conversation 
 ``` 
 
 Javascript to open chat with Group

```
 $applozic.fn.applozic('loadGroupTab', 'PUT_GROUP_ID_HERE');  // group Id returned in response to group create api  
 ``` 
 
 Javascript to open group chat using Client Group Id
 
```
 $applozic.fn.applozic('loadGroupTabByClientGroupId',{clientGroupId:'CLIENT_GROUP_ID'});
```

Anchor tag or button to load(open) individual tab conversation directly

Add a chat button inside your web page using ```a``` tag and use 'userId' for data attribute "data-mck-id"   

```
<a href="#" class="applozic-launcher" data-mck-id="PUT_OTHER_USERID_HERE" data-mck-name="PUT_OTHER_USER_DISPLAY_NAME_HERE">CHAT BUTTON</a>
 ```        
 
 **Note** - Data attribute **mck-name** is optional in above tag       
 
#### Step 5: Group 
 
 Javascript to get group list
 
 ```
 $applozic.fn.applozic('getGroupList', {'callback':function (response) { //write your logic}});   
 ``` 
 
Sample response:

```
           {'status' : 'success' ,                 // or error
            'data': [ {'id': 'GROUP_ID',
                       'name' : 'GROUP_NAME',
                       'type' : 'GROUP_TYPE',      // 1,2 or 5   (private, public or broadcast)
                       'memberName':[],           // Array of group member ids
                       'adminName': 'ADMIN_USER_ID',
                       'removedMembersId' [],     // Array including removed or left members Id  
                       'unreadCount' : '10'       // total unread count of messages for current logged in user
                        }]    
                     }]
           }
```


 Javascript to create group
 
 ```
 $applozic.fn.applozic('initGroupTab', {'groupName' : 'GROUP_NAME',   // required
                                        'type' :1,                    // 1 for private , 2 for public (required)
                                        'clientGroupId' : 'CLIENT_UNIQUE_GROUP_ID', // optional
                                        'users': [{userId:'USER_ID_1', displayName:'USER_NAME'},
                                                  {userId:'USER_ID_2', displayName:'USER_NAME'}
                                                 ]});   
 ``` 
 
Javascript to add group member (only for group admin)
 
 ```
$applozic.fn.applozic('addGroupMember',{'groupId':'GROUP_ID',  
                                        'clientGroupId' : 'CLIENT_GROUP_ID',  //use either groupId or clientGroupId
                                        'userId':'USER_ID_OF_MEMBER_TO_ADD', 'callback': function(response) {console.log(response);}});
 ``` 
 
 Javascript to remove group member (only for group admin)
 
 ```
$applozic.fn.applozic('removeGroupMember',{'groupId':'GROUP_ID',
                                           'clientGroupId' : 'CLIENT_GROUP_ID', //use either groupId or clientGroupId
                                           'userId':'USER_ID_OF_MEMBER_TO_REMOVE',
                                           'callback': function(response) {console.log(response);}
                                           });
 ```  
 
 Javascript to exit group
 
 ```
$applozic.fn.applozic('leaveGroup', {'groupId' : 'GROUP_ID', 
                                     'clientGroupId' : 'CLIENT_GROUP_ID', //use either groupId or clientGroupId
                                     'callback' :function(response){console.log(response);}});
 ```  
 
 Javascript to update group info
 
 ```
$applozic.fn.applozic('updateGroupInfo', {'groupId' : 'GROUP_ID', 
                                     'clientGroupId' : 'CLIENT_GROUP_ID', //use either groupId or clientGroupId,
                                     'name' : 'GROUP_NAME', // optional
                                     'imageUrl' : 'GROUP_ICON_URL',  //optional
                                     'callback' : function(response){console.log(response);}});
 ```  
 
#### Step 6: Context (Topic) based Chat
 
 Add the following in window.applozic.init call:
 
 ```
  topicBox: true,
  getTopicDetail: function(topicId) {
         //Based on topicId, return the following details from your application
         return {'title': 'topic-title',      // Product title
                     'subtitle': 'sub-title',     // Product subTitle or Product Id
                     'link' :'image-link',        // Product image link
                     'key1':'key1' ,              // Small text anything like Qty (Optional)
                     'value1':'value1',           // Value of key1 ex-10 (number of quantity) Optional
                     'key2': 'key2',              // Small text anything like MRP (product price) (Optional)
                     'value2':'value2'            // Value of key2 ex-$100  (Optional)
                  };
  }
 ```
 
 Add a chat button inside your web page using ```a``` tag and add the following:
 
 ```
 Class Attribute - applozic-wt-launcher 
 Data Attriutes  - mck-id, mck-name and mck-topicid
```

```
 mck-id      :  User Id of the user with whom to initiate the chat
 mck-name    :  Display name of the user with whom to initiate the chat
 mck-topicId :  Unique identifier for the topic/product 
 ```
 
 ```
 <a href="#" class="applozic-wt-launcher" data-mck-id="PUT_USERID_HERE" data-mck-name="PUT_DISPLAYNAME_HERE" data-mck-topicid="PUT_TOPICID_HERE">CHAT ON TOPIC</a>
 ```
 
#### Step 7: Events subscription

Using events callback, you can subscribe to the following events.

```
var apzEvents =  {onConnect: function () {
                        console.log('connected successfully');
                  }, onConnectFailed: function () {
                       console.log('connection failed');
                  }, onMessageDelivered: function (obj) {
                       console.log('onMessageDelivered: ' + obj);
                  }, onMessageRead: function (obj) {
                       console.log('onMessageRead: '  + obj);
                  }, onMessageReceived: function (obj) {
                       console.log('onMessageReceived: ' + obj);
                  }, onMessageSentUpdate: function (obj) {
                       console.log('onMessageSentUpdate: ' + obj);
                  }, onUserConnect: function (obj) {
                       console.log('onUserConnect: ' + obj);
                  }, onUserDisconnect: function (obj) {
                       console.log('onUserDisconnect: ' + obj);
                  }, onUserBlocked: function (obj) {
                       console.log('onUserBlocked: ' + obj);
                  }, onUserUnblocked': function (obj) {
                       console.log('onUserUnblocked: ' + obj);
                  }, onUserActivated: function () {
                       console.log('user activated by admin');
                  }, onUserDeactivated: function () {
                       console.log('user deactivated by admin');
                  }
                };
```

#### Events description:

1) onConnect: Triggered when user subscribed successfully. 


2) onConnectFailed: Triggered when user failed to subscribe. 


3) onMessageDelivered: Triggered when message is delivered. 

{'messageKey': 'delivered-message-key'} 


4) onMessageRead: Triggered when delivered message is read on other end. 

Response object - 

{'messageKey': 'delivered-message-key'}


5) onMessageReceived: Triggered when new message received. 

Response object - {'message': message} 


6) onMessageSentUpdate: Triggered when message sent successfully to server. 

Response object- {'messageKey':'sent-message-key'} 


7) onUserConnect: Triggered when some other user comes online.

Response object - {'userID': 'connected-user-Id'} 


8) onUserDisconnect: Triggered when some other user goes offline. 

Response object - {'userId': 'disconnected-user-id', 'lastSeenAtTime' : 'time in millsec'}


9) onUserBlocked : Triggered when user is blocked or current user blocked other user from different source 

Response object - {'status': 'BLOCKED_TO or BLOCKED_BY', 'userId': userId}


10) onUserUnblocked : Triggered when user is unblocked or current user unblocked other user from different source 

Response object - {'status': 'UNBLOCKED_TO or UNBLOCKED_BY', 'userId': userId}


11) onUserActivated : Triggered when user is activated by app admin 


12) onUserDeactivated : Triggered when user is deactivated by app admin



#### Javascript to subscribe to events

```
 $applozic.fn.applozic('subscribeToEvents', apzEvents);  // object containing event definations 
 ``` 

#### Step 8: Messages     

```
  $applozic.fn.applozic('messageList', {'id': 'Group Id or User Id',   
                                        'isGroup': false,               // True in case of group 
                                        'clientGroupId' : 'CLIENT_GROUP_ID', // use either groupId or clientGroupId
                                        'callback': function(response){ // write your logic} 
                                        });
```        

 
Sample response:           

 ```
 response = {'status' : 'success',                     // or error
             'messages' :[{'key': "MESSAGE_IDENTIFIER",
                          'from': "SENDER_USERID",         
                          'to': 'RECEIVER_USERID',
                          'message': "MESSAGE_TEXT",
                          'type': 'inbox or outbox',
                          'status': "MESSAGE__CURRENT_STATUS",        // For outbox message  (sent, delivered or read)
                                                                    // For inbox messsage (read, unread)
                          'timeStamp': 'MESSAGE_CREATED_TIMESTAMP'          
                         }]                
           }
```         

### UI Customization
 
 
 For customizing the UI, download files from https://github.com/AppLozic/Applozic-Web-Plugin/tree/master/message/advanced
 Open message.html file as a reference and add all scripts and html in your web page in same order as given in message.html
 
 You can modify mck-sidebox-1.0.css class located at:
 https://github.com/AppLozic/Applozic-Web-Plugin/blob/master/message/advanced/css/app/mck-sidebox-1.0.css

  
  
###Advance options
 
 
####  Send message

Send message from logged in user to another user
 ```
 var messageJson = 
          {"to":'USER_ID',                                 // required
           "message" : 'TEXT_MESSAGE'                      // required
        }; 
$applozic.fn.applozic('sendMessage', messageJson);
 ```



Send message visible only to the receiver.
 ```
var messageJson = 
          {"to":'USER_ID',                                     // required
           "type" : 12,                                        // required
           "message" : 'TEXT_MESSAGE'                          // required
        };  
$applozic.fn.applozic('sendMessage', messageJson);
 ```

####  Get User Details


```
  $applozic.fn.applozic('getUserDetail', {callback: function getUserDetail(response) {
        if(response.status === 'success') {
           // write your logic
        }
     }
  });
```

Sample response:

```
           {'status' : 'success' ,                     // or error
            'data':  {'totalUnreadCount': 15           // total unread count for user          
                     'users':                          // Array of other users detail
                        [{"userId":"USERID_1","connected":false,"lastSeenAtTime":1453462368000,"createdAtTime":1452150981000,"unreadCount":3}, 
                        {"userId":"USERID_2","connected":false,"lastSeenAtTime":1452236884000,"createdAtTime":1452236884000,"unreadCount":1}]    
                     }
           }
```



### Light weight plugin with your own UI 

#### Add following scripts before ```</head>``` tag

```
<script type="text/javascript" src="https://www.applozic.com/resources/lib/js/mck-socket.min.js"></script>      
<script type="text/javascript" src="https://www.applozic.com/resources/sidebox/js/app/apz-client-1.0.js"></script>
```

#### Initialize Plugin

Create APPLOZIC instance by configuring your options

```

 var applozic = new APPLOZIC({'baseUrl': "https://apps.applozic.com",
                              'userId': 'PUT_USERID_HERE',                   // LoggedIn userId
                              'appId': 'PUT_APPLICATION_KEY_HERE',           // obtained from Step 1 (required)
                              'onInit': function(response) { 
                                           if (response === "success") {
                                                 // plugin loaded successfully, perform your actions if any, for example: load contacts, getting unread message count, etc
                                           } else {
                                                 // error in loading plugin (you can hide chat button or refresh page) 
                                           }
                                         }
                            });
```


Javascript to subscribe to events

```
 applozic.events = apzEvents;      // apzEvents defined in Step 8
 ``` 


More details here: 
https://www.applozic.com/docs/web-chat-plugin.html


##Help

We provide support over at [StackOverflow] (http://stackoverflow.com/questions/tagged/applozic) when you tag using applozic, ask us anything.

Applozic is the best jquery chat plugin for instant messaging, still not convinced? Write to us at github@applozic.com and we will be happy to schedule a demo for you.

##Github projects

Android Chat SDK https://github.com/AppLozic/Applozic-Android-SDK

Web Chat Plugin https://github.com/AppLozic/Applozic-Web-Plugin

iOS Chat SDK https://github.com/AppLozic/Applozic-iOS-SDK
