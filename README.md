# how-to-deployment-old-centos-version-centos-7.4-on-AWS-repair



how-to-deployment-old-centos-version-centos-7.x-on-AWS-repair

感觉之前的的不清楚，重新写一遍步骤：



## 1、先确认你要在哪一个区域创建老版本的Cent OS，比如印度孟买=ap-south-1





## 2、使用AWS CLI搜索这个区域的image，命令行如下：

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



## 3、获得了清单，但是里面看不到CentOS版本号。

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



## 4、我们尝试一个centos 的老版本，创建《ami-82a3eaed》的EC2，即：

方法如下：

用关键字在 makrplace 中搜索老版本centos：

CentOS Linux 7 x86_64 HVM EBS 1708_11.01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-95096eef.4

 

![image-20210621175529596](https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210621175529596.png)

【CentOS Linux 7 x86_64 HVM EBS 1708_11.01-b7ee8a69-ee97-4a49-9e68-afaee216db2e-ami-95096eef.4 (ami-82a3eaed)】



## 5、检验版本，看看是不是centos-7.4？

版本查看：

ssh -i "temp01.pem" centos@ec2-3-7-59-106.ap-south-1.compute.amazonaws.com

cat /etc/redhat-release

cat /proc/version

![image-20210621175609704](https://raw.githubusercontent.com/liangyimingcom/storage/master/uPic/image-20210621175609704.png)



## 6、centos-7.4创建成功了，有centos-7.6/7.8版本吗？ 请尝试以下的版本，谢谢。



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









