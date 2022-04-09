# Spark3 GPU Setup and Applications with Nvidia Rapidsai on AWS EC2

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
#Step1 - Open bashrc file of your user.
nano ~/.bashrc

#Step2 - Add the following lines and save the file.

#SPARK3
export SPARK_HOME=/opt/spark-3.2.1-bin-hadoop3.2
export PYSPARK_PYTHON=/usr/bin/python3

#Step3 - Source bashrc.
source ~/.bashrc
```

* [x] Add some GPU configurations into the config file of Spark.

```
#Step1 - Go to Spark config directory.
cd ${SPARK_HOME}/conf

#Step2 - Create sh file from the template.
cp spark-defaults.conf.template spark-defaults.conf

#Step3 - Open the file.
nano spark-defaults.conf

#Step4 - Add the following lines and save the file.

spark.worker.resource.gpu.amount  1
spark.worker.resource.gpu.discoveryScript /opt/spark-3.2.1-bin-hadoop3.2/examples/src/main/scripts/getGpusResources$

```

* [x] Start Spark Master and Spark Worker.

```
$SPARK_HOME/sbin/start-master.sh
$SPARK_HOME/sbin/start-slave.sh spark://$HOSTNAME:7077
```

## Step 3 - Download Necessary Jar Files

Cuda, Rapid, and XGboost drivers are necessary to be able to execute the GPU applications whşch we will see in the next steps.

* [x] Create an application directory.

```
mkdir /opt/xgboost
```

* [x] Download Jar Files in the application directory.

```
#Go to the application directory.
cd /opt/xgboost

#CUDA
wget https://repo1.maven.org/maven2/ai/rapids/cudf/22.02.0/cudf-22.02.0-cuda11.jar

#RAPIDS
wget https://repo1.maven.org/maven2/com/nvidia/rapids-4-spark_2.12/22.02.0/rapids-4-spark_2.12-22.02.0.jar

#XGBOOST
wget https://repo1.maven.org/maven2/com/nvidia/xgboost4j_3.0/1.4.2-0.2.0/xgboost4j_3.0-1.4.2-0.2.0.jar

wget https://repo1.maven.org/maven2/com/nvidia/xgboost4j-spark_3.0/1.4.2-0.2.0/xgboost4j-spark_3.0-1.4.2-0.2.0.jar
```

## Step 4 - Download the Datasets and the Application Files.

We will use mortgage, agaricus and taxi datasets for XGboost examples. All datasets and jupyter notebooks are placed in this repository.&#x20;

* [x] Clone this repository to /opt/xgboost directory.

```
cd /opt/xgboost

git clone https://github.com/ozgunakin/spark3-gpu-nvidia-rapidsai-setup-on-aws-ec2.git

cd spark3-gpu-nvidia-rapidsai-setup-on-aws-ec2/dataset

#EXTRACT AGARICUS FILES
tar -xvf agaricus-small.tar

#EXTRACT MORTGATE FILES
tar -xvf mortgage-small-2.tar

#EXTRACT TAXI FILES
tar -xvf taxi-small.tar
```

## GPU Based XGBoost Applications

You can find notebooks for XGBoost applications designed by using three different datasets in the notebooks directory of the repository that we have downloaded in the previous section.

* [ ] Open Jupyter Notebook in /opt/xgboost directory.

```
```

####



### Reference Repository:

{% embed url="https://github.com/NVIDIA/spark-rapids-examples" %}
