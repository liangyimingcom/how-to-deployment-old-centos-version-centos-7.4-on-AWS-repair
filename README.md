
# how-to-deployment-old-centos-version-centos-7.4-on-AWS-repair

## 如何在AWS全球region中，找到旧版本的官方centos 7.4，并创建EC2

[![image](https://user-images.githubusercontent.com/32609181/111964153-427acd00-8b2f-11eb-9488-ed7c88fb675c.png)](https://user-images.githubusercontent.com/32609181/111964153-427acd00-8b2f-11eb-9488-ed7c88fb675c.png)

# 

### 1-2）使用命令行列出仓库中的全部centos版本：

| 2018-05-17T08:59:21.000Z| CentOS Linux 7 x86_64 HVM EBS ENA 1804_2-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-55a2322a.4 | ami-d5bf2caa |
| 2018-04-04T00:06:30.000Z| CentOS Linux 7 x86_64 HVM EBS ENA 1803_01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-8274d6ff.4 | ami-b81dbfc5 |
| 2017-12-05T14:46:53.000Z| CentOS Linux 7 x86_64 HVM EBS 1708_11.01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-95096eef.4 | ami-02e98f78 |

### 2）用关键字在 makrplace 中搜索老版本centos

CentOS Linux 7 x86_64 HVM EBS 1708_11.01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-95096eef.4

【CentOS Linux 7 x86_64 HVM EBS 1708_11.01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-95096eef.4 (ami-82a3eaed)】

### 3）版本查看：

ssh -i "temp01.pem" [centos@ec2-3-7-59-106.ap-south-1.compute.amazonaws.com](mailto:centos@ec2-3-7-59-106.ap-south-1.compute.amazonaws.com)
cat /etc/redhat-release
cat /proc/version

[centos@ip-172-31-42-210 ~]$ cat /etc/redhat-release
CentOS Linux release 7.4.1708 (Core)
[centos@ip-172-31-42-210 ~]$
[centos@ip-172-31-42-210 ~]$ cat /proc/version
Linux version 3.10.0-693.5.2.el7.x86_64 ([builder@kbuilder.dev.centos.org](mailto:builder@kbuilder.dev.centos.org)) (gcc version 4.8.5 20150623 (Red Hat 4.8.5-16) (GCC) ) #1 SMP Fri Oct 20 20:32:50 UTC 2017
[centos@ip-172-31-42-210 ~]$

### 附：

https://wiki.centos.org/Cloud/AWS
