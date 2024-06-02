![MiniELK](resources/images/MiniELK-Logo01.png)

MiniELK is a docker-compose project for running the ELK-Stack in an easy way. MiniELK is a result of my former project
'elastax' that contained various elastic stacks (recipes) - so called cookbook.
To keep it simple this project contains only the ELK Stack which should help you to get up an running with Elasticsearch/Logstash/Kibana on your local box for learning and dev purposes without any effort. Have fun! 

Please give the project a [GitHub Star](https://github.com/schneidermatic/MiniELK/stargazers)
if you like it. Thx in advance!

###### ELASTIC v8.13.x
---
What's new in Elastic 8.13? [https://www.elastic.co/blog/whats-new-elastic-8-13-0](https://www.elastic.co/blog/whats-new-elastic-8-13-0) <br/>

###### ELK REFERENCES
---
Elasticsearch: [https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html) <br/>
Logstash: [https://www.elastic.co/guide/en/logstash/current/index.html](https://www.elastic.co/guide/en/logstash/current/index.html) <br/>
Kibana: [https://www.elastic.co/guide/en/kibana/current/index.html](https://www.elastic.co/guide/en/kibana/current/index.html) <br/>

###### ELASTIC & DOCKER COMPOSE
---
[Getting started with the Elastic Stack and Docker Compose: Part 1](https://www.elastic.co/blog/getting-started-with-the-elastic-stack-and-docker-compose) <br/>
[Getting started with the Elastic Stack and Docker Compose: Part 2](https://www.elastic.co/blog/getting-started-with-the-elastic-stack-and-docker-compose-part-2) <br/>

###### PREREQUISITES
---
MiniELK is tested on Windows 11, Docker Desktop and Windows Subsystem for Linux (WSL2)

Name           | Reference    
-------------- | --------------- 
Windows        | >= 11
Docker Desktop | >= 4.12.0
WSL            | >= 2
Ubuntu         | >= 20.04.6 LTS (Focal Fossa)
docker         | [https://docs.docker.com/engine/reference/run/](https://docs.docker.com/engine/reference/run/)
docker-compose | [https://docs.docker.com/compose/reference/overview/](https://docs.docker.com/compose/reference/overview/)

INITIALIZING
---
Before you can run the ELK-Stack with WSL2 you have to change the '.wslconfig' file.

01. Create .wslconfig file under your Windows user profile directoy

        C:\Users\<YourUsername>\.wslconfig

02. Add the following lines to '.wslconfig'

        [wsl2]
        kernelCommandLine = "sysctl.vm.max_map_count=262144"

03. Shutdown Ubuntu from PowerShell

        windows~$> wsl.exe --shutdown

04. Start Ubuntu again from PowerShell

        windows~$> start ubuntu
    
**NOTE:** More information here https://learn.microsoft.com/en-us/windows/wsl/ \
          Basis Setup of Ubuntu under wsl2 https://youtu.be/X3bPWl9Z2D0
   
SETUP
---

01. In Ubuntu clone the MiniELK repo

        ubuntu~$> cd $HOME
        ubuntu~$> git clone https://github.com/schneidermatic/MiniELK.git

02. Setup your environment

        ubuntu~$> cd MiniELK/stack
        ubuntu~$> source ./.xrc
        ubuntu~$> x_setup

    **NOTE:** x_setup modifies Linux Kernel parameters.

03. Rebooting Ubuntu from PowerShell in Windows

        windows~$> wsl --list
        windows~$> wsl --shutdown "Ubuntu (Default)"
        windows~$> start ubuntu
      
03. After the rebooting of Ubuntu go into the stack folder and run ...

        ubuntu~$> cd $HOME/MiniELK/stack
        ubuntu~$> docker-compose up -d

04. Get your IP-Address with ifconfig

        ubuntu~$> ifconfig

    ![Ubuntu CLI](./resources/images/image01.png)

05. Use Kibana in your Browser for further actions

        https://localhost:5601

    ![Kibana Login](./resources/images/image02.png)

    **user: elastic**\
    **password: changeme**

06. Create your first Data 

    ![First Data](./resources/images/image03.png)

    **Select on the left side 'Discover'**

07. Create a data View

    ![Data View](./resources/images/image04.png)
    
08. Define the Index Pattern

    ![Define the Index Pattern](./resources/images/image05.png)

09. Heartbeat Log Data View

    ![Log Data View](./resources/images/image06.png)

    **NOTE:** In the Logstash file './stack/resources/ls01/pipeline/event.pipeline' there is an heartbeat input defined\
    that sends events to elasticsearch in an interval of 5 sec.

Stop and Start the ELK Stack
---

01. Stop the docker containers

        ubuntu~$> docker-compose stop

02. Start the docker containers

        ubuntu~$> docker-compose start 

Remove the entire stack
---

01. Remove the docker containers

        ubuntu~$> docker-compose down -v

    **NOTE:** when you run 'docker-compose down -v' you'll loose all your data too!!!

CONTRIBUTING
---
If you find some bugs or have any requests/suggestions don't hesitate to open an issue or make a pull request.
