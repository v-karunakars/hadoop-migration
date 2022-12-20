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


    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
  
 
 
