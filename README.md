# Deploy Azure Iot Edge on a Red Het 7.2 VM in Azure 
This article explains the steps to take when deploying the current preview version of the Azure IoT Edge. The current deployment set and documentation is not prepared for Red Hat 7 and therefore a few small adjustments need to be made to succesfully install IoT Edge in this configuration. The generic steps can be found in the [linux quickstart](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux).

## Prepare a Red Hat 7.2 VM in Azure
** These steps replace the Prerequisites steps of the [linux quickstart](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux#prerequisites).
You can use the normal steps in Azure to deploy a Red Hat 7.2 VM [Create a Linux virtual machine with the Azure portal](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal). I've used the 'Red Hat Enterprise Linux 7.2 - Pay-As-You-Go Premium' image. Once you've deployed the VM, login using ssh and execute the following steps:
1.  Update yum: `sudo yum update`. This will take a few minutes.
2.  Install Python pip, to install the IoT Edge runtime: `sudo yum install python-pip`
3.  Install Docker-CE for Linux and make sure that it's running using the [CentOS setup](https://docs.docker.com/install/linux/docker-ce/centos/)
