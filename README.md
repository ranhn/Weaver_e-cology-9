# Weaver_e-cology-9
泛微e-cology-9存在任意金额数量修改等支付逻辑漏洞

漏洞地址：https://oa.xxxxxxx.cn/spa/workflow/static4form/index.html?

漏洞描述：本公司采购的泛微e-cology-9系统，在测试中，发现该系统在积分兑换页面可以随意修改金额、数量、以及给自己下发任意积分等支付逻辑漏洞。

漏洞详情：

1，点击文化积分兑换周边申请。
![image](https://github.com/user-attachments/assets/53ee0fa1-8348-4437-a79a-3dc23f231a4a)

2，当前个人积分为0，点击提交，此时会校验个人积分以及库存数量。
![image](https://github.com/user-attachments/assets/2d39d537-b076-462e-a012-3bdf1a7d8633)

3，使用burpsuite抓包拦截，修改响应，成功，此时积分为负数。
![image](https://github.com/user-attachments/assets/669a4fb9-507e-43b1-a60d-b8d70d318ef8)
![image](https://github.com/user-attachments/assets/bcea71c0-4c67-4252-804a-183af8537459)

4，同理，还可以在数据包中修改自己的个人积分，成功。
![image](https://github.com/user-attachments/assets/aa833283-fec0-42b4-a895-bc70661ff99f)

漏洞版本：e-cology-9 9.00.2104.07
![image](https://github.com/user-attachments/assets/9fa4f2de-7a50-4d4f-b7d0-0af430c79b1b)

修复建议：
1、后端检查每一项值，包括支付状态。

2、校验价格、数量参数，比如产品数量只能为正整数，并限制购买数量。

3、与第三方支付平台做检查，实际支付的金额是否与订单金额一致。

4、支付参数进行加密、解密、数字签名及验证，这个可以有效的避免数据修改，重放攻击中的各种问题。

