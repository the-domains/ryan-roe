---
inFeed: true
description: >-
  Keys on keyboards will malfunction and break so their keycode needs to be
  remapped or removed.
dateModified: '2018-06-28T06:48:07.511Z'
datePublished: '2018-06-28T06:48:08.489Z'
title: Disable a Key on your Keyboard in Linux and MAC
author: []
publisher: {}
via: {}
hasPage: true
sourcePath: _posts/2018-05-10-disable-key-on-keyboard-in-linux.md
starred: false
datePublishedOriginal: '2018-05-10T18:48:44.922Z'
url: disable-key-on-keyboard-in-linux/index.html
_type: Article

---
# Disable a Key on your Keyboard in Linux and MAC

Keys on keyboards will malfunction and break so their keycode needs to be remapped or removed.
![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/08d9fb1c-83ef-4696-9fb7-dbfb9de4b4ab.png)

Thread: Personal Development

May 10, 2018

Ryan Roe

---

My keyboard pressed and held the "+" key by the keypad by itself. So to disable this:

## Check your keyboard mappings

Open up the terminal.

    xmodmap -pke #//this command shows the mappings to all the keyboard buttons
    xev -event keyboard #//this allows you to press buttons on the keyboard to test for the mapping
    ##//You are looking for the keycode Ex: the '+' beside the numpad is keycode = 86
    ##//once you find the key code run:
    xmodmap -e "keycode 86 = " #//this disables the key
    

![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/039e21d9-01a6-49da-8e15-fbe276c912ef.png)

If you would like to learn how to remap the keys, Google it. Typing 'man xev' in terminal will get you started.

This script needs to be run everytime the computer is booted up so put it in the /etc/rc.local file

    cd
    
    cd/etc
    
    vi/etc/rc.local

* Input the command (research how to edit in VI)
* Then save it pressing Esc then typing ':w !sudo tee %' press enter
  * this is a read only file so you are unable to save it
  * Taken from [Adam Culp][0]
  * :w = Write a file.
  * !sudo = Call shell sudo command.
  * tee = The output of the vi/vim write command is redirected using tee.
  * % = Triggers the use of the current filename.
  * Simply put, the 'tee' command is run as sudo and follows the vi/vim command on the current filename given.

* [Link to create startup, shutdown scripts][1]

## Update May 11, 2018

The xmodmap function is only a temporary remapping and will be reset to default even in the same session. A full description of what is going on here is in this Medium article, [A Simple but Comprehensive Guide to XKB for Linux][2]. Basically, to make the change persist, you need to create a new file and add the script into it.

    #Open up terminal
    cd
    vi ~/.Xmodmap 
      #Type i to insert text
      xmodmap -e "keycode 86 = "
      #ESC :wq!

Ryan Roe

[0]: http://www.geekyboy.com/archives/629
[1]: https://ccm.net/faq/3348-execute-a-script-at-startup-and-shutdown-on-ubuntu
[2]: https://medium.com/@damko/a-simple-humble-but-comprehensive-guide-to-xkb-for-linux-6f1ad5e13450