# InGateway902 Docker user manual
InGateway902 series edge computing gateway (IG902 for short) supports manage docker images. You can publish your docker images to IG902 to quickly deploy and run applications developed by yourself. In order to introduce how to use IG902's Docker environment, this document will demonstrate how to run an Nginx image on IG902. This image is used for open source reverse proxy server for HTTP, HTTPS, SMTP, POP3 and IMAP protocols, and load balancer, HTTP cache And web server.  <br/>
Docker is an open source application container engine that allows developers to package their applications and dependencies into a portable container and then publish it to any popular Linux machine or Windows machine. It can also be virtualized. The container is completely with the sandbox mechanism, there will be no interface between each other.

## Prepare IG902 Hardware and Network Environment
### Connect IG902 to the Power Source and to a PC with a Network Cable
Connect IG902 to the power source and to a PC with an Ethernet cable according to the topology diagram.   <br/>
![](images/2020-01-21-10-08-56.png)

### Set LAN Parameters: Access the IG902 Through LAN
- Step 1: Set the PC’s IP address to be on the same subnet with GE 0/2. By default, the IP address of GE 0/2 on IG902 is 192.168.2.1. 
  - Method 1: Enable the PC to obtain an IP address automatically (recommended)  

     ![](images/2020-01-02-09-55-52.png) <br/>
 &nbsp;


  - Method 2: Set a fixed IP address  <br/>
     Select Use the following IP address, enter an IP address (By default,any from 192.168.2.2 to 192.168.2.254), subnet mask (By default,255.255.255.0), default gateway (By default,192.168.2.1), and DNS server address, and click OK.   

    ![](images/2020-01-21-15-57-32.png)  
<br/>

- Step 2: Launch the browser on the PC and access the IP address of GE 0/2. Enter the login user name and password. The default user name and password are adm and 123456 respectively.
![](images/2020-01-21-14-19-06.png)   
 &nbsp;

- After successful login, you can see the web page as shown below: 
![](images/2020-02-14-11-13-27.png)  
 &nbsp;

- Step 4: To change the user name and password for logging in to the web management interface of IG902, choose System > User Management page of IG902 and set the new user name and password. 
![](images/2020-01-21-10-37-54.png)
&nbsp;

- Step 5: To change the IP address of GE 0/2, choose Network > Network Interfaces > Ethernet > Gigabitethernet 0/2 page of IG902 to configure GE 0/2.
![](images/2020-01-21-10-42-52.png)  

### Set WAN Parameters: Connect IG902 to the Internet
  - Method 1: Connect to the Internet by SIM card
    - Step 1: Insert the SIM card. (Note: Before inserting or removing the SIM card, unplug the power cable; otherwise, the operation may cause data loss or damage the IG902.) After inserting the SIM card, connect the 4G LTE antenna to the ANT interface and power on the IG902.  <br/>

      ![](images/2020-01-21-11-14-06.png)  <br/>
 &nbsp;


    - Step 2: Choose Network > Network Interfaces > Cellular page of IG902 and select Enable Cellular and click Submit.
![](images/2020-01-21-11-05-24.png)
&nbsp;

      When the network connection status is Connected and an IP address has been allocated, the IG902 has been connected to the Internet with the SIM card. 
      ![](images/2020-01-21-16-41-33.png)
&nbsp;

  - Method 2: Connect to the Internet by Ethernet
    - Step 1: Use the Ethernet cable to connect the GE 0/1 and GE 0/2 ports of the IG902 respectively, as shown below: 
 
      ![](images/2020-01-21-11-23-29.png)  </br>
&nbsp;

    - Step 2: Choose Network > Network Interface > Ethernet > Gigabit Ethernet 0/1 page of IG902 to configure the IP address of the GE 0/1 port and click Submit. (When the network type is a static IP address, you need to configure the IP, subnet mask, and other information according to the site network conditions.)
![](images/2020-01-21-11-35-11.png)

      ![](images/2020-01-21-11-35-37.png)  </br>
&nbsp;

    - Step 3: Choose Network > Static Routing > Configuration page of IG902 to add a static route for GE 0/1 port and click Submit. (Select "Gigabitethernet 0/1" for the interface item, and configure the other items according to the site network conditions.)
![](images/2020-01-21-11-33-52.png)  </br>
   &nbsp;
    - Step 4: Choose System > Network Tools page of IG902 and use the Ping tool to check whether the IG902 has successfully connected to the Internet. The following figure shows that IG902 have successfully connected to the Internet:
  ![](images/2020-01-21-11-39-12.png)

### Update the firmware
To obtain the latest firmware version of IG902 and updated functions, contact the customer service center. To update the IG902 firmware, do as follows:<font color=#FF0000> (The firmware version should be 2.0.0.r12057 and above)</font>   </br>
Choose System > Firmware Upgrade page of IG902 and select the corresponding firmware file and click Start Upgrade. Select a firmware file and click Start Upgrading. After the update is completed, you are prompted to restart the system to Apply the new firmware.  <font color=#FF0000> It is recommended to ensure that the IG902 has the https service enabled before the upgrade, otherwise the IG902 cannot be accessed through the web page after the upgrade. </font>
![](images/2020-01-21-14-20-39.png)
 &nbsp;

## Enable and configure Docker manager
### Install Docker SDK and enable Docker manager
The Docker SDK integrates the operating environment and docker image manager required to run the docker image. Before using Docker, you must install the Docker SDK. To obtain the Docker SDK, please contact the customer service center.  </br>
- Step 1: If you already have the Docker SDK, choose Edge Computing > Docker Manager page of IG902, close the Docker Manager and import the Docker SDK.
![](images/2020-02-12-17-27-06.png)  </br>
   &nbsp;

- Step 2: After importing, IG902 will automatically install the Docker SDK. The installation process usually takes 1-2 minutes. Please be patient. After successful installation, select Enable Docker Manager and click Submit.
![](images/2020-02-11-15-19-42.png)  </br>
   &nbsp;
   
- Step 3: Then you can modify the port number and login password to access the Docker manager.
![](images/2020-02-11-15-23-39.png)

### Configure Docker Manager--Portainer
IG902 uses Portainer to build, manage and maintain Docker images and containers. For a detailed introduction and instructions on Portainer, please see the [Portainer official website](https://www.portainer.io/overview/). This document will show you how to add and deploy an Nginx docker image on IG902.

#### Access Portainer
- Step 1: Click Portainer's access button, and Portainer will prompt you to enter your username and password. At this time, copy the user name and the set password from the Edge Computing > Docker Manager page of IG902 and click Login.
![](images/2020-02-11-15-27-41.png)
![](images/2020-01-21-14-36-08.png)  </br>
   &nbsp;
   
- Step 2: After the login is successful, as shown in the figure below, select Local to use the Portainer to manage the docker image on the IG902, and then click Connect.
![](images/2020-01-14-16-20-37.png)  </br>
   &nbsp;
   
- Step 3: On the Home page of Portainer, select local to manage the docker image on IG902.
![](images/2020-01-14-16-21-43.png)  </br>
   &nbsp;
   
  Then you will jump to the local dashboard, where you can get an overview of the IG902's containers and images.
![](images/2020-01-14-16-22-43.png)

#### Add docker image
There are two ways to add docker images for Portainer.
- Method 1: Import the local docker image from the Edge Computing > Docker Manager page of IG902. (The time required for import varies depending on the size of the docker image; please be patient when the docker image is large.)
![](images/2020-02-11-15-29-07.png)  </br>
   &nbsp;
   
  You can see the docker image successfully imported on the Local > Images page of Portainer.
![](images/2020-01-14-17-24-07.png)  </br>
   &nbsp;
   
- Method 2: Choose Local > Images page of Portainer and download the nginx docker image from DockerHub. (The time required to download the image varies depending on the size of the image; please be patient when the docker image is large)
![](images/2020-01-21-15-24-52.png)  </br>
   &nbsp;
   
  After the docker image is downloaded, you can see the corresponding docker image information in Local > Images as shown below: 
![](images/2020-01-21-15-28-04.png)

#### Configure and deploy container
- Step 1: Choose Local > Containers page of Portainer and click Add container to add a new container.
![](images/2020-01-13-18-08-05.png)  </br>
   &nbsp;
   
- Step 2: Configure the operating parameters for the container and deploy the container.
![](images/2020-01-21-15-33-01.png)  </br>
   &nbsp;
   
- Step 3: The container will run automatically after deployment. You can view the container running status on Portainer's Local > Containers page.
![](images/2020-01-13-18-16-28.png)  </br>
   &nbsp;
   
- Step 4: After entering the Nginx access link (IP address + port number of IG902) configured in the container in the browser, you can see the Nginx welcome page.This shows that the Nginx docker image has been running on the IG902 normally. Now, you have completed adding and deploying an Nginx docker image on the IG902.
![](images/2020-01-14-17-42-52.png)

## Appendix
### How to download docker images from gitlab / github 
Choose Local > Registries page of Portainer and click Add registry to add a docker mirror repository (must be a public repository).
![](images/2020-01-19-10-39-19.png)  </br>

Then select Custom registry and configure the mirror repository information. After configuration, click Add registry.
![](images/2020-01-21-15-40-36.png)  </br>

After the mirror repository is successfully added, you can see the web page as shown below:
![](images/2020-01-21-15-41-25.png)  </br>

After the addition is successful, you can select the configured image repository when pulling the docker image.
![](images/2020-01-21-15-41-59.png)
