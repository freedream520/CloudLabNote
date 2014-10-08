# SSH免密码登陆设置

作者 : 马超 mctt90@gmail.com

---

根据公钥加密的思想,如果机器A想无密码登陆到其他机器,只需要在自己机器上生成一对公钥和密钥,然后把密钥给这N台机器,这样,这机器有了A的公钥接可以解密A的数据包,跟A正常通信了.
<br>
通常在一个集群中,我们会选择一台机器作为跳板机,在这台机器上登陆到其他机器,因此,需要在跳板机上生成一对公钥和密钥.一般而言,我们也会把跳板机作为整个集群的Master, 例如Hadoop的NameNode.

下面详细讲解如何配置从跳板机SSH无密码登陆到所有机器.

### 前提: 修改hosts文件

**1. 在master上生成一对公钥和密钥** <br><br>
```bash
ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa
```
<br>

**将公钥拷贝到其他机器** <br><br>
```bash
scp ~/.ssh/id_dsa.pub alex@worker01:~
ssh worker01
mkdir .ssh
cat id_dsa.pub >> .ssh/authorized_keys
```
