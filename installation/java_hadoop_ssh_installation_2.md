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

1. Installing SSH for creating connection between Hadoop and Linux Machine.

    ```
    sudo apt install openssh-server openssh-client -y  
    ```

2. Adding a new individual user as `hdoop` and this user will use the Hadoop in the system.

    ```
   sudo adduser hdoop 
    ```

3. Login to the new user `hdoop` and enter password when it promts for it.

    ```
    su - hdoop
    ```

4. Generating the SSH key for the connection between local machine and Hadoop

    ```
    ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
    ```
    
    > During the key generation, --------------  needed explanation ------------------

5. Authorizing the key for connecting new user to the Hadoop.

    ```
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
    ```
    
6. Changing permissions of the authorized key file by using chmod.

    ```
    chmod 0600 ~/.ssh/authorized_keys
    ```
    
7. Connect to SSH localhost by creating connection to the local host so that the system works on server.

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
    
10. Login to individual `hdoop` user :  

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

	a) Run the below command to open bashrc file.
	
	       ```
               sudo nano .bashrc
	       ```

        b) Add the below lines at the end. Save[CTRL + S] the file and Quit[CTRL + X]. Also make sure HADOOP_HOME location is correctly given.
	
	       ```
	       export HADOOP_HOME=/home/hdoop/hadoop-3.3.4
	       export HADOOP_INSTALL=$HADOOP_HOME
	       export HADOOP_MAPRED_HOME=$HADOOP_HOME
	       export HADOOP_COMMON_HOME=$HADOOP_HOME
	       export HADOOP_HDFS_HOME=$HADOOP_HOME
	       export YARN_HOME=$HADOOP_HOME
	       export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
	       export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
	       export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
	       ```
	
	c) Reload the modified code.
	
	       ```
	       source  ~/.bashrc 
	       ```
	       
	c) To check whether code is commited or not.
	  
	       ```
                cat .bashrc
	       ```
     	
2. Modification 2 

	a) Run the below command to edit the hadoop-env.sh file.

		```
		sudo nano $HADOOP_HOME/etc/hadoop/hadoop-env.sh
		```
	
	b) Add the below lines for adding the Java path, save it and exit .
	
		```
		export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
		```
	
3. Modification 3 

	a)  Run the below command to edit the core-site.xml file. 

		```
		sudo nano $HADOOP_HOME/etc/hadoop/core-site.xml
		```
		
	b)  Add the following code within configuration tags, save it and exit .	
	
		```
		<property>
		<name>hadoop.tmp.dir</name>
		<value>/home/hdoop/tmpdata</value>
		<description>A base for other temporary directories.</description>
		</property>
		<property>
		<name>fs.default.name</name>
		<value>hdfs://localhost:9000</value>
		<description>bla bla</description>
		</property>

		```
																				Modification 4 :
																				
	a)  Run the below command to edit the hdfs-site.xml file. 
	
		```
		sudo nano $HADOOP_HOME/etc/hadoop/hdfs-site.xml
		```
		
	b)  Add the following code within configuration tags, save it and exit .
		
		```
		<property>
		<name>dfs.data.dir</name>
		<value>home/hdoop/dfsdata/namenode</value>
		</property>
		<property>
		<name>dfs.data.dir</name>
		<value>home/hdoop/dfsdata/datanode</value>
		</property>
		```
		
Modification 5 :

	a)  Run the below command to edit the mapred-site.xml file. 
	
		```
		sudo nano $HADOOP_HOME/etc/hadoop/mapred-site.xml
		```
		
	b)  Add the following code within configuration tags, save it and exit .
		
		```
		<property>
		<name>mapreduce.framework.name</name>
		<value>yarn</value>
		</property
		```
		
Modification 6 :

	a)  Run the below command to edit the yarn-site.xml  file. 
	
		```
		sudo nano $HADOOP_HOME/etc/hadoop/yarn-site.xml
		```
		
	b)  Add the following code within configuration tags, save it and exit .
		
		```		
		<property>
		<name>yarn.nodemanager.aux-services</name>
		<value>mapreduce_shuffel</value>
		</property>
		<property>
		<name>yarn.nodemanager.aux-services.mapreduce_shuffel.class</name>
		<value>org.apache.hadoop.mapred.ShuffleHandler</value>
		</property>
		<property>
		<name>yarn.resourcemanager.hostname</name>
		<value>127.0.0.1</value>
		</property>
		<property>
		<name>yarn.acl.enable</name>
		<value>0</value>
		</property>
		<property>
		<name>yarn.nodemanager.env-whitelist</name>
		<value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME</value>
		</property>

		```



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



    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
  
 
 
