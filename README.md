<h1>Group-Policy</h1>

- Group Policy allows administrators to manage and apply various settings and configurations across multiple computers in an organisation. Behaviour of users and computers in a network can be controlled, for example password policies can be enforced, certain features can be restricted, and software updates and applications can be deployed.

**Install RSAT: Group Policy Management Tools on a Windows 10 machine**
- Login with an admin account -> Right click Start -> Apps and Features -> Optional features -> Add a feature -> Group Policy Management Tools

<img src="https://i.imgur.com/Bd1ZQMO.png" height="50%" width="50%" alt="Install Group policy managment tool"/>

**See the Group Policy on a workgroup computer**
- Search 'edit group policy'

<img src="https://i.imgur.com/e5KWPUF.png" height="50%" width="50%" alt="local group policy editor screen"/>

**How to check the minimum password length on a Windows 10 computer**
- Search 'edit group policy' -> Windows Settings -> Security Settings -> Account Policies -> Password Policy

<img src="https://i.imgur.com/LROYbs3.png" height="50%" width="50%" alt="Check minimum password length"/>

**From DC (Domain controller) how to check default domain policy**
- Group Policy Management -> Default Domain Policy -> Settings
- This will generate a report of the default domain policy

<img src="https://i.imgur.com/tQVq3p4.png" height="60%" width="60%" alt="Default group policy report"/>

**How to change a Group Policy. For example, changing the minimum password length**
- Group Policy Management -> Forest -> Domains -> Right click Default Domain Policy -> Edit -> Policies -> Windows Settings -> Security Settings -> Account Policies -> Password Policy -> Minimum password length

<img src="https://i.imgur.com/1dvrqhA.png" height="60%" width="60%" alt="Password policy editor screen"/>

**Once a policy has been applied how can it be implemented to a client machine**
- Restart the machine
- Or cmd -> 'gpupdate /force'
- The changes made in the domain will now be applied to this machine
- **Note:** Some policy may require a restart

**If you don't have access to DC, how can you see Group Policy from your machine?**
- Run cmd as an admin -> 'gpresult' -> 'gpresult /h' specify a path eg 'c:\gpresults.html'
- Go to the file that was created, from there you will see the Group Policy. Screenshot below displays this

<img src="https://i.imgur.com/Wc6DrZ0.png" height="60%" width="60%" alt="Screen showing password and account policy"/>

- Another method you can use: search in start 'rsop.msc'

<img src="https://i.imgur.com/MyVh1TR.png" height="60%" width="60%" alt="Resultant set of policy screen showing password policy"/>

**From rsop.msc can also see Group Policy for other users that are part of this computer**
- Right click the computer name -> Change Query -> This computer -> Select a user

**Deploy a software from Group Policy**
- Group Policy Management -> Domain -> Right click the OU -> Create a GPO in this domain, and link it here
- Other computers in the network should be able to access the file through network share:
  - This PC -> C: -> New Folder -> Right click -> Properties -> Sharing -> Advanced Sharing -> Check 'Share this folder' -> Permissions -> Add -> Type 'domain users' -> For now give full access
- From a client machine, verify you have access to that path:
  - File explorer -> \\DC\software
- In Win 10 go to google and search 'firefox download msi' -> Deploy Firefox with MSI installers -> Under MSI Installers click the link https://www.mozilla.org/firefox/all/
- Select your preferred installer: Windows 64-bit MSI -> Download -> Open folder

need m.sci file

can create a OU in AD and deploy group policy on top of that OU 

start -> Windows Administrative Tools -> Group Policy Management -> Forest -> Domains -> Domain 

ADUC -> Domain name -> Right click OU name and create an OU, this eg call it Staff -> 

From Staff is where we want to deploy GP, anything inside Staff will get the GP

Put the computer inside the Staff OU so that the GP can be applied to the computer

Here we are going to setup a GP to install a software from the GP
Open GP management -> forest -> Domains -> Domain name -> Right click Staff OU -> Create a GPO in this domain, and Link it here -> In this eg name it firefox

Need to create a shared folder so other computers can have access to this folder through the network:
File explorere -> This PC -> C: -> Create new folder name it software -> Right click folder -> Properties -> Sharing -> Advanced Sharing -> Check 'share this folder' -> Permissions -> Add -> Type domain users -> For now check full control, change, read -> and give Everyone full access 

Verify that you can get to this path:


