---
inFeed: true
description: 'May 9, 2018'
dateModified: '2018-05-09T20:05:26.868Z'
datePublished: '2018-05-09T20:05:27.878Z'
title: Installing OpenOffice on Linux Ubuntu Unity (Deb & Rem?)
author: []
publisher: {}
via: {}
sourcePath: _posts/2018-05-09-installing-openoffice-on-linux-deb-and-rem.md
hasPage: true
starred: false
datePublishedOriginal: '2018-05-09T19:29:37.799Z'
url: installing-openoffice-on-linux-ubuntu-unity-deb-and-rem/index.html
_type: Article

---
# Installing OpenOffice on Linux Ubuntu Unity (Deb & Rem?)
![](https://the-grid-user-content.s3-us-west-2.amazonaws.com/93b0ac92-92f3-48e6-bf6f-c51b6954fcf3.png)

## LibreOffice and Microsoft Word Files are notoriously incompatible, so installing OpenOffice on a Linux distribution is a necessary addition. This post details how to **properly **install OpenOffice on a Ubuntu Unity Desktop. Here is help if you get a similar error:

    SAXParseException: '[word/document.xml line 2]: Attribute w:themeShade redefined ', Stream 'word/document.xml', Line 2, Column 73125(row,col).

May 9, 2018

Ryan Roe

---

## Introductory concepts: 

Unix is the great grandaddy operating systems of linux. Linux is the grandaddy of many open source operating systems used for development, server management, and for tech professionals. One could say Linux is the step father of MacOS. One of the notable open source operating systems that utilizes Linux is Ubuntu which is software that supports a computer's basic functions, such as scheduling tasks, executing applications, and controlling peripherals. Unity is a graphical shell for the GNOME desktop environment originally developed by Canonical Ltd. for its Ubuntu operating system.

Now that you understand the background, in Unity, LibreOffice is already downloaded (Word is not available on Linux based OS), however there are compatibility issues that take place when editing .docx (Microsoft Word files) that make them almost completely unreadable and your average user would have no idea how to recover the document.

## Problem:****

I opened a .docx file on Ubuntu, edited the file, changing colors of text etc. I saved teh file, uploaded it to dropbox. I came back a week later and opened the file using libreoffice and received an XML parsing error that would not allow me to open the file even using Word on a Windows laptop. 
    
    SAXParseException: '[word/document.xml line 2]: Attribute w:themeShade redefined ', Stream 'word/document.xml', Line 2, Column 73125(row,col).

So I turned to the internet to find a solution to repair the file. First is from **[Self-help methods to fix .docx files with SAXParse error. ][0]** I shortened for you because \#2 & \#3 did not work for me:

1. Download and open the file with Adobe Open Office
2. Zip the file, unzip it, edit the document.xml file and remove the problematic attributes
3. Zip the file, unzip it, extract all of the html tags using find and replace from Notepad++

So downloading Open Office allowed me to open the file, but this is no simple task on Ubuntu.

## **Downloading Open Office on Ubuntu**

[OpenOffice Download Information][1]

### Step 1: PreInstallation

Completely Remove LibreOffice. This is necessary because of dependency issues that OpenOffice has. Sorry, if you figure out how to keep them both, let me know. Run the following code from your home directory (open up terminal, type cd). 
    
    sudo apt-get -f remove libreoffice-common

    sudo apt-get purge libreoffice*

Remove any Symbolic Links (sym links are like shortcuts) to LibreOffice. Open terminal:

    whereis soffice

It will (most likely) return: 
    
    /usr/bin/soffice

Remove this symbolic link (or any others that appeared):

    rm /usr/bin/soffice

### Step 2: Download

[Download your favorite Linux version of Apache OpenOffice][2] Make sure that it corresponds with your operating systems 32bit vs 64 bit architecture AND your Linux Distribution

* .deb because it is based from debian like Ubuntu, and mint 
* .rpm files are for Redhat based distr like CentOS, Fedora

[0]: https://forum.openoffice.org/en/forum/viewtopic.php?f=7&t=80923&p=404588#p404588
[1]: https://www.openoffice.org/download/common/instructions.html#linux-preinstall
[2]: https://www.openoffice.org/download/