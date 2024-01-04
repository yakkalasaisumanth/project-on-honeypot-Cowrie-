# Setting Up A Honeypot.

1. what is Honey pot?

- Honey pot is a type of machine deployed by the defenders to know the attackers moves.

- in other way a machine deployed to trap attacker from accessing into the real network and monitoring their attack modules to build a better and secure environment.

2. Do we really need honey pots?

- It depends upon the organization. but it is the best practice to be implemented to study the motive of attackers.

3. basic honey pot looks some what like this:-

- ![Honey Pot](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/honeypot.png)

- the DMZ is where all you servers are located like ftp,dns,etc,.

- it is the best practice to deploy the honey pot in DMZ for better monitoring and security purposes.

- some may follow different procedures of deploying the honey pots. it's again up to you.

## More Information Of Honey Pot Setup

- the setup i used is pre built honey bot setup named 'cowrie'

- you can create a simple honey pot by yourself like fake access point honey pot, deploying a Linux Apache server and making some changes to look like honey pot,etc,.

- in this project we are going to setup **COWRIE** honey pot.

- ![cowrie honeypot](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/cowrie%20honeypot.png)

- there are so many pre determined honey pots to play with you can choose your favorite one.

all in one honey pot image

## Brief Introduction Of Cowrie.

- ![cowrie official](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/cowrie%20official%20page.png)

- cowrie is ssh/telnet based honey pot.

- cowrie can be deployed with the default settings or custom settings.

- like we can change the default ports.

- cowrie uses 2222 and 53 ports which are default ports of the ssh and telnet services.

- but as we think like attacker he can easily identify that this is a honey pot.

- so make sure to change the ports something like 4464 and 6655,etc,.

- you can also make this honey pot spicier by adding custom files to it. to make it look like more genuine machine.

- here in this project i am just going with defaults just to understand how cowrie is working.

- Honey pots list:- [HONEYPOTS](https://github.com/telekom-security/tpotce)

- ![honeypots list](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/all%20in%20one%20honeypot.png)

- ![TPOT LIST](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/cowrie%20honeypot.png)

## Installation Of Cowrie.

- cowrie link :- [COWRIE](https://github.com/cowrie/cowrie)

- please open the link and follow the steps.

- we are going to use the docker installation method you can also use the python 3.11-venv also.

- i have installed the honey pot in the both the ways if you want to install in any way its up to you.

   ### Installing Using Docker.

   - run the following command on any Linux server machine.
   ```
   docker run -p 2222:2222 cowrie/cowrie:latest
   ```

   - ![COWRIE DOCKER](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/cowrie%20installation..png)

   - Before Running the command please make sure that you check the following.
   - [x] python 3
   - [x] docker
   - [x] git

   - if do not have docker installed. please type the following command.
   ```
   sudo apt install docker.io
   ```

   - it will install docker for you.

   - to start the cowrie enter the following code.
   ```
   docker run -p 2222:2222 cowrie/cowrie:latest
   ```

   - ![COWRIE SETUP](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/cowrie%20insstallation%20and%20setup.png)

   - all set you are good to go.

   ### Installing using the python venv.

   - before we start make sure you have these installed.
     [x] python 3
     [x]python 3.11-venv
     [x]git

   - if do no have these tools paste the following command
   ```
   sudo apt install python3 python3.11-vene -y
   ```

   - after that you should install some dependencies.
   ```
   sudo apt-get install git python3-virtualenv libssl-dev libffi-dev build-essential libpython3-dev python3-minimal authbind virtualenv
   ```

   - add a new user.
   ```
   sudo adduser cowrie
   ```

   - now change user.
   ```
   sudo su cowrie
   ```

   - now type the following commands.
   ```
   cd ..
   cd cowrie
   ```

   - now clone the repository.
   ```
   git clone http://github.com/cowrie/cowrie
   ```

   - now cd into cowrie directory.
   ```
   cd Cowrie
   ```

   - now type the following commands
   ```
    python -m venv cowrie-env
    source cowrie-env/bin/activate
    python -m pip install --upgrade pip
    python -m pip install --upgrade -r requirements.txt
   ```

   - if you want to run telnet service.

   - you should create a file called cowrie.cfg

   - make sure to follow the process.
   ```
   cd etc
   touch cowrie.cfg
   nano cowrie.cfg
   ```

   - now paste the following or write the following.
   ```
   [telnet]
   enabled = true
   ```

   - now press ctrl+x and then y 

   - now come back to the cowrie directory.
   ```
   cd ..
   ```

   - now starting the cowrie
   ```
   bin/cowrie start
   ```

   - now cowrie is up and running.

### Conflicts or Error Messages.

- please refer to the documentation provided by the cowrie.

- documentation link:- [DOCUMENTATION](https://cowrie.readthedocs.io/en/latest/index.html)

### Now All The Things Set up And Running. Lets Start The Attack Process.

   ### Assumptions To Be Kept In Mind.

   1. we are acting as a malicious hacker.

   - which means a hacker already have access to the organization network.

   2. A hacker had successfully entered the network.

   ### Starting the Attack Session.

   1. open a new Linux machine make sure that the cowrie and the Linux machine are on the same network.

   2. first if you are a hacker how is inside the network what you will do?.

   - I like to scan the entire network using Nmap you can use zenmap if you are using the widows machine.

   - ![NMAP IMAGE](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/nmap%20scan.png)

   3. we can see that port 2222 is open and if we recall network basics the port 2222 is used for ssh.

   4. in case you have set up the telnet you will find 53 port opened.

   5. in my case i didn't setup now i am going to connect to the system using the ssh.

   6. first please make sure that this is not a real scenario, because if have identified a port open we go to further analysis of the port like what other ports are open and we do further more analysis etc,. 

   7. but if we don't know any further details we try username as root and IP as our local host.

   8. in this case lets do that.
   ```
   ssh -p 2222 root@10.0.2.15
   ```

   - ![SSH ROOT](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/sucessfuly%20connected.png)

   9. now it prompts for a password as attacker we will try a default passwords used for root/.

   10. lets use password as **"root"**

   11. now we are successfully logged in to the server.

   12. now lets run simple commands.

   - ![ATTACK SIMULATION](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/attacker%20attacks.png)

   - ![ATTACK SIMULATION1](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/attacker%20attacks%201.png)

   - ![ATTACK SIMULATION2](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/attacker%20attacks%202.png)

### Now From The Server Side.

1. we can see that some one is connected to the network.

2. and we can see each and everything the attacker is doing.


#### Please Note The Following.

1. as this is not a real server we can be safe from hackers and we can also learn their foot prints.

- ![ATTACKER TRACKS](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/attacker%20tracks.png)

- ![ATTACKER TRACKS1](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/attacker%20tracks1.png)

- ![ATTACKER TRACKS2](https://github.com/yakkalasaisumanth/settingup-Cowrie-honeypot/blob/main/images/attacker%20tracks%202.png)

2. of course some might guess that why hacker didn't suspect the logging attempt made.

   - it is because there are many ssh machines which run on default passwords and with no passwords.

   - and after login the attacker is presented with the Linux machine files which diverts the thoughts of the attacker.

   - of course some hackers can easily predict what is a honey pot and a real one.

3. these honey pots will terminate a low profile hackers who are new to the industry and also if we combine 4-5 honey pots the attacker might think it is real.


4. like combining the cowrie, ddospot, elasticpot, and mailhoney etc,.

##### It IS Best Practice To Know About Honey Pots And Being Aware Of Them Try to play With As Many Honey Pots As Possible.

##### Make Sure That DePLoying Honey Pots On To Your Network May Damage Your Network And The Devices INtegrated With IT.

##### The Above Project Is Done In A Secure Environment. So Please Be Careful And I Am Not Responsible For Your Losses.

##### Thank You For Your Valuable Time.











  