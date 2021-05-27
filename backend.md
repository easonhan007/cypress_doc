# cypress relaworld的后台接口分析

## 数据库设计

我一般喜欢在读后端代码的时候先看后端的数据库设计。

RWA的数据库使用的是[lowdb](https://github.com/typicode/lowdb)。这其实是一个基于json文件进行存储的超简单数据库实现。

所有数据表的定义在[这里](https://github.com/cypress-io/cypress-realworld-app/blob/develop/data/empty-seed.json)。

```javascript
{
  "users": [],
  "contacts": [],
  "bankaccounts": [],
  "transactions": [],
  "likes": [],
  "comments": [],
  "notifications": [],
  "banktransfers": []
}
```

### user表

用户表，存储用户信息，比如

```javascript
{
    "id": "t45AiwidW",
    "uuid": "6383f84e-b511-44c5-a835-3ece1d781fa8",
    "firstName": "Edgar",
    "lastName": "Johns",
    "username": "Katharina_Bernier",
    "password": "$2a$10$5PXHGtcsckWtAprT5/JmluhR13f16BL8SIGhvAKNP.Dhxkt69FfzW",
    "email": "Norene39@yahoo.com",
    "phoneNumber": "625-316-9882",
    "avatar": "https://cypress-realworld-app-svgs.s3.amazonaws.com/t45AiwidW.svg",
    "defaultPrivacyLevel": "public",
    "balance": 168137,
    "createdAt": "2019-08-27T23:47:05.637Z",
    "modifiedAt": "2020-05-21T11:02:22.857Z"
},
```
这里用户表里有个balance字段，应该存的是用户账户余额，属于比较重要的信息。

### contacts表

联系人表，用来保存联系人信息，比如

```javascript
{
    "id": "LSQ1h-WU1z",
    "uuid": "2413a170-304d-4118-93ba-6b52a9cc581a",
    "userId": "t45AiwidW",
    "contactUserId": "qywYp6hS0U",
    "createdAt": "2019-10-30T16:33:36.608Z",
    "modifiedAt": "2020-05-21T11:29:12.141Z"
},
{
    "id": "c4A_5NFD3z",
    "uuid": "9ab08f66-a458-487c-9bde-1c0bc3db6c7b",
    "userId": "t45AiwidW",
    "contactUserId": "bDjUb4ir5O",
    "createdAt": "2019-09-02T00:35:52.232Z",
    "modifiedAt": "2020-05-21T04:38:43.738Z"
},
```
从上面可以看出userId == t45AiwidW的用户有2个联系人，分别是qywYp6hS0U和bDjUb4ir5O。

### bankaccounts

银行账户表，这个很容易理解。

```javascript
{
    "id": "RskoB7r4Bic",
    "uuid": "a45f1803-b845-42aa-9142-f5f80ea09416",
    "userId": "t45AiwidW",
    "bankName": "O'Hara - Labadie Bank",
    "accountNumber": "6123387981",
    "routingNumber": "851823229",
    "isDeleted": false,
    "createdAt": "2020-05-09T07:57:26.947Z",
    "modifiedAt": "2020-05-21T22:18:50.916Z"
},
```

上面的数据就表示userId为t45AiwidW的用户，银行卡账号是6123387981。

### transactions

交易表，存交易数据，银行账户的一次转账就是一笔交易。

```javascript
{
    "id": "-jCJOEkLh0J",
    "uuid": "0dd2a4e1-7cfd-4acd-bf53-6a377be01c56",
    "source": "RskoB7r4Bic",
    "amount": 47410,
    "description": "Payment: t45AiwidW to qywYp6hS0U",
    "privacyLevel": "contacts",
    "receiverId": "qywYp6hS0U",
    "senderId": "t45AiwidW",
    "balanceAtCompletion": 38316,
    "status": "complete",
    "requestStatus": "",
    "requestResolvedAt": "2020-06-03T01:22:21.937Z",
    "createdAt": "2019-08-24T18:58:38.088Z",
    "modifiedAt": "2020-05-21T11:46:37.285Z"
},
```

上面数据的意思是用户t45AiwidW给用户qywYp6hS0U转账了47410，这笔交易的状态是complete。

### likes

点赞表,用户可以给交易点赞。

```javascript

{
    "id": "MC54o2D5r9aU",
    "uuid": "745e203b-1246-4e1c-a76e-d053c9f932ed",
    "userId": "t45AiwidW",
    "transactionId": "WIHpqM0xpcTx",
    "createdAt": "2020-04-20T12:02:27.515Z",
    "modifiedAt": "2020-05-21T06:23:07.619Z"
},
```

猜一猜上面的数据代表了什么。

### comments

评论表，下面的数据表示用户t45AiwidW给交易lPUBZKlc4MLR添加了一条评论。

```javascript
{
    "id": "K3HLpKcGKDiP",
    "uuid": "4f2adee3-dd86-4948-bdc3-3e44b18206e7",
    "content": "inventore perferendis soluta",
    "userId": "t45AiwidW",
    "transactionId": "lPUBZKlc4MLR",
    "createdAt": "2019-07-03T01:35:58.062Z",
    "modifiedAt": "2020-05-21T22:14:55.334Z"
},

```

### notifications

通知表，用户在一定的条件下可以收到通知，比如收到了一笔交易的时候，这里就不举例子了。

### banktransfers

银行交易相关的信息，每一次的交易都会发生关联的银行账户变动，这个表就保存了这些信息。

```javascript
{
    "id": "WgiYCFrxjGIo",
    "uuid": "2c07eba1-2027-476c-be42-4bb56b78187a",
    "userId": "t45AiwidW",
    "source": "RskoB7r4Bic",
    "amount": 40101,
    "type": "deposit",
    "transactionId": "jjxVhrcgwW-",
    "createdAt": "2019-06-07T19:01:48.699Z",
    "modifiedAt": "2020-05-21T06:01:23.277Z"
},
```

## 接口设计

理解了持久化层之后，我们看一下后台系统具体的接口，接口的路由定义在backend文件夹下的这些文件里。

```
bankaccount-routes.ts
banktransfer-routes.ts
comment-routes.ts      
contact-routes.ts      
like-routes.ts         
notification-routes.ts 
testdata-routes.ts     
transaction-routes.ts  
user-routes.ts
```

### user接口

[user-routes.ts](https://github.com/cypress-io/cypress-realworld-app/blob/develop/backend/user-routes.ts)


| method  | endpoint | 描述 |
| ------- | ---------| ------------- |
| GET     |  /users  | 返回所有用户信息|
| GET     |  /search  | 按条件搜索用户|
| POST     |  /users  | 创建用户|
| GET     |  /users/:user_id  | 通过用户id查找用户|
| GET     |  /users/profile/:username  | 通过用户名查找用户，返回用户的基本信息["firstName", "lastName", "avatar"]|
| PATCH     |  /users  | 更新用户信息|