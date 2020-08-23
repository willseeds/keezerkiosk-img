#Keezer Kiosk IMG v1.0 (08-08-2020)

**********************************************
**************   KEEZER KIOSK   **************
**************    Image file    **************
**********************************************

// Keezer Kiosk project goal (1.0)
// - to create a touch-screen intranet accessible
// - LAMP website that allows for keezer management
// - to add/revise/delete beers and open/close taps
// - with the ability to report temp from a sensor

// opening
the Keezer Kiosk project was initially thought of after seeing the magic mirror project from Michael Teeuw, kinda before everyone was doing it and there was an easy img file. I liked the thought of feedback on the mirror using a webpage started in kiosk mode. i later discovered that i could use that same tech on another project i had been recently pondering.

i have been a home-brewer since 2015 and a electronics tinkerer since about the same time. after about two years of homebrewing i wanted a keezer, which is a chest-freezer that has the door taken off, a wood rim added, then the door reattached. It is a really simple idea that allows multiple taps to be served, depending only on the size of the freezer. With a simple temp controller for about $20, it will not freeze the beer and i know my worth ($20 to not let it keep the release hostage). there are dozens of how-tos on various search engines for building one. 

that leaves me with how to show people what is on tap. I saw many ways to use chalkboards, magnets and other ways to show what's on tap. for the last couple years I have used a small magnetic white board for the 3-tap system in my fridge. i didn't want to designate too many bells and whistles for this project, as it would never get done. in giving back to the two communities that i spent a lot of time learning from (and teaching others), i felt that it should be enough to allow immediate use, but still be a good platform for teaching php/mysql and coding basics. 

if you are a expert electronics tinkerer, learn to brew. if you brew, learn more about the raspberry pi you own and maybe break it a few times. seek out those of like-mindness such as electronic clubs or your local home-brewers club. i joined my local Greater Everett Brewers League (GEBL) and my tastes for beer have become very sharpened, and building this project helped me learn more about my next love, internet applications that i need in my life. ~cheers friends. 


// minimum requirements
(you)
zero HTML knowledge, or expertise
very little computing knowledge

(hardware)
external/internal home network
another computer to load initial software and share files
raspberry PI version 3 rev B (wifi) w/ a simple case & power
specific USB mouse and keyboard
32GB SD card 
old tv w/ HDMI connection for pi video

(wrap up)
touch monitor, HDMI connection or web-accessible monitor
waterproof DS18B20 Temperature sensor (w/ 6' cable length or more) 
1/2 sized breadboard w/ about 1' of wire
4.7K ohm resistor
of course, a keezer

*requirements note: spend the time learning before you invest in the wrap up parts. You may be able to spread the investment out as you learn. this was designed to be plug and play for someone with some simple computing skills.


//it can also
- run on any internal internet device, as long as it can show a webpage (smart tv, ipads/iphones, etc). It just has to be able to resolve the DNS query from that device to your router (which you should do for security anyway, not outside your network) and call it in a web browser using http://keezer/

- with that being said, be sure to check out the skinny version with a minimal header/footer; http://keezer/indextv.php. this is good for when you want people to see with their eyes and not their hands (mine is a touch-screen for the full effect). 

- split between two screens for even more taps! Just have a second webpage link; copy the index.php to index2.php. copy the globals.php file to globals2.php and edit the globals.php to call the 1st keezer total quantity of taps (vs. all quantity), while on globals2.php put the full quantity of taps in total so it will skip based on the index2.php $i variable. edit the "$i" variable on the index2.php page to be the number of the first tap on the second keezer (dare i say 'etc..'). Put screen over second keezer that is web-accessible and link to index2.php (does not have to be another full pi unless you want additional sensors or have enough CAT5 cable). 
 

// get up and going
this installation starts with putting on a SD card for a plug-in setup (step 1-4 below). the image file installation already has all the bells and whistles for using on first boot up. The links below do not review all the package installations and do not review anything Raspberry Pi. It just gets the Keezer Kiosk up and running. You can use these instructions to make as many keezer installations you want. just remember to rename the PI before joining your wifi network in thr Raspberry PI configuration. 

finalizing would be getting the 1-wire set up (step 5) and then work carefully to test pins (shutdown, unplug, tinker, plug in, boot, test... remember). the 1-wire connection is enabled on the image by default. you can change the temp reporting by setting "temp_f" to "temp_c" for applicable measurement at the bottom of the globals.php file (/var/www). everything will run without the sensor plugged in, but you might want to remove (or edit out) the degree symbol in the header.php files. using 1-wire and DS18B20 Temperature sensors, it will allow multiple sensors to be addressed, but only one was programmed for feedback for the purposes of this project. 


// set up
Step 1
- gather the initial hardware: 
   USB mouse, keyboard and hdmi connection to an old tv
   this is what it was tested to run on with a fresh install on Raspian (now called Raspberry OS), wifi with no issues.

- hardware list links:
   Raspberry PI (Rev 3 Vers.B, with wifi) & a 32gb SD card
   - use the wifi raspberry to minimize wires
   - go with Amazon for a good deal and fast shipping for both. Make sure its the right PI though.
   - if you are already on Adafruit: https://www.adafruit.com/product/3055
   - don't forget to order a power connection too!

   if you order from Adafruit, you can get the half-sized breadboard for making sensor connections here:
   - https://www.adafruit.com/product/1609

   and a wiring bundle package (there are cheaper, you will only need about 1')
   - https://www.adafruit.com/product/153

   DS18B20 - Waterproof sensor (with 6' extension for reaching inside your keezer)
   - you need to order 4.7K ohm resistor with this!
   - if more distance is needed, try splicing in CAT5 cable between the PI and sensor.
   - https://www.adafruit.com/product/381?gclid=EAIaIQobChMIzMrHxtbc6gIVlh6tBh3R0gpOEAAYASAAEgK8l_D_BwE

   if you have hardware issues (keyboard/mouse), try different hardware. 


Step 2
- download info
   download 8gb image from my Google Drive (KeezerKiosk-v1-8GBSD (08-08-2020).img):
   https://drive.google.com/file/d/1jV_Ab5kSmzc5rdaup32u-4dqu-8yMTAj/view?usp=sharing

   zip file of only the website files (if you need backup files):
   https://drive.google.com/file/d/106zigLnzKdHQyBHhygDxb7cb85RPfRRY/view?usp=sharing

   on Google Drive public sharing (info only):
   https://gsuitetips.com/tips/drive/share-a-google-drive-file-publicly/

- the image install part
   install Win32DiskImager
   https://sourceforge.net/projects/win32diskimager/

   install SD card formatter to format the card if the imager hangs.
   https://www.sdcard.org/downloads/formatter/

   if you are using Windows, the app "Rocketcake" is a pretty good editor (not required).
   
- put image on SD card (8-32gb card, 32gb suggested)
   insert the SD card into the adapter and put in your computer.

   your computer may prompt what to do with it, just make sure it is a working SD.

   close any windows and verify the contents can be deleted.

   Open SD card formatter. Format using quick-format. then close the SD card formatter.

   Open Win32DiskImager. Point the link on top to the .img file you downloaded. Click write. 

   when complete, close the program and remove the SD card from the adapter and put in the PI (gold up).   

- once you have all the connections to the PI, the power connection is last. verify connections and power.
   if it doesnt power when applied, check for power switch on cord.


Step 3
- since this is an image file made from an 8gb, its missing a lot of programs, but will be functioning website. 

- when the system boots up, it is set to the greatest coast (West coast, PST) and the passwords for root and pi are already set.

- the system should boot up with an opening firefox window, showing the Keezer Kiosk website.
   if you installed the temp sensor correctly, this should be showing too.

- change the computer name and Localization (requires reboot), by clicking the menu button in the upper left and clicking Preferences, then Raspberry PI configuration. Do this before joining your wifi network, so it doesn’t cause issues resolving at the router.

- last item before going online, reset root user password
   click icon for the command prompt in the taskbar and type; "sudo passwd root" to change the rarely used admin user password.
   between the pi account and the one for the admin side (called 'root') of the database (which should be different passwords), you shouldn't need more. do this for the pi user also typing; "sudo passwd pi"
   the 'keezer' user is only in the database.

   initial passwords on the system;
      root: beerl0ver425 (system and database)
      pi: beerl0ver (system only)
      keezer: beerl0ve (update later using 'sudo nano /vaw/www/keezerdb.php')

- in the taskbar, use the wifi network scanner to locate and join your network.

- on the command line, run ‘sudo apt-get update’ (answering yes to the size questions).

- installed packages 
   apache2 (webserver)
   mariadb-server (SQL)
   php-MySQL
   phpmyadmin (SQL admin)
   nano (command line text editor)
   iceweasel (firefox for PI)

- update phpmyadmin
   visit "localhost/phpmyadmin" from the opened webpage.
   enter root user and password "beerl0ver425".
   click on the "user accounts" on the upper-right.
   on the right of each user, click 'Edit privileges'.
   click 'Change password' at the top again.
   do this for every user, keeping the root and phpmyadmin (first) password the same.
   changing root password last as it will void your phpmyadmin login and password.
   changing 'keezer' password will require the password to updated in /var/www/keezerdb.php
     from the command line type; "sudo nano /vaw/www/keezerdb.php"
     update keezer password and use keyboard CTRL+X and hit "Y" and enter.
   visit http://localhost

- edit for your keezer config
   from the command prompt one more time 'sudo nano /vaw/www/config.php'
   edit your keezer name, tap count, temp and color (black and white initially) 

Step 4 
- go back to your original computer and attempt to find the PI on your network.

- the default name of the Raspberry PI image is 'keezer' 
   if you didn't change the PI's name; on your computer internet browser type: "http://keezer/"
   you should see the Keezer Kiosk website on your other computer. 

- try "http://keezer/phpmyadmin" and use your root credentials (with updated passwd) and can use keezer but will have limited functionality.
   you can enter all your beer info here because its easier to copy/paste into the keezer database.
   reveiw how the beers are put on tap by entries in the database.
   make sure you take advantage of future/past beers.


Step 5
- 1-wire info
   How the 1-wire is connected
   https://thepihut.com/blogs/raspberry-pi-tutorials/18095732-sensors-temperature-with-the-1-wire-interface-and-the-ds18b20

   Check out Tim's w1thermsensor package that can verify your 1-wire serial numbers and connectivity.
   https://github.com/timofurrer/w1thermsensor

   and this one that shows a lot about the w1thermsensor
   https://bigl.es/ds18b20-temperature-sensor-with-python-raspberry-pi/


// sensors
i used the waterproof DS18B20 Temperature sensor and found it was not actually working correctly and fried my pi checking pins, so i bought two more pis/sensors (keeping one each secure for future known-good testing). before you starting hacking on the code, make sure the wiring connections are sound using a known-good voltmeter AND code snippets. 


// tap management
I tried to make the config file the only thing you need to update for all pages, so if you go beyond eight taps, you may have to update some code. start by adding your info to the config.php file and look at the site. you can edit the css files for text size/color and font. design is mostly based on a loop, based on $tapcount in the config.php file, so more than 8 taps should be able to be used (screen limiting). look through the simple design of the database. you cannot have things "on tap" and be "kicked". you can physically enter two beers with the same tap, but it may cause a conflict in tap-counting sql queries. my suggestion is to use as it was planned to be; a brewery management system. enter planned beers in the future with a little info. on brew-day enter a little more info, along with more info when it is kegged. You can go into the database and see the entries flowing down and to the right. there are also comments in the page queries that you might want to see if you think the database is missing something. entries not performed in the web-interface may affect functionality. try to minimize moving tables around, changing keys or renaming fields. if you want to add functionality, use new variable names. i found it easier to manage outside of the system and my first drinks would populate the keezer info (name, dates, comments, etc). 


// my lessons learned, your warning
- do not expose this website to the internet. if you have to, pull the admin stuff (but then whats the point).
- backup your data. even though its on a SD card, not just your webroot, the whole thing. at least your database...
- use known-good equipment. i tried a new meter and toasted a pi. swapping the SD card to another was a minimal impact.
- if you suspect malicious intent, look up how to lock down the admin folder with an .htaccess file ;)


// links, shout-outs and notable mentions
After seeing the Magic Mirror project, i thought of other ways to use Michael Teeuw's original version of the magic mirror. it was a little outside of my skillset at the time, but i loved the idea of a kiosk-style website. shortly after seeing this and thinking how i could use it, i came up with the Keezer Kiosk project. 
   https://michaelteeuw.nl/post/80391333672/magic-mirror-part-i-the-idea-the-mirror

Tania Rascia's excellent article on building a simple CRUD database app allowed me to get back up to date with new PHP/SQL coding examples along with setting the stage for how much of the Keezer Kiosk project was structured. 
   https://www.taniarascia.com/create-a-simple-database-app-connecting-to-mysql-with-php/

DS18B20 Temperature sensor (get the waterproof ones on Adafruit for around $10/ea)
i suggest this sensor for the ability to just add in another sensor (1-wire) and the system will pick it up on booting. this functionality was designed in for the use of 1 sensor for just keezer temperature.
   The code used in this was based on bouncymat's post on this string:
   https://www.raspberrypi.org/forums/viewtopic.php?t=35487

Raspberry Pi Touch Display - 7" touch screen and case for about $90
   https://www.raspberrypi.org/documentation/hardware/display/

cron for backing up mysql/site
   set up time-interval backups locally or over your network (mine goes to a nas)
   https://www.raspberrypi.org/documentation/linux/usage/cron.md

*final note: nothing was ever learned without breaking it first.


// about @willseeds
most of my interests come from my 90's teen-life which includes my music interests in rock, metal and even some oldies. along with making beer an tinkering on electronics, i find myself working in the aerospace industry as a technical expert for a daily job. i have held mostly production jobs at companies such as Apple, Boeing and Microsoft. there's also a decent background in construction, computer aided drafting (CAD) and CNC programming. i am also known to snowboard, ride atvs and camp when i can. issues with my right shoulder in February 2020, just as a major pandemic hits, made it almost unbearable to cope with daily life and this project was my only focus to keep my sanity (i know, go figure). i hope to put a lot of this behind me and get back to brewing, my next electronics project and maybe learn to fly small airplanes soon. 


// about @keezerkiosk
  Started 5.6.20 - 1.0 image released 8.8.20
  Target Goal: create a simple 
  touch-management viewable website 
  for showing keezer contents and
  history for 2 to 8 taps. 

  include insert/update/delete ability on past/upcoming
  beers for easy brewing/keezer management.

  simple HTML pages (with .php extension)
   - use include/require to add functionality
   - leave out the ID and SQL stuff from the user
   - source pages and phpMySQLadmin tables contain SQL understanding
   - admin area for add/edit/delete
   - touch-only for users, admin will need keyboard/mouse
   - globals page for keezer name, tap count, colors

The site was designed to be accessible from an internal network with very little computing knowledge. i tried to point out areas that will cause conflict, but learning is the point of this, not a full-free commercial application. The files were put directly on the site as opposed to the sub-folder method used on the original release. this was designed to be an out-of-the-box application for those that prefer to use the product and not figure it out. :) 

***WARNING***
This site was not designed for external exposure to the internet. Only for internal/local network. It should for no reason at all be exposed to the external internet. If you want to show friends/family take a picture or invite them over for a beer and surprise them. 

-------

Happy Brewing and Cheers!

-------