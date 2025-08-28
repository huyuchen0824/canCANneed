# Intro
canCANneed(以下缩写为CCN), 为适应新型需求的通信协议，上位替代CAN.
# 物理层
## 1 物理层电平
CCN采用差分线传输，包含H,L两根物理线材.对于同一个网络上的多个CCN节点，所有节点的H端相连，所有节点的L端相连，不允许不同节点之间交换H,L端口的连接。
CCN物理层支持下列几种情况:
|H|L|CASE|
|---|---|---|
|+12V|-12V|A|
|0V|0V|B|
|-12V|+12V|C|
|浮空|浮空|节点断开连接|
## 2 信号编码方式
CCN 采用 4-State-Circular NRZ-I 编码。4个State对应物理层的CASE为：\[B,A,B,C\].规定B->A->B->C序列为顺时针循环.当CCN遇到数据0时，State保持不变；当CCN遇到数据1时，按照顺时针方向切换到下一个State.
## 3 CCN总线速率
规定 CCN-25 即 25Msymbol/second.即, 每个Data持续40ns. 
注意，CCN V0.1 仅支持 CCN-25速率。
# 数据链路层
## 1 CCN总线帧格式/类型
CCN V0.1 仅支持1种帧格式/类型.
## 2 CCN 帧结构
| 字段    | 位数   | 说明  |
| ----- | ------ | ------------------------- |
| 前导    | 3 bit  | 固定3'b111, 用于时钟同步|
| 有效负载  | 64 bit | 8Byte 传感器/控制数据|
| SECDED ECC | 8 bit  | 覆盖64bit 负载，实现1bit纠错，2bit检出 |
|ACK|3bit|主机复位并浮空，从机上报接收情况|
### 前导段
表示该帧的起始，数据值固定为3'b111.通过连续的电平翻转进行时钟同步。
### payload
负载段，64bit数据
### ECC
对已经传输完成的64bit数据段增加SECDED-ECC校验.
### ACK.
ACK段的功能相对复杂.若此时发送节点处于CaseB,则下1bit发送节点Tx端浮空；若此时发送节点处于CaseA或CaseC, 则先用 
|ECC bit8|ACKbit1|ACKbit2|ACKbit3|
|---|---|---|---|
|CaseB|发送节点Tx浮空|-|-|
|CaseA/C|CaseB|发送节点Tx浮空|-|
|从机Tx浮空|从机ECC校验计算|从机ECC校验计算|从机返回ACK|
### 1 帧起始(SOF)

