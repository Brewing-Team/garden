---
title: "[UPDATE] [Dolphin [KDE file explorer]] After very long and several months of testing (it's a CORE piece of KDE)...I decided that 33 out of 117 community-made plugins are actually useful and worth to be installed. What about you?"
source: "https://www.reddit.com/r/kde/comments/1rugryk/update_dolphin_kde_file_explorer_after_very_long/"
author:
  - "[[RebirdgeCardiologist]]"
published: 2026-03-15
created: 2026-03-15
description: "Reddit is where millions of people gather for conversations about the things they care about, in over 100,000 subreddit communities."
tags:
  - "clippings"
---
For those who missed the previous post with all details, I give you the direct URL to the post \[[reddit](https://www.reddit.com/r/kde/comments/1p41hu2/dolphin_kde_file_explorer_has_a_rich_context_menu/)\].

\--

So, I tested every single plugin I installed on my machine.

...this time it took really...really...really...long time to do it.

After this process...out of 117...33 plugins has been kept, are installed...all the rest is gone.

PLUGINS that are actually USEFUL (there is a reason they are installed, not just "cool having plugins"...I asked myself "Do I need this plugin? Yes or No": no "maybe/maybe not" type of answers allowed).

\--

Long work, but it was worth to be done (especially sharing with KDE community).

\--

The last time, they were too many and above all, there were several problems:

- the context menu was huge, and it occupied all the vertical space available, it was very problematic, no "Properties" entries visible:
	- since the number of plugins set to appear in context menu (the most problematic scenario was the "blank" right click, that is non selecting a specific file) was greater than the number of entries displayable, "Properties" entry (the last one in order) was not easily accessible;
	- You know how Dolphin context menu looks like and how it is organized (5 sections, from top to bottom, the 4th is the one for plugins, similar to how a browser's context menu works) and the "Properties" entry is in the last one in the context menu;
	- Since I used often "Properties" section, it was very problematic to reach (I had to move with arrow keys, see current entry selected (blue background) and move to the top. Then, If you have focus on the first entry, you move back (up key) and it goes in last (from top) entry, "Properties". Enter key).
- a good amount of them do not work AT ALL, broken, not maintained. It's when something is called "deprecated" ;
- another important amount of them threw errors via KDialog (e.g."VSCodium not installed", even though I have it installed);
- others (not many) of them worked, but not completely (they stopped at last/second-last step of what they were suppose to do, or they showed an empty window with no info);
- some plugins were doing all the same things (e.g. operations with PDF files);
- 1 was not needed anymore since Dolphin integrated naturally (e.g. Sharing via Bluetooth).

\--

Using a previous major version of KDE (5.27.12), and not the last (6.6.2 if I remember correctly) affected the evaluation?

Absolutely yes, but that's what I'm using right now (kubuntu 24.04.03 LTS). See this comment \[[reddit](https://www.reddit.com/r/kde/comments/1r4jq74/comment/o5hyglf/)\] I wrote before to understand better why I use KDE5...in short that's the DE' version of the latest LTS of kubuntu, that's Ubuntu + KDE.

\--

So...

33 plugins were and ARE actually useful.

If I missed something (duplicate plugins for same stuff, using them) LET me know. I'm here for this too.

\--

The list of my installed plugins is the following:

1. launch\_lshw
	- Why > launche KDialog with List Hardware info. Useful if you need to have all this infos quickly to copy & paste.
2. Set as wallpaper and lockscreen
	- Why > change desktop wallpaper and lock screen image. Self-explanatory.
3. external\_ip
	- Why > retrieve your external-ip in a KDialog popup. Sometimes is really useful.
4. k4DirStat Here \[folder statistics\]
	- Why > Open folder statistics program 'k4dirstat' in the selected place. When you need to analyze that portion of memory, not all (like if you open k4dirstat directly).
5. Reverse Image Search
	- Why > search images using known reverse image search engines. Avoid several steps (open browsers, go to website, upload it, etc.).
6. VLC\_flatpak
	- Why > Launch file using VLC (installed the Flatpak version, via Discover), add to playlist.
7. Open with Live Server
	- Why > open selected directory on [http://127.0.0.1:5555/](http://127.0.0.1:5555/) with your default web browser. Useful when you want a raw view, just the content (CLI-like, no GUI).
8. Rename the PDF file to its title
	- Why > rename the PDF file to its title. This especially useful with research papers: they often are named weirdly by publisher, so you gen have as filename the real title of the PDF file.
9. Open with Kate \[Select Sessions or Instances\]
	- Why > allow to open the selected files with the Kate text editor, in particular within one of the opened windows or in a session previously stored. Self-explanatory.
10. Share with LocalSend Flatpak
- Why > share selected file(s) and/or folder(s) with LocalSend (installed the Flatpak version, via Discover). Self-explanatory.
1. usb\_devices
- Why > pipe usb-devices through kdialog. So you do not have to open a terminal and issue manually. Useful if you need to have all this infos quickly to copy & paste (or troubleshooting).
1. Read-It
- Why > perform quick OCR for images. It creates a new txt file with the same filename of the file whose you perform OCR on. Very hand when you need/want to do in snap.
1. distro\_info
- Why > give detailed info on your linux distro. Useful if you need to have all this infos quickly to copy & paste (or troubleshooting especially on Reddit).
1. Extract AppImage
- Why > extract the AppImage application to the folder, with the name of the application, with one click. Useful to answer questions like "what's in this black box?".
1. New folder from selected
- Why > create a new folder containing the selected files. All I say is...I use it every single day.
1. Export LibreOffice and Office documents to PDF
- Why > export LibreOffice format files to PDF in a quick and handy way. Self-explanatory.
1. Create Link in Desktop
- Why > generate shortcut(s) with just a click. Self-explanatory.
1. launch\_resolution
- Why > shows current resolution and refresh rate. Sometimes is really useful.
1. Export Markdown documents as PDFs
- Why > export Markdown files to PDF in a quick and handy way. Self-explanatory.
1. Compose with Thunderbird Flatpak edition
- Why > compose a new email using the selected files as attachments (installed the Flatpak version, via Discover). It also allows caching files from different folders and composing them later. Handy when you need to send an email.
1. last\_system\_boot
- Why > show last time system was booted.. Useful if you need to have all this infos quickly to copy & paste (or troubleshooting especially on Reddit).
1. launch\_kinfocenter
- Why > open quickly kinfocenter. Just this.
1. Install Debian Packages with konsole
- Why > allow to install debian packages quickly via the Konsole (GUI for .deb files).
1. KDE-Services
- Why > THE BIG ONE (probably the richest, most features-rich). Includes several 20 submenus
	- Actions, AVI Tools, Android Tools, Backup Tools, CheckSum Tools, Dolphin Tools, Dropbox Tools, Graphic Tools, ISO-9660 Image Tools, MEGA Tools, Midnight Tools, Multimedia Tools, Network Tools, PDF Tools, Package Tools, SSH Tools, Search Tools, Security Tools (2 with same name, but different entries), System Tools, Terminal Tools, Youtube Tools.
1. Make notes Spectacle
- Why > annotate images using spectacle (launch in edit mode directly). Self-explanatory.
1. Color Folder
- Why > a simple one: just change the color of folders (blue default, sometimes for special folder, I want to differentiate them so they stand out from the crowd).
1. KDE 5 Service Menu PDF
- Why > I know there is "PDF Tools" submenu from KDE-Services, but this one seemed to have more features for PDF files compared to the other plugin.
	- Am I right? Or did I miss something?
1. Git Tools
- Why > For those who know Git, this is not something new at all. It a gui for a collection of essential git commands needed to manage local git repositories.
1. Refresh
- Why > Refresh View (other options are F5 or in toolbar > View > Refresh). Having a context menu option is handy (and more quickly). Self-explanatory.
1. Open\_Doublecmd\_Open\_Doublecmd\_root
- Why > I use Double Commander as second file manager (Dolphin is the main core). I use it a "back up", "different experience" scenarios. It opens currently opened path into Double Command as user or as Root.
1. Copy to klipper \[file name path dirname hash and more\]
- Why > allow to copy to the clipboard through the Klipper, D-Bus service, several details about the selected files, like the filename, full filename, file path, file permissions. Very very useful when you need to get just a details of a file.
1. Quick backup and restore files
- Why > I know there is "PDF Tools" submenu from KDE-Services, but this one seemed to have more features for PDF files compared to the other plugin.
	- Am I right? Or did I miss something?
1. 7zip Service
- Why > have a right-click context menu for 7zip: in Linux there is no native menu. I know there is CLI option (I use it too) and GUI option (Ark is great, no problem with them), but home is home (consistency across OSs).

\--

All the other plugins were removed/uninstalled.

NOT Installed:

1. Write ISO to USB drive \[isoimagewriter\]
2. Add exe games to Lutris library
3. Open Dolphin as root \[KDE5/KDE6\]
4. USB Formatter \[mintstick\]\[gnome-disks\]
5. Menu set Login Manager gif
6. KDE 5 Service Menu Reimage
7. Open in VSCode / VS Code
8. etch-file-to-disk
9. Remove Metadata
10. Converter
11. Create folder from selected files
12. audiokonverter
13. KDE Connect Enviar a Menu
14. Advanced Rename Options open files with kRename
15. Send to Chromecast
16. Do All With PDF
17. Download with yt-dlp here \[youtube and other social media\]
18. Edit in kate
19. KDE 5 Template Manager
20. Convert video files to \*.mp3
21. Convert to webm/mp4
22. Compose with Thunderbird
23. Compare using Meld
24. Install Flatpak Service Menu - as user or system-wide
25. Office Converter Service Menu
26. pdf2image
27. Copy File Name
28. \[NEW\] Send file with Telegram using Telegram Desktop
29. OCR using Tesseract
30. Rotate or flip images
31. Resize images
32. Meld Menu
33. Open with VSCodium
34. JetBrains Dolphin Plugin
35. Send via bluetooth
36. Make multiple script or binary executable
37. Notepadqq Open with Service Menu - Quick Simple Install
38. Dolphin JSON tools - service menu
39. Find with kFind
40. Shortcuts for Windows executable files
41. makePDF
42. Build Dockerfile
43. VirusTotal
44. kiview
45. installdebs
46. Extract Icons
47. Image Information Identity
48. OCR PDF
49. VirusTotal Uploader Scan Analyze Menu - Quick Simple Install
50. Annotate-it
51. launch\_hardinfo
52. Partitions
53. imgur-servicemenu
54. Test Archive Verify
55. get\_PATH
56. launch\_plasma\_system\_settings
57. Reverse Image Search
58. launch\_hw\_info
59. open\_with\_gedit
60. Open with Kate \[Select Sessions or Instaces\]
61. launch\_speedtest-cli
62. date\_distro\_installed
63. Multi-File Total Media Duration //??
64. Print PDFs - Dolphin Service Menu
65. Wipe Partitions
66. Open Random File
67. Toggle Terminal Panel
68. Toggle Hidden Files View
69. Bionic Batch Renamer
70. Peazip Flatpak Service Menu
71. SystemUpdateMenu
72. Dolphin service menu to add ISO to grub
73. ShowMetadata
74. Add to Steam
75. Java(tm)
76. Play on Smart TV
77. View on TV
78. Dolphin-PowerActions
79. Lock It (File Locker/Unlocker)
80. Clonator ICON
81. Convert rpm2deb
82. list files
83. LateX Service Menu
84. Audiometadata

\--

Have you changed the plugins you use in Dolphin during these 4 months?

If yes, which one(s)? Anything new?

Comment on my choice? What about you?

\--

![r/kde - [UPDATE] [Dolphin [KDE file explorer]] After very long and several months of testing (it's a CORE piece of KDE)...I decided that 33 out of 117 community-made plugins are actually useful and worth to be installed. What about you?](https://preview.redd.it/update-dolphin-kde-file-explorer-after-very-long-and-v0-cb2iojjbl6pg1.jpeg?width=640&crop=smart&auto=webp&s=9ab64c7746ca275e88b6f1cf25ebf9b0c662eed8)

---

## Comments

> **AutoModerator** • [1 points](https://reddit.com/r/kde/comments/1rugryk/comment/oal233j/) •
> 
> Thank you for your submission.
> 
> The KDE community supports the Fediverse and open source social media platforms over proprietary and user-abusing outlets. Consider visiting and submitting your posts to our community on [Lemmy](https://lemmy.kde.social/) and visiting our forum at [KDE Discuss](https://discuss.kde.org/) to talk about KDE.
> 
> *I am a bot, and this action was performed automatically. Please* [*contact the moderators of this subreddit*](https://www.reddit.com/message/compose/?to=/r/kde) *if you have any questions or concerns.*

> **UKZzHELLRAISER** • [4 points](https://reddit.com/r/kde/comments/1rugryk/comment/oal310l/) •
> 
> Saving the hell out of this list. Havent read it in full yet but already seen some out of both the keep and remove list that I could want.

> **goodwill764** • [3 points](https://reddit.com/r/kde/comments/1rugryk/comment/oal41od/) •
> 
> KISS: 0 and used specific applications for every case.