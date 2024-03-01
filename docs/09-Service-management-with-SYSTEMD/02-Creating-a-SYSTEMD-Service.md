# Creating your own SYSTEMD Service

- Take me to the [Tutorial](https://kodekloud.com/topic/creating-a-systemd-service/)

In this lecture we will learn how to create a SYSTEMD Service.
- All the major distributions, such as Rhel, CentOS, Fedora, Ubuntu, Debian and Archlinux, adopted systemd as their init system.
- Systemd is a Linux initialization system and service manager that includes features like on-demand starting of daemons, mount and automount point maintenance etc.
- Systemd also provides a logging daemon and other tools and utilities to help with common system administration tasks.

#### What is a service unit? 

- A file with the .service suffix contains information about a process which is managed by systemd. It is composed by three main sections:

  #### 1.Unit

  - The **`Unit`** section of a .service file contains the description of the unit itself, and information about its behavior and its dependencies: (to work correctly a service can depend on another one). Here we discuss some of the most relevant options which can be used in this section
  - First of all we have the **`Description`** option. By using this option we can provide a description of the unit. The description will then appear, for example, when calling the systemctl command, which returns an overview of the status of systemd.
  - Secondly, we have **`Documentation`** option. By using this option we can get the details of the service and documentation related to it.
  - By using the **`After`** option, we can state that our unit should be started after the units we provide in the form of a space-separated list.

    ```
    [~]$ cat /etc/systemd/system/project-mercury.service
    [Unit]
    Description=Python Django for Project Mercury
    Documentation=http://wiki.caleston-dev.ca/mercury
    After=postgresql.service
    ```


  #### 2.Service

  - In the **`Service`** section of a service unit, we can specify things as the command to be executed when the service is started, or the type of the service itself.

    ```
    [Service]
    ExecStart=/usr/bin/project-mercury.sh
    User=project_mercury
    Restart=on-failure
    RestartSec=10
    ```

  #### 3.Install

  - This **`Install`** section contains information about the installation of the unit

    ```
    [Install]
    WantedBy=graphical.target
    ```

#### How to Start the Service now ?

- The system to detect the changes you have done in the file, we need to reload the daemon and start the service.

  ```
  [~]$ systemctl daemon-reload

  [~]$ systemctl start project-mercury.service
  ```
<hr />

#### Additional: 

Mar 1, 2024: 
Systemd: 

`$ systemctl status docker`
```
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2024-03-01 10:35:48 IST; 1h 39min ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 2519 (dockerd)
      Tasks: 50
     Memory: 84.4M
        CPU: 2.264s
     CGroup: /system.slice/docker.service
             └─2519 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

Mar 01 10:35:45 Laptop-LX dockerd[2519]: time="2024-03-01T10:35:45.266200660+05:30" level=info msg=>
Mar 01 10:35:45 Laptop-LX dockerd[2519]: time="2024-03-01T10:35:45.284581418+05:30" level=info msg=>
Mar 01 10:35:45 Laptop-LX dockerd[2519]: time="2024-03-01T10:35:45.976754166+05:30" level=info msg=>
Mar 01 10:35:46 Laptop-LX dockerd[2519]: time="2024-03-01T10:35:46.412658659+05:30" level=info msg=>
Mar 01 10:35:47 Laptop-LX dockerd[2519]: time="2024-03-01T10:35:47.431663519+05:30" level=info msg=>
Mar 01 10:35:47 Laptop-LX dockerd[2519]: time="2024-03-01T10:35:47.510802487+05:30" level=info msg=>
Mar 01 10:35:47 Laptop-LX dockerd[2519]: time="2024-03-01T10:35:47.784303868+05:30" level=info msg=>
Mar 01 10:35:47 Laptop-LX dockerd[2519]: time="2024-03-01T10:35:47.784906668+05:30" level=info msg=>
Mar 01 10:35:48 Laptop-LX dockerd[2519]: time="2024-03-01T10:35:48.209844055+05:30" level=info msg=>


```

`$ vim /lib/systemd/system/docker.service`

- To start the service: `sudo systemctl start <service>`
- to stop a service: `sudo systemctl stop <service>`
- after making changes, to start the service again:
  `systemctl daemon-reload`


`/etc/systemd/system/project-mercury-service`

```
[Unit]
Description= Python Django for Project Mercury
Documentation= http://wiki.

After=postgresql.service # start the mercury python app after PostgresDB
[Service]
Execstart= /usr/bin/project-mercury.sh # program /usr/bin/project/project-mercury.sh
User=project_mercury # use service account project_mercury

Restart=on-failure # Auto restart on failure

RestartSec= 10 # restart interval 10 sec


[Install]
WantedBy graphical.tartget # Load when booting into Graphical Mode

```
`Automatic log service by systemd`
