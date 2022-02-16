# test-project


Installation steps for Nexus Repository:

1. sudo apt-get update

2. sudo apt install openjdk-8-jre-headless

3. sudo wget http://download.sonatype.com/nexus/3/nexus-3.22.0-02-unix.tar.gz --> download nexus repo

4. tar -zxvf nexus-3.22.0-02-unix.tar.gz

5. sudo adduser nexus --> add the nexus username

6. sudo chown -R nexus:nexus /root/nexus-3.22.0-02

7. sudo chown -R nexus:nexus /root/sonatype-work

8. sudo vi /root/nexus-3.22.0-02/bin/nexus.rc
   run_as_user="nexus"
   
9. sudo vi /root/nexus-3.22.0-02/bin/nexus.vmoptions
-Xms512m
-Xmx512m
-XX:MaxDirectMemorySize=512m

10. Run nexus as a service using systemd

sudo vi /etc/systemd/system/nexus.service

[Unit]
Description=nexus service
After=network.target
[Service]
Type=forking
LimitNOFILE=65536
ExecStart=/root/nexus-3.22.0-02/bin/nexus start
ExecStop=/root/nexus-3.22.0-02/bin/nexus stop
User=nexus
Restart=on-abort
[Install]
WantedBy=multi-user.target

11. start the nexus using

   cd /root/nexus-3.22.0-02/bin
   ./nexus start
   
12. Allow port 8081 using
   
    ufw allow 8081/tcp
	
13. login to the browser:

    http://localhost:8081
	
default username: admin
Default passwaord: cat /opt/nexus/sonatype-work/nexus3/admin.password --> u can get from here
