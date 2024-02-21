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

**If you don't have access to DC, how can you see Group Policy from your machine?**
- Run cmd as an admin -> 'gpresult' -> 'gpresult /h' specify a path eg 'c:\gpresults.html'
- Go to the file that was created, from there you will see the Group Policy
- Another method you can use: search in start 'rsop.msc'

**From rsop.msc can also see Group Policy for other users that are part of this computer**
- Right click the computer name -> Change Query -> This computer -> Select a specific user

**Deploy a software from Group Policy**
- Group Policy Management -> Domain -> Right click the OU -> Create a GPO in this domain, and link it here
- Other computers in the network should be able to access the file through network share:
  - This PC -> C: -> New Folder -> Right click -> Properties -> Sharing -> Advanced Sharing -> Check 'Share this folder' -> Permissions -> Add -> Type 'domain users' -> For now give full access
- From a client machine, verify you have access to that path:
  - File explorer -> \\DC\software
- In Win 10 go to google and search 'firefox download msi' -> Deploy Firefox with MSI installers -> Under MSI Installers click the link https://www.mozilla.org/firefox/all/
- Select your preferred installer: Windows 64-bit MSI -> Download -> Open folder
