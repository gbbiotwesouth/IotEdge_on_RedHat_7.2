# Deploy Azure Iot Edge (Preview) on a Red Hat 7.2 VM in Azure 
This article explains the steps to take when deploying the current preview version of the Azure IoT Edge. The current deployment set and documentation is not prepared for Red Hat 7 and therefore a few small adjustments need to be made to succesfully install IoT Edge in this configuration. The generic steps can be found in the [linux quickstart](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux).

## Prepare a Red Hat 7.2 VM in Azure
** These steps replace the Prerequisites steps of the [linux quickstart](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux#prerequisites).<br>
You can use the normal steps in Azure to deploy a Red Hat 7.2 VM [Create a Linux virtual machine with the Azure portal](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal). I've used the 'Red Hat Enterprise Linux 7.2 - Pay-As-You-Go Premium' image. Once you've deployed the VM, log in using ssh and execute the following steps:
1.  Update yum: `sudo yum update`. This will take a few minutes.
2.  Install Python pip, to install the IoT Edge runtime: <br>
    a.  Install the setup tools: <br>
        `wget https://pypi.python.org/packages/source/s/setuptools/setuptools-7.0.tar.gz --no-check-certificate` <br>
        `tar xzf setuptools-7.0.tar.gz` <br>
        `cd setuptools-7.0` <br>
        `sudo python setup.py install` <br>
    b.  Once the setup tools are installed you can install pip: <br>
        `wget https://bootstrap.pypa.io/get-pip.py` <br>
        `sudo python get-pip.py` <br>
    c.  Check if pip was installed correctly: <br>
        `pip --version` <br>
3.  Install Docker-CE for Linux and make sure that it's running using the [CentOS setup](https://docs.docker.com/install/linux/docker-ce/centos/)

## Install Azure IoT Edge (Preview)
Once these steps have been executed correctly you can then install IoT Edge on Red Hat 7.2 similar as describe in [Install and start the IoT Edge runtime](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux#install-and-start-the-iot-edge-runtime) steps, with some minor adjustments.
On the Red Hat VM run the following commands: 
1.  Download the IoT Edge control script: <br>
    `sudo pip install -U azure-iot-edge-runtime-ctl` <br>
2.  Edit the /usr/lib/python2.7/site-packages/edgectl/utils/certutil.py file to ensure it runs on Red Hat 7.2: <br>
    `sudo nano /usr/lib/python2.7/site-packages/edgectl/utils/certutil.py` <br>
    Go to line 530 and change `passphrase = None` into `passphrase = '<your passphrase>'`. The passphrase can be anything you want as long as it is a string of minimum length 4 and between single quotes. `passphrase = '12345'` works.<br>
    Goto line 540 and replace `cipher=cipher` with `cipher`<br>
    Goto line 541 and replace `passphrase=passphrase` with `passphrase` <br>
    Save the file. <br>
3.  Then continue with the steps as descibed in the quickstart: `sudo iotedgectl setup --connection-string "{device connection string}" --auto-cert-gen-force-no-passwords` and following.

## Deploy a module to the IoT Edge
Once the Iot Edge is deployed and running on Red Hat 7.2 you can deploy a module as described in the [linux quickstart](https://docs.microsoft.com/en-us/azure/iot-edge/quickstart-linux#deploy-a-module).
