---
description: >-
  This is a step-by-step guide for setting up GPU-based Spark with Nvidia Rapids
  on AWS EC2.
---

# Spark3 GPU Setup with Nvidia Rapidsai on AWS EC2

## Step 1 - Launch an EC2 Instance on AWS

* [x] Select Deep Learning AMI while you are in eu-west-2 region.

![AWS AMI Selection](<.gitbook/assets/image (4).png>)

* [x] Select p3.2xlarge instance type and click Next.

![](.gitbook/assets/image.png)

* [x] 1 - Click "Configure Security Group" on the navigation bar.&#x20;
* [x] 2 - Select "All Traffic" in the rule section then click "Review and Launch".&#x20;

![](<.gitbook/assets/image (1).png>)

* [x] Click ""Launch"

![](<.gitbook/assets/image (3).png>)

### Reference Repository:

{% embed url="https://github.com/NVIDIA/spark-rapids-examples" %}
