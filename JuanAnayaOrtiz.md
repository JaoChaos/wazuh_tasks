# Tasks for the selection process.
# Juan Anaya Ortiz.

## Index:
  1. **Common Tasks**
    1. Deploy manager and agent
    2. Verify agent works properly
    3. Verify manager generates alerts
    4. Comment the problems found during the work
  2. **Specific tasks**
    1. Fork documentation repository
    2. Generate docs and comment about dependencies
    3. Create a branch in my fork and add something new on it
    4. Create a second branch fixing or adding something
    5. Create 2 pull requests with the last 2 branches
    6. Accept the P.R. and see if everything has worked
  3. **Conclusions**

## 1. Common tasks:

##### Lets the company review if I'm able to use their technologies properly.
I'm asked to install the software that the company uses on its everyday.
Then, I'm asked to show how it works and if it works as it should.

### 1.1 Installing and deploying the software:

First of all, we must add the Wazuh repository to our PC.

For this, we should follow the instructions they give us, and as I use Ubuntu, I did:

To install the packages necesaries to use the software.
```
$ apt-get update
$ apt-get install curl apt-transport-https lsb-release
```

This to create a new python file.
```
$ if [ ! -f /usr/bin/python ]; then ln -s /usr/bin/python3 /usr/bin/python; fi
```

This to add the GPG key.
```
$ curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | apt-key add -
```

And finally, this to add the repository and actuallize everything.
```
$ echo "deb https://packages.wazuh.com/3.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list
$ apt-get update
```
![imagen1](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/1.png)
![imagen2](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/2.png)

After adding the repository, we install the manager:

It's super-easy, just use:
```
$ apt-get install wazuh-manager
```

And then, use this order to check the service status:
```
$ systemctl status wazuh-manager
```

![imagen3](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/3.png)
![imagen4](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/4.png)


Now,, to install the agent, as we have configured the repository installation, we only need to do:

```
$ apt-get install wazuh-agent
```

After this, we need to create a new agent in the manager, extraxt its key, and paste it in the agent machine.

![imagen11](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/11.jpeg)

Then, we go to the ``` ossec.conf ``` filoe and add the manager IP into the client.

To check if both are connected, we run ``` $ netstat -vatunp|grep ossec-agentd ```

![imagen12](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/12.jpeg)

Now, to see if they are really connected and to check if alerts are being sent, we check de alerts.log in the manager.

![imagen13](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/13.png)

In this file, we can check many things, like the agent has connected well, the ports have opened to listen the agent, etc.

All this says that we have done all well.


### 1.2 Verify the agent works properly.

To verify it, I'm going to send an event to the manager.
I could have created a Virtual MAchine to try this, but as I own 2 computers, I've installed the agent in the second one and I'm using one as the manager and the other as the agent.

Now, first thing is to register the agent:

Once installed the agent, in the manager we create the agent we will use:

```
$  /var/ossec/bin/manage_agents
```

Using this order, we create an agent with a name, an ID and an IP.



## 2. Specific tasks:

Here, I must show that I know how to work with GitHub.

### 2.1 Fork project:

I forked the project just using the web client of GitHub.
This is the result:
[GitHub](https://github.com/JaoChaos/wazuh-documentation)

### 2.2 Generate the documentation using "Make":

After I cloned the repository in my PC, I used the order ``` $ make ```, but I needed to install the requirements, so I did it:

```
$ sudo pip install -r requirements.txt
```

After that, I was able to use the order ``` $ make (arg)``` as I wanted, so to give it a try, i used ``` # make html```to make a documentation in that format, and also i used ``` $ make json``` to see if it worked as it should.

![imagen](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/5.png)
![imagen](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/6.png)

### 2.3 Create a branch in my fork and add something new on it:

To create a new branch in my forked repository, first of all I make a pull to update the files.
Now, I create the branch using ``` $ git checkout -b branch_1 ```

In the branch, I have changed the Makefile and added a new line, and I created a new folder to host static images that can be placed into the documentation.

### 2.4  Create a second branch fixing something.
For this purpose, i've changed a few more lines of the Makefile to leave a clearly reading of it.


### 2.5 Pull request the 2 branches into my forked repository:

For doing this, we just use the line command:

``` $ git push origin branch_1 ```

``` $ git push origin branch_2 ```

![imagen](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/7.png)

### 2.6 Accept the P.R. and see if everything has worked.

After pushing my local folder to the master branch, I check if everything has worked.
We can't see the img folder as it is empty, but it is there.

![img](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/8.png)
![img](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/9.png)
![img](https://github.com/JaoChaos/wazuh_tasks/blob/master/img/10.png)

## 3. Conclusions.

I have enjoyed really much doing this tasks, and I appreciate a lot to Wazuh for giving me the oportunity to know more about them.

Hope you like the work.

Juan Anaya Ortiz.
