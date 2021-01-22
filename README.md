# 支付代付接口文档

**文档属性**

版本号∶ v1.4
更新日期 ∶ 2020-01-01

# 代付对接文档

## 1. 下单接口说明
代付通过下单接口直接返回订单对应JSON数据。

### 1.1 请求方式
POST

### 1.2 请求网关地址
正式请求地址请联系年轻帅气的系统管理员获取 
https://api.xxxxx.com/lpay/agentpay/gateway

### 1.3 下单参数说明
### 参数说明 Tables

| 参数        | 参数名称   |  类型(长 度) |参数说明 |是否必填
| --------   | -----:  | :----:  |:----:  |:----:  |
| mch_id    | 商户号  |  String(5)     |签约商户的商户号|是
|out_trade_no|商户订单 号| String(24)| 合作商户唯一的订单号。| 是
|total_fee |交易金额 |String(24) |总金额，以分为单位，不允许 包含任何字、符号。| 是
|pay_type |支付类型 |String(2)| 86:代付；| 是
|body |商品名称| String| 商品标题/交易标题/订单标题/ 订单关键字等。 |是
|bank_account| 收款人账 号 |String |收款人账号。 |是 
|account_holder |收款人姓 名| String |收款人姓名。 |是 
|deposit_bank_code| 开户行代 码 |String |开户行代码。|参照附录 |是 
|deposit_bank |开户行名 称| String |开户行名称。|参照附录 |是 
|acct_type |渠道类型 |String |1对私;2对公。 |是 
|account_holder_mobile |开户人手 机号| String |开户人手机号。必填但是不是 必须正确 |是 
|province |开户行所 属省份| String |开户行所属省份号。必填但是 不是必须正确 |是 
|city |开户行所 属城市| String |开户行所属城市。必填但是不 是必须正确 |是 
|sub_branch |开户支行 名称| String |开户支行名称。必填但是不是 必须正确| 是 
|account_holder_id| 开户人身 份证号| String |开户人身份证号。必填但是不 是必须正确| 是 
|sign |签名 |String(32)| 对支付信息使用MD5签名。| 是


First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell
