# Deploy Azure Iot Edge (Preview) on a Red Hat 7.2 VM in Azure 
This article explains the steps to take when deploying the current preview version of the Azure IoT Edge. The current deployment set and documentation is not prepared for Red Hat 7 and therefore a few small adjustments need to be made to succesfully install IoT Edge in this configuration. The generic steps can be found in the [linux quickstart](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux).

## Prepare a Red Hat 7.2 VM in Azure
** These steps replace the Prerequisites steps of the [linux quickstart](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux#prerequisites).<br>
You can use the normal steps in Azure to deploy a Red Hat 7.2 VM [Create a Linux virtual machine with the Azure portal](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal). I've used the 'Red Hat Enterprise Linux 7.2 - Pay-As-You-Go Premium' image. Once you've deployed the VM, login using ssh and execute the following steps:
1.  Execute all steps as root: <br>
    `sudo su -` <br>
2.  Install Python version 2.7.14: <br>
    a.  Install GCC and Python 2.7.14: <br>
        `yum install gcc openssl-devel bzip2-devel` <br>
        `cd /usr/src` <br>
        `wget https://www.python.org/ftp/python/2.7.14/Python-2.7.14.tgz` <br>
        `tar xzf Python-2.7.14.tgz` <br>
        `cd Python-2.7.14` <br>
        `./configure --enable-optimizations` <br>
        `make altinstall` <br>
    b.  Check Python version: <br>
        `python2.7 -V` <br>
2.  Install Python pip, to install the IoT Edge runtime: <br>
    a. Install pip: <br>
        `wget https://bootstrap.pypa.io/get-pip.py` <br>
        `python2.7 get-pip.py` <br>
    c.  Check if pip was installed correctly: <br>
        `pip --version` <br>
3.  Install Docker-CE for Linux and make sure that it's running using the [CentOS setup](https://docs.docker.com/install/linux/docker-ce/centos/)

## Install Azure IoT Edge (Preview)
Once these steps have been executed correctly you can then install IoT Edge on Red Hat 7.2 as describe in [Install and start the IoT Edge runtime](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux#install-and-start-the-iot-edge-runtime). Execute all steps as root `sudo su -`. <br>

## Deploy a module to the IoT Edge
Once the Iot Edge is deployed and running on Red Hat 7.2 you can deploy a module as described in the [linux quickstart](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux#deploy-a-module).
