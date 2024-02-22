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

**Deploy a software from Group Policy. In this example I will be deploying Firefox**
- **Note:** Software can be deployed through an Organisational Unit (OU) in Active Directory.
- In DC -> ADUC -> Create an OU -> I have created an OU called 'Staff'
- Move the computer that you would like the Group Policy to be applied to into the Staff OU
- Go Group Policy Management -> Right click the Staff OU -> Create a GPO in this domain, and Link it here -> Give the GPO a name, I will name it Firefox
- Now the other computers in the OU need to be able to access this Firefox file through network share.
  - File Explorer -> This PC -> (C:) -> Create a folder, in this example the folder is called Software -> Right click the folder -> Properties -> Sharing -> Advanced Sharing -> Check 'Share this folder' -> Permissions -> Add -> type 'domain users' -> Check Names -> OK -> For now give domain users and everyone full access
- Make a note of the network path
- Login to a client computer using a domain user account
- In File explorer enter the network path into the search bar
- In Google search firefox download msi -> Click the 'Deploy Firefox with MSI installers - Mozilla Support' link -> Scroll down and click the link under MSI Installers
- Set the preferred installer to 'Windows 64-bit MSI' -> Download Now
- Once the download is complete copy the file and paste it into the network share
- Go back to DC -> Group Policy Management -> Right click the Firefox file -> Edit -> Policies -> Software Settings -> Right click Software installations -> New -> Package -> Enter the network path into the search bar -> Software file -> Firefox setup file -> Check 'Assigned' ->
- If you don't see the group policy right click and refresh
- In Group Policy Management remove Authenticated Users
- Add -> Object Types -> Check Computers
- Enter the client computer name
- From the client computer



need m.si file

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
- Win 10 -> File explorer -> in search bar type the path to this file eg \\plabdc01\\software

Download firefox from win 10
- google --> firefox download msi
- click 'Deploy firefox with msi installers - mozilla support'
- Under MSI installers click the link: https://www.mozilla.org/firefox/all
- select your preferred installer: Windows 64-bit MSI -> Download Now

Once download is complete copy the firefox folder and paste it into the shared folder

Go back to DC -> Group policy management --> right click firefox folder -> edit -> policies -> software settings -> right click software installation -> new -> package 
- Type the network path in the search bar eg \\plabdc01 -> Software -> Firefox setup -> check assigned ->

if don't see the GP right click refresh

Need to go back and apply this policy 
- Group policy management -> Staff -> firefox -> remove authenticated users -> add -> object types -> check everything -> type in the computer name eg plabwin101

In win 10 comp apply for policy
- cmd -> 'gpupdate /force'
- should get a message that says for this policy to be applied to PC needs to be restarted
- restart this machine, then log back in to see if Firefox has been installed 

