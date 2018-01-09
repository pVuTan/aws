# Install and Run R Server
## Documentation

*Objective: Install and Run R Server*

### Parameters:
1.	AMI: Amazon Linux AMI 2017.09.1 (HVM), SSD Volume Type - ami-1a962263
2.	Instance Type – t2.medium
    - RStudio recommends a minimum of 2 core / 4GB RAM for its server to support one analyst who performs testing and sandboxing.
    - Can possibly earn a few CPU credits to allow for performance burst. I do not expect it to earn lots of credits as I intend to shut it down after every use.
3.	Instance Details:
    - Network: RosettaHub VPC
    - Auto-assign Public IP – Enable
    - Create new subnet for R Server installation
    - Other settings kept as default
    - T2 Unlimited not enabled. Will observe performance before enabling
4.	 Advanced Details
```
#!/bin/bash
#install R
yum install -y R

#download and install RStudio-Server 1.1.383 (release: 2017-10-09)
wget https://download2.rstudio.org/rstudio-server-rhel-1.1.383-x86_64.rpm
yum install -y --nogpgcheck rstudio-server-rhel-1.1.383-x86_64.rpm
rm rstudio-server-rhel-1.1.383-x86_64.rpm

#add user(s)
useradd ****
echo ****:******** | chpasswd

```
5.	Storage: 20GB
6.	Tag -> Name: R Server
7.	Security Group
    - Opened SSH port 22 and HTTP port 80
    - Added port 8787 – for RStudio Server
8.	Re-used RosettaHub Key Pair

### R Studio Server AMI
I came across a R Studio Server AMI found in Community AMI. It is maintained by Louis Aslett with pre-installed R, RStudio Server, Julia and CUDA. I plan to use this AMI for future R needs to reduce set-up time and cost.

### References:
- https://aws.amazon.com/blogs/big-data/running-r-on-aws/
- http://strimas.com/r/rstudio-cloud-1/
- http://www.louisaslett.com/RStudio_AMI/
- https://www.rstudio.com/products/rstudio/download-server/


