# Access Client Solutions (ACS)

<br>

**ATTENTION!**
The rest of this documentation assumes that you gained access to an IBMI machine. 


## Installation

Already documented by IBM, so here is the reference, take a look:
https://www.ibm.com/support/pages/obtaining-ibm-i-access-client-solutions


## Getting Started

Upon launching Access Client Solutions, you are greeted with this screen.


<figure align="center">
	<img src="./core/ibmi/_assets/acs-01.PNG" alt="ACS Startup Screen" />
</figure>


## Setting up a System Connection

In order to do anything here, a system connection has to be configured.
Click on **Management** > **System Configurations** > **New** . Enter the **server name** and optionally a **description**.

<figure align="center">
	<img src="./core/ibmi/_assets/acs-02.PNG" alt="ACS Connection" />
</figure>

<br>

Click on the **Connection** tab. This is personal preference, but here is **Prompt for user name and password every time** used.
<br>

<figure align="center">
	<img src="./core/ibmi/_assets/acs-03.PNG" alt="ACS Connection" />
</figure>

<br>

Click **Ok** > **Close** and now the connection can be selected here

<figure align="center">
	<img src="./core/ibmi/_assets/acs-04.PNG" alt="ACS Setup" />
</figure>

<br>



## Custom Border in Run SQL Scripts
While working in different IBM i environments, it can be hard to distinguish what envirnoment is currently opened.
This will show you how to easily tell if you are running a SQL statement in a **production** environment using a border.

Go into **Run SQL Scripts** > **View** > **Custom Border Settings**

<figure align="center">
	<img src="./core/ibmi/_assets/acs-05.png" alt="Custom border settings" />
</figure>
<br>

This configuration is an example, but set it to anything you want in here.

<figure align="center">
	<img src="./core/ibmi/_assets/acs-06.png" alt="Custom border settings" />
</figure>
<br>

Now you can easily tell what environment you're in just by seeing the scary red border.

<figure align="center">
	<img src="./core/ibmi/_assets/acs-07.png" alt="Run SQL Scripts with Border" />
</figure>
<br>



As the documentation goes on, you will touch on a bit more of ACS roughly in the following sections:

* **5250 Emulator**
* **Schemas** and **Run SQL Scripts**
* **Integrated File System**

