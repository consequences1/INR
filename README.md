# 印度支付通道对接文档


## 目录

- [H5支付下单接口](#H5支付下单接口)
- [代付接口](#代付对接文档)


**文档属性**

版本号∶ v1.4
更新日期 ∶ 2020-01-01
# H5支付下单接口
## 1. 下单接口说明
H5支付通过浏览器或者APP的Webview直接跳转到生成支付信息URL的方式直接调起支付。
## 1.1 请求方式 
get方法
浏览器或者Webview跳转
##1.2 请求网关地址
找管理员获取支付下单网关地址

# 代付接口

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
|bank_account| 收款人账 号 |String |收款人银行账号或者UPI， ID。 |是 
|account_holder |收款人姓 名| String |收款人姓名。 |是 
|deposit_bank_code| 开户行代 码 |String |开户行代码。必填但是 不是必须正确，没有可随便填写|是
|deposit_bank |开户行名 称| String |开户行名称。必填但是 不是必须正确，没有可随便填写|是
|acct_type |转账类型 |String |bank：银行账户，wallet：用户钱包，upi用户传upi。 |是 
|account_holder_mobile |开户人手 机号| String |开户人手机号。必填但是不是 必须正确 |是 
|province |开户行所 属省份| String |开户行所属省份号。必填但是 不是必须正确，没有可随便填写 |是 
|city |开户行所 属城市| String |开户行所属城市。必填但是 不是必须正确，没有可随便填写 |是 
|sub_branch |收款方IFSC| String |收款方IFSC，印度银行卡代付必须填正确的(IFSC)| 是 
|account_holder_id| 收款方邮箱| String |收款方邮箱| 是 
|sign |签名 |String(32)| 对支付信息使用MD5签名。| 是


## 2. 接入步骤
### 2.1 生成订单MD5签名
```html
订单信息（商户订单号+交易金额+收款人账号+收款人姓名+开户行名称+开户人手机号 +商户号+商户秘钥）进行UTF-8编码的MD5编码。
订单信息（out_trade_no+total_fee+bank_account+account_holder+deposit_bank+account_holder_mobile+user_mch_id+商户秘钥）进行UTF-8编码的MD5编码。
备注：直接字符串拼接不包符号 “+”
```
### 2.2 请求支付网关接口
1.使用POST方式请求网关，传递参数如下
```html
sign=XXX
mch_id=XXXX
out_trade_no=XXXXX
total fee=XxxXXX
pay_type=XX
body=XXXXXXX
```
`备注：普通表单提交数据,非JSON数据}`

2.接收返回JSON数据，数据如下∶
JSON数据说明
| 参数        | 参数名称   |  类型(长 度) |参数说明 |是否必填
| --------   | -----:  | :----:  |:----  |:----:  |
|result_code |结果代码 |Int |0：订单成功； 1：订单失败； 此处返回的是代付订单提交是否成功状态，不是 代付打款是否成功，代付是否成功通过代付查询 接口，或者是异步回调获取| 是 
|err_msg| 错误信息 |String(256) |result_code=1时传递错误信息| 否 
|out_trade_no| 商户订单号| String(24) |合作商户唯一的订单号。 |是 
|transaction_id |平台订单号| String(24) |平台订单号。| 是


实例数据
```html
{  
  out_trade_no: "8000120170912170755", 
  transaction_id: "80001c868000120170912170755",  
  result_code: 0  
} 
```
