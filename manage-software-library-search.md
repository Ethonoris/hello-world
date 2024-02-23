## Week 6: 

- The **sudo** command allows you to perform commands in the shell as if you were a different user, by default this is the *"superuser"* unless specified otherwise.
- The superuser is named *root* and this user is essentially an admin with special privileges.[^1]
- Such privileges include the ability to update software and perform system maintenance, which is why we've needed to use it to do updates on our virtual machines so far.
- However, it's the **apt** command that is used to actually run those updates, sudo just grants the permission to do so.
- the apt command can also search for and install software applications on the virtual machine as well.

For the purpose of keeping a list of the examples in one place, here are several of these commands which we will be commonly be making use of in our virtual machines: 

![Sudo and Apt Commands](https://github.com/Ethonoris/hello-world/assets/44278023/8a64665a-cf2e-4ddb-9682-d273cbd82938)

- The program, **Yaz**, is used to assist with information retrieval via the **Z39.50 protocol** for sharing and accessing bibliographic information between library databases. 
- Once installed, the Yaz client can be opened and in it the command to connect to a library's discovery service can be entered.
- In this case we used `open saalck-uky.alma.exlibrisgroup.com:1921/01SAA_UKY`
- I first used the command: `f @attr 1=21 "anthropology"`
- After using the `show 1` command, it returned the first record!

![Yaz3](https://github.com/Ethonoris/hello-world/assets/44278023/e93b82ad-8494-450f-94e2-8b1718d5ebde)

- Additionally, I installed the **bat** application for future use. See the following for the process:

![bat1](https://github.com/Ethonoris/hello-world/assets/44278023/5000dfaa-4c6c-4fe9-837b-7232f9435543)

![bat2](https://github.com/Ethonoris/hello-world/assets/44278023/8145e622-6b2c-4f2b-8bf6-59542dffa1dd)


[^1]: Although sudo does allow you to execute commands as if you were an administrator, it is actually the **group** command that would be used to user privilege groups. These are different groups with different levels of access that users are placed in. 
