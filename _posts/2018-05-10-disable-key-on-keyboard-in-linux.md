---
inFeed: true
description: >-
  Keys on keyboards will malfunction and break so they either need to be
  remapped or removed. 
dateModified: '2018-05-10T18:48:43.653Z'
datePublished: '2018-05-10T18:48:44.017Z'
title: Disable Key on Keyboard in Linux
author: []
publisher: {}
via: {}
hasPage: true
starred: false
datePublishedOriginal: '2018-05-10T18:48:44.017Z'
sourcePath: _posts/2018-05-10-disable-key-on-keyboard-in-linux.md
url: disable-key-on-keyboard-in-linux/index.html
_type: Article

---
# Disable Key on Keyboard in Linux

Keys on keyboards will malfunction and break so they either need to be remapped or removed. ![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/08d9fb1c-83ef-4696-9fb7-dbfb9de4b4ab.png)

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

If you would like to learn how to remap the keys, Google it. Typing 'man xev' will get you started.

Ryan Roe