#### TMS对接，接口整理

---

##### 1. 订单、费用同步接口

- **`说明`**：

  同步tms所有费用未确定的订单、费用详情、账单信息，每天同步一次。

- **`注意事项`**:

  财务系统采用被动接受数据的方式，发送方在发送前，将发送的数据记录备份，接受方在数据接收后同步前也需将数据记录备份；

  数据发送方，采用增量的方式来发送数据（只发送修改过的数据，未修改的数据不予发送）

  财务系统因各种原因不能接收数据导致的无法同步，则此次数据推迟到下一次同步； 

- **`URI`**：待定

- **`Method`**： POST

- **`Content-Type`**：application/json

- **`Body`**：

~~~json
{
  "order": [
    {
      /* 单据编号 String not null */
      "OrderCode": "",
     	/* 任务号，多个任务号用;（英文分号）分割  String null */ 
      "taskCodes": "",
      /* 提运单号 String not null */
      "waybillCode": "",
      /* 接单客户Id Integer null */
      "customerId": 0,
      /* 接单类型 String null 
      	可选值：[
          ORDER_TYPE_IMPORT, 	//进口
          ORDER_TYPE_EXPORT,	//出口
          ORDER_TYPE_ENTRY,		//进境
          ORDER_TYPE_LEAVE		//出境
      	]  */
      "orderType": "",
      /* 运输方式 String null 
        可选值： [
        	TRANSPORT_TYPE_SHIP,	//海运
        	TRANSPORT_TYPE_AIR,		//空运
        	TRANSPORT_TYPE_LAND		//陆运
        ] */
      "transportType": "",
      /* 接单时间 String yyyy-MM-dd HH:mm:ss not null */
      "orderReceiveDate": "",
      /* 单据来源，请填写"ORDER_TMS" */
      "orderFrom": "ORDER_TMS"
    }
  ],
  "fee": [
    {
      /* 单据编号  String not null */
      "OrderCode": "",
      /* 任务号 String not null */
      "taskCode": "",
      /* 费用ID 字段类型再商量 */
      "feeId": "",
      /* 费用类型/名称（根据费用字典查询费用编码，字典后续提供） Integer not null */
      "feeType": "",
      /* 金额 Double null */
      "money": 0,
      /* 币种 String null */
      "currencyType": "",
      /* 汇率 Double null */
      "exchangeRate": 0,
      /* 金额-人民币 Double not null  */
      "RMBMoney": 0,
      /* 费用操作类型 String not null
        可选值：[
          FEE_OPTION_PAY,			//应付
          FEE_OPTION_RECEIVE	//应收
        ] */
      "feeOptionType": "",
      /* 费用所属部门 Integer not null not 0 */
      "feeBelongDeptId": 0,
      /* 支付方 类型 String not null
        可选值：[
        	PAYER_TYPE_SUPPLIER,	//供应商
        	PAYER_TYPE_CUSTOMER,	//客户
        	PAYER_TYPE_DEPARTMENT	//公司内部部门
        ]*/
      "payerType": "",
      /* 账单号 String not null */
      "BillCode": "",
      /* 备注 String not null */
      "remark": "",
      /* 费用状态 String not null
        可选值：[
        	STATUS_DEL,		//删除
        	STATUS_NORMAL	//正常
        ]*/
      "status": "",
      /* 费用创建人Id 类型暂定 */
      "feeCreatorId": "",
      /* 费用创建时间 String yyyy-MM-dd HH:mm:ss not null */
      "feeCreateDate": "",
      /* 费用最后修改人Id 类型暂定 */
      "feeModifierId": "",
      /* 费用最后修改时间 String yyyy-MM-dd HH:mm:ss not null*/
      "feeModifyDate": "",
    }
  ]
}
~~~

- **`返回结果`**：

~~~json
/* success */
{
  "code": 0,
  "errmsg": ""
}

/* fail */
{
  /* 
    code 可以有以下值，可能会增加： [
      400,	//请求的数据有误，校验不通过，如非空字段却未包含
      500,  //数据同步时出错
    ] */
  "code": 500,
  "errmsg": "这里是具体的失败原因，如数据校验不通过、数据不完整、同步时逻辑错误等等"
}
~~~





##### 2. 应收账单，客户已确定费用，订单、费用同步接口

- **`说明`**：

  当客户确定费用时，将对应的费用、账单、订单数据推送给财务系统进行同步。

- **`注意事项`**：

  **若同步失败了的方案？**

  数据发送方，数据接收方都需要做数据记录

- **`URI`**：待定

- **`Method`**： POST

- **`Content-Type`**：application/json

- **`Body`**：

~~~JSON
/* 请参考上一个接口的 body，字段类型基本一致，下面的是新增的字段 */
{
  "order": [
    { 
  	}
  ],
  "fee": [
    {
  	}
  ]
}

~~~


- **`返回结果`**：

~~~json
/* success */
{
  "code": 0,
  "errmsg": ""
}

/* fail */
{
  /* 
    code 可以有以下值，可能会增加： [
      400,	//请求的数据有误，校验不通过，如非空字段却未包含
      500,  //数据同步时出错
    ] */
  "code": 500,
  "errmsg": "这里是具体的失败原因，如数据校验不通过、数据不完整、同步时逻辑错误等等"
}
~~~





##### 3. 发起付款流程接口

> https://emhq5w.axshare.com/#g=1&p=%E5%BA%94%E4%BB%98%E4%BE%9B%E5%BA%94%E5%95%86%E8%B4%A6%E5%8D%95%E5%88%97%E8%A1%A8

- **`说明`**：

  当需要发起付款流程时，由业务线填写付款表单，提交后请求财务系统，财务系统自动发起付款流程。

- **`注意事项`**:

   

- **`URI`**：待定

- **`Method`**： POST

- **`Content-Type`**：application/json

- **`Body`**：

~~~json
{
  
}
~~~












