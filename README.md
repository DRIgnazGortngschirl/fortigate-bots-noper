# fortigate-bots-noper
Basically the [Fortigate Bots Refuser](https://github.com/MrMarioMichel/fortigate-bots-refuser) 2.0

# What is FortiGate Bots Noper ?
FortiGate Bots Noper is a very good approach to proptect internal server no matter if those hosts are in the DMZ or behind NAT from external to internal. Since we can restrict access to certan hosts that can be defined in the policiy section of an FortiGate.

# Inspiration for FortiGate Bots Noper
We live in a world full of digitalized information/data. We have the responsibility to protect either our/any data on any host we own.

# Motivation for FortiGate Bots Noper
Due to my passion in security I try to keep my firewall policies as tight as possible but what if you can't have such policy tighten down to host 2 host on port x. The Best example would be an web server, as everyone should have access to reach it. Under, form us legal ways of protection and certain circumstances.

# What does FortiGate Bots Noper do ?
FortiGate Bots Noper isn't a product of me it was crated by Fortinet and is known under Security Fabric. I do use this product to create my own service without breaking any Terms of usage by Fortinet.

# Requirements for FortiGate Bots Noper
An FortiGate able to run 6.2.X or higher.



# How to Implement
Now we are talking...

1. Do understand that you are using a service created by someone on the internet. I will/can't grantee anything. 
2. Understand the limitations form Fortinet. 
3. Implement the following at your own risk.

### Lets get started
GUI setup 

#### 1. Step
Login to your FortiGate and navigate to "Security Fabric" -> "Fabric Connector" -> * Click * on "Create"
![](https://github.com/MrMarioMichel/fortigate-bots-noper/blob/main/img/step_1-gui.png)

#### 2. Step
*Click* on "IP Address"
![](https://github.com/MrMarioMichel/fortigate-bots-noper/blob/main/img/step_2-gui.png)

#### 3. Step
Configure the following:

* Name = Can defined by you as you wish.
* URI of external resource = https://mariomichel.com/bots/contact_list-22.txt
* HTTP basic authentication = * Turn off *
* Refresh Rate = Can defined by you as you wish. (Recomened 1/2 of the update rate of the feed)
* Comments = Can defined by you as you wish.
* Status = * Turn on *

*Click* on "OK"

![](https://github.com/MrMarioMichel/fortigate-bots-noper/blob/main/img/step_3-gui.png)

#### 4. Step
*Right click* -> Edit

![](https://github.com/MrMarioMichel/fortigate-bots-noper/blob/main/img/step_4-gui.png)

#### 5. Step 
If all went fine you should also see this. Check Entries with "View Entries"

![](https://github.com/MrMarioMichel/fortigate-bots-noper/blob/main/img/step_5-gui.png)


#### 6. Step 

You can now use the IP list to restrict access to hosts by an denying policy defined in the "Source"

![](https://github.com/MrMarioMichel/fortigate-bots-noper/blob/main/img/step_6-gui.png)

CLI setup [ For pros ;) ]

Note* This is my config you need to replace certain things but you know that ...

```
config system external-resource
    edit "FortiGate Bot Noper"
        set type address
        set comments "https://github.com/MrMarioMichel/fortigate-bots-noper"
        set resource "https://mariomichel.com/bots/contact_list-22.txt"
        set refresh-rate 720
    next
end
```

```
config firewall policy
    edit 0
        set srcintf "wan"
        set dstintf "v10_Server"
        set srcaddr "FortiGate Bot Noper"
        set dstaddr "michels-server"
        set schedule "always"
        set comments "https://github.com/MrMarioMichel/fortigate-bots-noper"
        set service "ALL"
        set logtraffic all
    next
end
```
