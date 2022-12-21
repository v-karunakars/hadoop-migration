# Steps for installing Ubuntu on Windows Subsytem for Linux [WSL]

1. Open Windows Power shell as administrator and run the below command to install WSL.

    ```
    wsl --install
    ```
2. To check available online distributions, run the below command.

    ```
    wsl --list --online 
    ```
    
    > Here you would see many distributions with different version. Make sure you install **Ubuntu 20.04** using `wsl --install -d <Distribution Name> ` command.

3. To install Ubuntu 20.04, run the below command.

    ```
    wsl --install -d Ubuntu 20.04
    ```

4. Make sure you restart your VM for the changes to be effective. Once you restart your VM, a terminal pops-out which completes Ubuntu installation.

5. Set the username and password for Ubuntu

    a) username
    
    ``` 
    hadoopuser 
    ```
    b) password
    
    ``` 
    hadoop123  
    ```



