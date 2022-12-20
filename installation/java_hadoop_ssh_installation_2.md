#    Steps for installing Java, Hadoop AND SSH

###    Java Installation 

1. Open the Ubuntu terminal and update the package repository to ensure you download the latest software version.

    ```
    sudo apt update  
    ```
     
 2. Install openJDK
 
    ```
    sudo apt install openjdk-8-jdk -y
    ```
    
 3. Verify the version of the JDK
 
    ```
    java -version    
    ```
 
###    Create and setup SSH certificates

1. Install the SSH Service on Ubuntu.

    ```
    sudo apt install openssh-server openssh-client -y  
    ```

2. Adding a new individual user as `hdoop`

    ```
   sudo adduser hdoop 
    ```

3. Login to the new user

    ```
    su - hdoop
    ```

4. SSH key generation 

    ```
    ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
    ```
    
    > During the key generation, --------------  needed explanation ------------------

5. Authorizing the key  

    ```
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
    ```
    
6. Change the permission of the key 

    ```
    chmod 0600 ~/.ssh/authorized_keys
    ```
    
7. Connect to ssh localhost

    ```
    ssh localhost
    ```

8. Navigate to existing user.

    ```
    su - hadoopuser  
    ```
    
    > Enter password when it prompts .
    
9. Adding new user `hdoop` to sudo group.

    ```
    sudo adduser hdoop sudo
    ```
    
10.	Login to individual `hdoop` user :  

    ```
    su - hdoop
    ```

    
### Hadoop Installation

1. Downloading Hadoop

    ```
    wget https://downloads.apache.org/hadoop/common/hadoop-3.3.4/hadoop-3.3.4.tar.gz 
    ```
    
2. Extract 

    ```
    tar -xvzf hadoop-3.3.4.tar.gz 
    ```
    
### Setup configuration files

There are 6 modifications to be done on 6 different files.

1. Modification 1 : 

        a)	Open bashrc file.
                sudo nano .bashrc

        b)	After the last line , add the following .Make sure you save the file . Also make sure that the  home location is correct.																																																																																																																																																																		



        c)	To check whether code is commited or not.
                cat .bashrc
d)	Reload the modified code : source  ~/.bashrc 
             Modification 2 :
a)	Now run this command to modify the hadoop-env.sh file. 
sudo nano $HADOOP_HOME/etc/hadoop/hadoop-env.sh
b)	Add below line somewhere  and save the file.









Modification 3 :
a)	Now run this command to modify the core-site.xml file. 
sudo nano $HADOOP_HOME/etc/hadoop/core-site.xml
b)	Add the following code within configuration tags.									
																																																																																																																																																																																																																			
          Modification 4 :
a)	Now run this command to modify the hdfs-site.xml file. 
sudo nano $HADOOP_HOME/etc/hadoop/hdfs-site.xml
b)	Add the following code within configuration tags. [ <configuration>  </configuration> ]																																																																																																																																																																																			
        Modification 5 :
a)	Now run this command to modify the mapred-site.xml file. 
               	sudo nano $HADOOP_HOME/etc/hadoop/mapred-site.xml
b)	Add the following code within configuration tags. [ <configuration>  </configuration> ]	

																																																																								
        	




















Modification 6 :
a)	Now run this command to modify the yarn-site.xml file. 
             		  sudo nano $HADOOP_HOME/etc/hadoop/yarn-site.xml
b)	Add the following code within configuration tags. [ <configuration>  </configuration> ]	

																																																																																																																															



---------------------------------------------------------------------------------------------------------------------------












Step 6 : After  6  modifications , run the below commands one-by-one .
a)	Come out of your Individual hadoop user environment.
logout
b)	Start the SSH 
sudo service ssh start 
c)	To check the status of localhost :
sudo service ssh status
d)	Now navigate into individual user
su – hdoop
e)	Check if localhost works or not
ssh localhost 
f)	To Format the New Hadoop File system
hdfs namenode -format
g)	Navigating into /sbin.
cd ~/hadoop-3.3.4/sbin
h)	Starting dfs
./start-dfs.sh
i)	Starting YARN.
./start-yarn.sh
j)	Checking daemons
jps
k)	Create HADOOP HOME
hadoop fs -mkdir -p /user/bhatshreya/
l)	Checking HDFS Web UI on any browser.
http://localhost:9870
m)	Checking whether hadoop commands are running or not.
hdfs dfs -ls /
n)	Now try copying the file from local to hdfs path. [ Make sure you create any empty file inside /home/hadoopuser/ ]
hdfs dfs -put /home/hadoopuser/shreya.txt / 
o)	Check if the file is copied or not .
hdfs dfs -ls /



    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
  
 
 
