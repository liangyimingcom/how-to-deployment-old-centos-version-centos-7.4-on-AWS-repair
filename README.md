# how-to-deployment-old-centos-version-centos-7.4-on-AWS-repair / 如何在AWS全球region中，找到旧版本的官方centos 7.4，并创建EC2


## 2024年12月的更新版本：
1）用这个链接，用标准方式创建：

https://us-east-2.console.aws.amazon.com/ec2/home?region=us-east-2#LaunchInstances:ami=ami-05a36e1502605b4aa;product=d9a3032a-921c-4c6d-b150-bde168105e42

2）创建成功后：AMI location
aws-marketplace/CentOS-7-2111-20220825_1.x86_64-d9a3032a-921c-4c6d-b150-bde168105e42

3）最后的版本我开机检查过了，版本是：CentOS Linux release 7.9.2009 (Core)

4）centos7免费的AMI地址：https://aws.amazon.com/marketplace/pp/prodview-foff247vr2zfw
直接在这个页面点击订阅，然后开启EC2就好用。


--- 
how-to-deployment-old-centos-version-centos-7.x-on-AWS-repair 感觉之前的的不清楚，重新写一遍步骤：

### 1、先确认你要在哪一个区域创建老版本的Cent OS

 比如印度孟买=ap-south-1





### 2、使用AWS CLI搜索这个区域的image，命令行如下：

~~~bash
aws ec2 describe-images \
      --owners aws-marketplace \
      --filters Name=product-code,Values=aw0evgkw8e5c1q413zgy5pjce \
      --query 'Images[*].[CreationDate,Name,ImageId]' \
      --filters "Name=name,Values=CentOS Linux 7*" \
      --region ap-south-1 \
      --output table \
  | sort -r
~~~

搜索结果如下：

![image-20210621174946104](https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210621174946104.png)





### 3、获得了清单，但是里面看不到CentOS版本号。

1. | 2020-03-09T21:54:49.000Z | CentOS Linux 7 x86_64 HVM EBS ENA 2002_01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-0042af67f8e4dcc20.4 | ami-026f33d38b6410e30 |
   | ------------------------ | ------------------------------------------------------------ | --------------------- |
   |                          |                                                              |                       |

2. | 2019-01-30T23:45:21.000Z | CentOS Linux 7 x86_64 HVM EBS ENA 1901_01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-05713873c6794f575.4 | ami-02e60be79e78fef21 |
   | ------------------------ | ------------------------------------------------------------ | --------------------- |
   |                          |                                                              |                       |

3. | 2018-06-13T15:58:26.000Z | CentOS Linux 7 x86_64 HVM EBS ENA 1805_01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-77ec9308.4 | ami-1780a878 |
   | ------------------------ | ------------------------------------------------------------ | ------------ |
   |                          |                                                              |              |

4. | 2018-05-17T09:04:41.000Z | CentOS Linux 7 x86_64 HVM EBS ENA 1804_2-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-55a2322a.4 | ami-48301d27 |
   | ------------------------ | ------------------------------------------------------------ | ------------ |
   |                          |                                                              |              |

5. | 2018-04-04T00:12:19.000Z | CentOS Linux 7 x86_64 HVM EBS ENA 1803_01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-8274d6ff.4 | ami-2014314f |
   | ------------------------ | ------------------------------------------------------------ | ------------ |
   |                          |                                                              |              |

6. | 2017-12-05T14:48:48.000Z | CentOS Linux 7 x86_64 HVM EBS 1708_11.01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-95096eef.4 | ami-82a3eaed |
   | ------------------------ | ------------------------------------------------------------ | ------------ |
   |                          |                                                              |              |





### 4、我们尝试一个centos 的老版本，创建《ami-82a3eaed》的EC2，即：

方法如下：

用关键字在 makrplace 中搜索老版本centos：

CentOS Linux 7 x86_64 HVM EBS 1708_11.01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-95096eef.4

 

![image-20210621175529596](https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210621175529596.png)

【CentOS Linux 7 x86_64 HVM EBS 1708_11.01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-95096eef.4 (ami-82a3eaed)】





### 5、检验版本，看看是不是centos-7.4？

版本查看：

ssh -i "temp01.pem" centos@ec2-3-7-59-106.ap-south-1.compute.amazonaws.com

cat /etc/redhat-release

cat /proc/version

![image-20210621175609704](https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210621175609704.png)





### 6、centos-7.4创建成功了，有centos-7.6/7.8版本吗？ 请尝试以下的版本，谢谢。



1. | 2020-03-09T21:54:49.000Z | CentOS Linux 7 x86_64 HVM EBS ENA 2002_01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-0042af67f8e4dcc20.4 | ami-026f33d38b6410e30 |
   | ------------------------ | ------------------------------------------------------------ | --------------------- |
   |                          |                                                              |                       |

2. | 2019-01-30T23:45:21.000Z | CentOS Linux 7 x86_64 HVM EBS ENA 1901_01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-05713873c6794f575.4 | ami-02e60be79e78fef21 |
   | ------------------------ | ------------------------------------------------------------ | --------------------- |
   |                          |                                                              |                       |

3. | 2018-06-13T15:58:26.000Z | CentOS Linux 7 x86_64 HVM EBS ENA 1805_01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-77ec9308.4 | ami-1780a878 |
   | ------------------------ | ------------------------------------------------------------ | ------------ |
   |                          |                                                              |              |

4. | 2018-05-17T09:04:41.000Z | CentOS Linux 7 x86_64 HVM EBS ENA 1804_2-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-55a2322a.4 | ami-48301d27 |
   | ------------------------ | ------------------------------------------------------------ | ------------ |
   |                          |                                                              |              |

5. | 2018-04-04T00:12:19.000Z | CentOS Linux 7 x86_64 HVM EBS ENA 1803_01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-8274d6ff.4 | ami-201431 |
   | ------------------------ | ------------------------------------------------------------ | ---------- |









附录：https://wiki.centos.org/Cloud/AWS






## 中国区的centos 7.6版本

CentOS 7.6.1810-Linux version 3.10.0-957.1.3.el7.x86_64 = ami-0d8487330873f710c
CentOS 7.6.1810-Linux version 3.10.0-957.1.3.el7.x86_64 ,  AMI NAME = ami-0d8487330873f710c
Linux version 3.10.0-957.1.3.el7.x86_64 (mockbuild@kbuilder.bsys.centos.org) (gcc version 4.8.5 20150623 (Red Hat 4.8.5-36) (GCC) ) #1 SMP Thu Nov 29 14:49:43 UTC 2018

<img width="820" alt="image" src="https://user-images.githubusercontent.com/32609181/204427111-6f5383fe-e56b-44c8-8637-b273640e12f7.png">

![image](https://user-images.githubusercontent.com/32609181/204427137-12ad8d3c-eb90-4f40-a232-fb48b40a2b80.png)
最近有许多同事问CentOS 7.6，这个1901_01就是CentOS 7.6,请知晓￼


 
 ## 中国区的centos 8.0 版本

<img width="772" alt="image" src="https://user-images.githubusercontent.com/32609181/204451743-a7ca88f4-bc0a-40b6-85d8-7cb8c041da59.png">

<img width="828" alt="image" src="https://user-images.githubusercontent.com/32609181/204451759-9ed05eba-fb70-49e5-843e-0c5e60d11edb.png">

结论：
centos8 - 4.18.0-348.7.1.el8_5.x86_64 = ami-0cf85527e94362217

$ uname -r
4.18.0-348.7.1.el8_5.x86_64




