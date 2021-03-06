
# Set Up Access to a Remote Server on Mac

**Installing VS Code**

Go to [Visual Studio Code](https://code.visualstudio.com/) and follow the steps to download and install VS Code on mac. After opening the application, it should look like this: 

![Image](1.png)

**Remotely Connecting**

- Find your [account information](https://sdacs.ucsd.edu/~icc/index.php). Enter your current UCSD username and student ID in the "Account Lookup" section. After submission, look for the account that starts with `cs15lwi22`. This is your CSE 15l specific account. 

- Open a terminal window in VS Code(Terminal button on the top of the screen -> New Terminal) and type the command(notice ... are the letters in your account): 

`$ ssh cs15wi22…@ieng6.ucsd.edu` 

- A message will be displayed. Type `yes` and press enter. 

- A prompt for your password will show up. Type in your password carefully because the text that you are typing does not actually appear even though it is being inputted to the terminal. After typing in your password, something similar to this screenshot should be displayed. 

![Image](2.png)

- To logout of a remote server, type `exit`.

**Trying Some Commands**

All the commands that are normally available on your local machine are also available when logged into a server. The only difference is that you will be interacting with your files on the server rather than on your own computer. 

![Image](3.png)

**Moving Files with SCP**

Sometimes you want to copy files from your client to the server. This can be done with a command called `scp`, which stands for secure copy. Create a new file on your local machine, such as `WhereAmI.java` which has the following code:
```
class WhereAmI {

   public static void main(String[] args) {
   
   System.out.println(System.getProperty("os.name"));

   System.out.println(System.getProperty("user.name"));

   System.out.println(System.getProperty("user.home"));

   System.out.println(System.getProperty("user.dir"));

   }

 }
 ```


On your local machine, open a terminal from the directory that contains your file, run the command:  
`$ scp (local file’s name) cs15kwi22…@ieng6.ucsd.edu:(The directory you would like to place your file in on the server)`

An example using `WhereAmI.java` would look like this: 

`$ scp WhereAmI.java cs15lwi22zz@ieng6.ucsd.edu:~/`

Once your file is on the server, you can treat it as if it were on your client. For example, `WhereAmI.java` can be compiled and executed on the server: 

![Image](4.png)

**Setting an SSH key**

Constantly needing to type in your password is tedious. This can be solved with SSH keys. You can create a private and public key pair with the command `ssh-keygen`, give the public key to a server, and ssh is able to match the keys on your client and the server so you don't need to type your password every time you want to login. 
- Type `ssh-keygen` into your terminal on your local machine.
- Enter where you want the keys to be created, or just press enter to create them in the default directory
- If you want a passphrase for the private key, type it in. If not, just press enter 2 times. Notice the passphrase is for the private key, not the password that you use to login to the server. 

![Image](5.png)

- Go to the directory where you create the keys, you should see two files, `id_rsa` is the private key. `id_rsa.pub` is the public key. The private key file should be stored on your local machine, under `home directory/.ssh`
- Now you need to copy the public key to your account on the server. Log into your account, and create a directory called .ssh under home directory using this command:
 
`$ mkdir .ssh`
 
Logout by typing the command: `exit`.

- On your local machine, go to the directory where you store the public key, and run the command:

`$  scp id_rsa.pub cs15lwi2zz@ieng6.ucsd.edu:~/.ssh/authorized_keys`

This command will copy the public key file `id_rsa.pub` to your server's `home directory/.ssh` and rename it to `authorized_keys`. After this step, you will be able to run the `ssh` or `scp` command without typing your password.

![Image](6.png)

**Optimizing Remote Running**


If you want to edit a java program locally and run it on the remote server, You need to first edit your java file, then:

- copy it to the remote server

`$ scp WhereAmI.java cs15lwi22...@ieng6.ucsd.edu:~/`

- login to the server

`$ ssh cs15lwi22...@ieng6.ucsd.edu`

- compile it with the command javac on the server

`$ javac WhereAmI.java`

- run it with the command java on the server

`$ java WhereAmI`

Assuming you have all the commands typed in a text file, for each of the above commands, you need to click to go to the text file, highlight the command in the file, copy(`ctl-c`), click to go to the terminal, paste(`ctl-v`) to terminal, and hit `enter`. You need a total of 24 keystrokes/mouse clicks. It can take up to 40 seconds to do all the steps.

You can use semicolons to run multiple commands on the same line. You can also write a command in quotes at the end of an `ssh` command to directly run it on the remote server. As a result, the above four steps can be done in one line that looks like this:

`$ scp WhereAmI.java cs15lwi22...@ieng6.ucsd.edu:~/; ssh cs15lwi22...@ieng6.ucsd.edu "javac WhereAmI.java; java WhereAmI"`

Assuming you have this line typed in a text file, it takes 6 keystrokes/mouse clicks, and you can complete it in 7-10 seconds.


![Image](7.png)