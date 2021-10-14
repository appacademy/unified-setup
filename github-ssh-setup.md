# Using SSH Authorization for GitHub 
GitHub recently decided that password authentication from terminal was causing 
too many security issues. As a result, you can no longer authorize your terminal 
using your password and will instead have to use a Personal Access Token (PAT) 
or Secure Shell (SSH) for authorization. I prefer SSH authorization and have 
created this guide to help you get set up.

### Getting Started
Before we can go much further, we'll need to check to see if your terminal has 
an SSH agent running. Enter this command into your terminal and make make note 
of what follows

`ssh-add`

If you see nothing, you're in good shape. You can skip ahead to Creating Your 
Identity.

If you see a message stating something to the effect of

![](https://i.imgur.com/UvBqaE3.png)

You'll need to edit your .bashrc/.zshrc to make sure it starts each time.

`cd` to your Home directory then enter `code .bashrc` or `code .zshrc` depending 
on your operating system/shell of choice. If you're unsure of which one to 
enter, run `ls -a` and see which one already exists in your home folder.

Before editing your .bashrc/.zshrc you should back up what's currently there to 
avoid breaking things. Enter the command `cp .bashrc bashrccopy` or 
`cp .zshrc zshrccopy` depending on which file you have.

Once you've got the file opened in code, add this line to the bottom:
~~~
#Start SSH Agent
eval `ssh-agent -s`
~~~


### Creating your Identity
Now that we've got everything set up, let's create our identity.

Enter the following command (but fill in your GitHub email address where 
appropriate)

`ssh-keygen -t ed25519 -C "your_email@example.com"`

You should see output that looks similar to

![](https://i.imgur.com/Rq1NuwX.png)

For simplicity's sake, hit enter (you can change the default file name if you'd 
like or think you may set up different SSH keys for other services). 

Next it will ask you for a passphrase. Opinions will differ, but mine is this: 
I am the only person that uses this password protected computer and knows how 
to use terminal in my house. This computer is a desktop computer and has a low 
likelyhood of falling into nefarious hands. I did not create a passphrase for 
my SSH key.

Your opinion may differ, you may have concerns about people using your computer 
or even stealing your computer if it is a laptop. They could then theoretically 
have access to any private repos on GitHub that you have access to and with 
enough effort could really cause trouble for you. If this sounds like you, enter 
a passphrase at the following prompt. 
(Please note that when you take actions on GitHub you will be prompted for this 
passphrase each time. Make it something memorable)

![](https://i.imgur.com/f8PsCCK.png)

After entering your passphrase (or leaving it blank), it will then give you 
output that looks similar to this 

![](https://i.imgur.com/nL7kRN5.png)

With a lot more underneath 

Congratulations! You've generated your SSH identity and are almost ready to live 
a password/PAT free existence (unless you opted for a passphrase).

### Creating a Config file for your identity
After some initial feedback, this guide has been altered to be a bit more 
adaptable for folks that opt for the passphrase or rename their identity file. 
Let's start by going to our home directory 
`cd`
and then going into the .ssh directory
`cd .ssh`

Here, we're going to create a `config` file that lets us specify which key to 
use in what situations (helpful if you need to set up multiple accounts[though 
that will require some extra fiddling])

Enter the command `touch config` to create the config file. Next, we're going to 
open this directory with VSCode by entering `code .`

Your VSCode should show some contents in the folder already, namely your 
identity file, the .pub version of that file and the config file we just 
created. If you've used SSH in the past (or are revisiting this guide to create 
the config file) you may have some extra things as well. I've included a 
screenshot of my folder for reference.

![](https://i.imgur.com/B4EgwYd.png)

Click on config to open it with your editor. Once inside, we're going to add 
some lines to it to instruct SSH how to handle our identity when interacting 
with GitHub. I'll share what mine looks like and explain a bit about what each 
line does after.

```
Host github.com
    UpdateHostKeys yes
    IdentityFile /home/bill/.ssh/id_ed25519
```

`Host github.com` specifies that when our terminal is making contact with the 
host github.com it should take the following actions: 

`UpdateHostKeys yes` make sure that the keys provided by GitHub are up-to-date. 
This helps us make sure we're getting an appropriate connection and not being 
redirected/spoofed to somewhere else

`IdentityFile /home/bill/.ssh/id_ed25519` this is where the magic happens. This 
line instructs our terminal to add and make use of this specific identity file 
when communicating with GitHub. 

You'll want to add all of those lines, but alter the `IdentityFile` line to 
match your path. Easiest way to get the path is to right click on the file from 
the filebrowser in VSCode, then choose Copy Path

![](https://i.imgur.com/woRzg6y.png)

After you've got the path copied, you'll want to paste it in after your 
`IdentityFile` line. Afterwards, it should look somewhat like the example above.



### Adding your identity to GitHub
We're on the home stretch! You should still have your VSCode open in your .ssh 
directory. Click on the .pub version of your identity file and copy its contents 
to your clipboard. It should begin `ssh-ed25519`(or whatever your chosen 
encryption algorighm was) and end with your e-mail address.

Next we'll navigate to GitHub.com, click on your profile icon in the top right, 
then choose settings.

![](https://i.imgur.com/ZSxYHlb.png)

From there we'll go into SSH and GPG Keys

![](https://i.imgur.com/HED9PAZ.png)

Then New SSH Key![](https://i.imgur.com/ZQ6cnDE.png)
Here you'll give the key a descriptive title (so you know which machine/terminal 
it's for) and then paste the key you copied from the .pub file into the Key 
area. Once that's completed click Add SSH Key

![](https://i.imgur.com/zuiBZ0n.png)

And with that you should be all set!

### Using Your Awesome New SSH Key
To begin making use of your, navigate to a repo that you have access to on 
GitHub, click the green Code button on the middle-right and make sure the SSH 
option is selected and click the little copy button that looks like a clip 
board.

![](https://i.imgur.com/3eGg8va.png)

Navigate to an appropriate place with your terminal to clone the repo and 
`git clone` the repo.

When you use it for the first time with GitHub(and some subsequent times if you 
get routed to a different GitHub server) it will ask you if you trust this 
source. You will want to say that Yes, you trust it, otherwise you'll need to 
restart the process. 

If you specified a passphrase, you'll be prompted to enter the passphrase to 
complete any activity that requires authentication on GitHub. 

GitHub should now remember that you're using SSH, however make sure that future 
repo links follow the form `git@github.com:username/repo.git` rather than 
`https://github.com/username/repo.git`. When setting up repos, make sure you're 
on the correct link otherwise you'll run into trouble -- the Quick Setup page 
should look something like this, for reference 

![](https://i.imgur.com/KFlMbxJ.png)

### You're all set!
You've done it. You've created a new SSH identity file, created a configuration 
file for your SSH agent that instructs on how to behave with GitHub and ensured 
that GitHub is aware of the key and knows that it's you using it. You should 
give yourself a round of applause for not only your courage and bravery, but 
foresight and wisdom as well.

Happy hacking.