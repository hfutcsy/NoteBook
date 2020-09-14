# 以太帧
在以太网链路上的数据包称作以太帧。以太帧起始部分由前导码和帧开始符组成。后面紧跟着一个以太网报头，以MAC地址说明目的地址和源地址。帧的中部是该帧负载的包含其他协议报头的数据包(例如IP协议)。以太帧由一个32位冗余校验码结尾。它用于检验数据传输是否出现损坏。

![frame.png](https://raw.githubusercontent.com/hfutcsy/NoteBook/master/Assets/frame.PNG)

## Reference
* <https://zh.wikipedia.org/wiki/%E4%BB%A5%E5%A4%AA%E7%BD%91%E5%B8%A7%E6%A0%BC%E5%BC%8F>
* [WireShark 无法抓取以太帧前序和FCS或出现IP报头校验和错误 -- 原因](https://blog.csdn.net/yetugeng/article/details/100514693)