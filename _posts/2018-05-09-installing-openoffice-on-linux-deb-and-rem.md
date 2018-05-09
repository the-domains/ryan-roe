---
inFeed: true
description: 'May 9, 2018'
dateModified: '2018-05-09T19:46:24.122Z'
datePublished: '2018-05-09T19:46:24.914Z'
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

## LibreOffice and Microsoft Word Files are notoriously incompatible, so installing OpenOffice on a Linux distribution is a necessary addition. This post details how to **properly **install OpenOffice on a Ubuntu Unity Desktop.

May 9, 2018

Ryan Roe

---

Introductory concepts: Unix is the great grandaddy operating systems of linux. Linux is the grandaddy of many open source operating systems used for development, server management, and for tech professionals. One could say Linux is the step father of MacOS. One of the notable open source operating systems that utilizes Linux is Ubuntu which is software that supports a computer's basic functions, such as scheduling tasks, executing applications, and controlling peripherals. Unity is a graphical shell for the GNOME desktop environment originally developed by Canonical Ltd. for its Ubuntu operating system.

Now that you understand the background, in Unity, LibreOffice is already downloaded (Word is not available on Linux based OS), however there are compatibility issues that take place when editing .docx (Microsoft Word files) that make them almost completely unreadable and your average user would have no idea how to recover the document.

**Problem: **I opened a .docx file on Ubuntu, edited the file, changing colors of text etc. I saved teh file, uploaded it to dropbox. I came back a week later and opened the file using libreoffice and received an XML parsing error that would not allow me to open the file even using word 
    
    SAXParseException: '[word/document.xml line 2]: Attribute w:themeShade redefined ', Stream 'word/document.xml', Line 2, Column 73125(row,col).