# Spark3 GPU Setup with Nvidia Rapidsai on AWS EC2

This is a step-by-step guide for setting up GPU-based Spark with Nvidia Rapids on AWS EC2.

## Step 1 - Launch an EC2 Instance on AWS

* [x] Select Deep Learning AMI while you are in eu-west-2 region.

![AWS AMI Selection](<.gitbook/assets/image (4).png>)



* [x] Choose p3.2xlarge instance type and click Next.

![Choose and Instance Type](.gitbook/assets/image.png)



* [x] 1 - Click "Configure Security Group" on the navigation bar.&#x20;
* [x] 2 - Choose "All Traffic" in the rule section then click "Review and Launch".&#x20;

![Configure Security Group](<.gitbook/assets/image (1).png>)



* [x] Now you can Launch your instance with your key-pair. If you need further information about launching EC2 instance, please visit [https://aws.amazon.com/ec2/getting-started/](https://aws.amazon.com/ec2/getting-started/)

## &#x20;Step 2 - Setup Spark3 on EC2

First, connect to your EC2 instance which we launched in the previous step.

* [x] Change the owner of the /opt directory then go to /opt.

```
sudo chown -R ubuntu:ubuntu /opt
cd /opt
```

* [x] Download Spark3 and extract the files. (We will use 3.2.1 version. If the link does not work, find a proper download link from [https://spark.apache.org](https://spark.apache.org))

```
wget https://dlcdn.apache.org/spark/spark-3.2.1/spark-3.2.1-bin-hadoop3.2.tgz

tar -xvf spark-3.2.1-bin-hadoop3.2.tgz

#You can remove the tgz file after extracting the files.
rm spark-3.2.1-bin-hadoop3.2.tgz
```

* [x] Add Spark Home into bashrc file.

```
#1-Open bashrc file of your user.
nano ~/.bashrc

#2-Add the following lines and save the file.

#SPARK3
export SPARK_HOME=/opt/spark-3.2.1-bin-hadoop3.2
export PYSPARK_PYTHON=/usr/bin/python3

#3-Source bashrc.
source ~/.bashrc
```

* [ ] Add some GPU configurations into the config file of Spark.

```
cd ${SPARK_HOME}/conf

cp spark-env-sh.template spark-env-sh

nano spark-env-sh

#Add the following lines and save the file.


```



### Reference Repository:

{% embed url="https://github.com/NVIDIA/spark-rapids-examples" %}
