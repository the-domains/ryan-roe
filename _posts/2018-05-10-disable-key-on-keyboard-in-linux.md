---
inFeed: true
description: >-
  Keys on keyboards will malfunction and break so they either need to be
  remapped or removed.
dateModified: '2018-05-10T19:22:41.246Z'
datePublished: '2018-05-10T19:22:41.886Z'
title: Disable Key on Keyboard in Linux
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
# Disable Key on Keyboard in Linux

Keys on keyboards will malfunction and break so they either need to be remapped or removed.
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

Ryan Roe

[0]: http://www.geekyboy.com/archives/629
[1]: https://ccm.net/faq/3348-execute-a-script-at-startup-and-shutdown-on-ubuntu