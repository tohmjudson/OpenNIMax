This is an original post written for my blog on Wednesday, January 12th, 2011 as a way to get the Kinect working on the Mac and working with Max. I had lost it in a database issue and thought, though the tech is now outdated, it would be worth archiving.  Here it is, brought back to life from the ether by the amazing [Wayback Machine](https://web.archive.org/web/20110209113113/http://tohmjudson.com/?p=30).

## OpenNI to Max/MSP via OSC

[OpenNI](http://www.openni.org/) is a “natural interaction” software that uses the [Kinect](http://www.xbox.com/en-US/kinect) for XBox 360\. Using this, connected to a Mac, we can control various software via OSC. Here, I will show you how to get the data into [Max](http://cycling74.com/). The idea here is that you are like me, longing to try, but missing the few crucial steps that the README’s forget about the amateur hacker.

## Preliminaries:

First, if you are not comfortable with the terminal, I will try to walk you through it. Everything in this tutorial will require being in the terminal. That does not mean that it is hard, just different for many of us.

Second, I have tried this on three machines just to be safe that I did not ruin anything. My school computer went first (17” MacBook Pro 2006, 2.33 ghz), then my old Mac Mini (1.83 ghz, 2006) and now my MacBook Pro (2008, 2.4 ghz). All are working great. All are Intel. I can make no promises about your machine… but mine are all running smooth.

Third… I cannot help you. I would not even know where to begin. I am amazed that I have gotten this to work as it is with out something catching on fire or opening a hole to [the Nether](http://www.minecraftwiki.net/wiki/The_Nether)… there are far better programmers that could help you further than I ever will.

### A Brief Terminal Primer (all you will need to know; no more, no less)

_Where is it?_

Applications > Utilities > Terminal

_What to do with it for now?_

Add it to your Dock if you don’t have it there… trust me on this one… you will use it a lot

_What code will I need to know?_

**sudo**= superuser… makes things happen. [See this for more info](http://xkcd.com/149/)

**cd**= change directory

Quick Tip: Drag a <span style="text-decoration: underline;">folder</span> into terminal of where you want to go after typing cd[single space] to save from typing.

### **Software you will need to install before beginning with the OpenNI fun (all free, as in beer):**

1.  Install [Xcode](http://developer.apple.com/technologies/tools/xcode.html)
2.  Install [CMake](http://www.cmake.org/)
3.  Install [MacPorts](http://www.macports.org/install.php)

*** Click “Select Command Line Links” when finishing up MacPorts install, its very important for the next steps***

<span style="text-decoration: underline;">RESTART</span>

1.  Open the Terminal (in your Dock right? I warned you…)
2.  Type: `sudo port install libtool`

Be patient, MacPorts is flying through the interwebs getting you files for you. It took about 20 minutes to run its course for me… just enough time to catch up on some [music tech news](http://createdigitalmusic.com/) or a [little humor](http://theoatmeal.com/).

<span style="text-decoration: underline;">RESTART</span>

1.  Back in Terminal, Run: `sudo port install libusb-devel +universal`

*** Do not forget the +universal, it’s very important as well!!***

This takes awhile as well, get comfortable and perhaps enjoy a little light reading or a movie (yes, it is that long… your mileage may vary).

<span style="text-decoration: underline;">Again RESTART</span>

If you have troubles with the Macports portion, I have been getting good feedback about the [Homebrew](http://mxcl.github.com/homebrew/) version of the install. More on that [here](http://openkinect.org/wiki/Getting_Started#Homebrew). I personally have not tried it yet, but plan to on my next install (plus you gotta love the “Macports driving you to drink? Try Homebrew!” motto)

## **Into OpenNI (finally)**

### OpenNI:

1.  You will need [the latest unstable](http://www.openni.org/downloadfiles/openni-binaries/20-latest-unstable) version (be brave) for Mac. Be sure to download the mac version found at the bottom only, do not go to the github link at the top of the page!
2.  Create a **OpenNI** Folder in your Documents (I use that here because it is clean, you may need/want to put it elsewhere).
3.  Unpack the download and drag into an newly unpacked OpenNI… folder in your Documents> OpenNI folder
4.  Navigate to the <span style="text-decoration: underline;">folder</span> using the terminal. Type (or drag the visible folder after a space following cd):

cd (folderpath)

example:

cd /Users/YOURUSERHERE/Documents/OpenNI/OpenNI-Bin-MacOSX-v1.0.0.25

1.  Hit Enter to select that folder and in the terminal type:

`sudo ./install.sh`

### SensorKinect

The avin2 version worked best for me. I had tried two others, but had problems, not sure why… get it here:

[https://github.com/avin2/SensorKinect](https://github.com/avin2/SensorKinect)

Please note, versions vary, I will not be typing out versions numbers for now.

1.  Unpack the avin2 SensorKinect file and drag into your OpenNI folder
2.  Navigate through the SensorKinect folder to: avin2…>Bin>… And unpack the SensorKinect-MacOSX-5.0.0.tar.bz2
3.  Navigate to the new folder using the terminal

cd (folderpath)

example:

`cd /Users/YOURUSERNAME/Documents/OpenNI/avin2…/Bin/SensorKinect-MAcOSX5.0.0.25`

1.  Hit Enter and in the terminal type

`sudo ./install.sh`

### NITE

Again, you need [the latest unstable](http://www.openni.org/downloadfiles/openni-compliant-middleware-binaries/33-latest-unstable)

1.  Unpack the NITE file download and drag into your OpenNI folder
2.  Navigate to the new folder using the terminal

`cd (folderpath)`

example:

`cd /Users/YOURUSERNAME/Documents/OpenNI/Nite…/`

1.  Hit Enter and in the terminal type: <span style="font-family: monospace;">sudo ./install.sh</span>
2.  The Primesense license key is found on their site and is **0KOIk2JeIBYClPWVnMoRKn5cdY4=**
3.  Hit Enter

COPY FILES…

***This is important, or you will get errors. Copy the 3 files from avin2…>NITE>Data to Nite-1.3.0.18>Data. It is ok to replace these files***

FIRST TEST:

1.  In Terminal change directory to the Nite…> Samples> Bin>
2.  Run the **Sample-PointViewer** program (you can just drag it into the terminal and hit enter)
3.  Wave your hands like you care that you see the point…

SUCCESS? Then keep going… we are almost there. You will need to quit Sample-PointViewer and then…

### OSCeleton

1.  Unpack the OSCeleton file download and drag into your OpenNI folder
2.  Navigate through to the folder to: Sensebloom…> bin> OSX> osceleton-osx
3.  Drag the **osceleton-osx** file onto your terminal
4.  The terminal should be running happy if you step back… Users will be added, calibrated and sending data (FYI, put your hands up to calibrate.. surprisingly, not many places say that…)
5.  The Calibrate position is called the “Psi” Pose… Arms in a “stick’em up” pose… like [this](http://1.bp.blogspot.com/_lHQV7pC9HHg/TQhSarqcqYI/AAAAAAAAAE0/jCF6pjGPVIM/s1600/SamplePlayersCalPose.png) or [this](http://www.superconductors.org/kitty.jpg) (be sure to watch the terminal for calibration… hold the pose and it will catch you. Also, be sure to stand far enough back… I am rather tall and had to step about 8 feet back…)

## **Lets leave that running and then…**

To test, we can use a pre-made Processing example… but its not needed, you can just skip to Max if you wish

1.  Download the [examples from Sensebloom](https://github.com/Sensebloom/OSCeleton-examples)
2.  [](https://github.com/Sensebloom/OSCeleton-examples)You will need [Processing](http://processing.org/download/) if you don’t have it (If you are new to processing you will also need to download: [oscP5](http://www.sojamo.de/libraries/oscP5/) and [pbox2d](http://code.google.com/p/pbox2d/)
3.  Open Processing
4.  Close Processing
5.  Move the Folders for oscP5 and pbox2d into the created libraries folder (should be in your Documents folder after running Processing the first time)
6.  Open the file Stickmanetic and press the Play icon
7.  Stand/Calibrate (stand about 6ft away)/ AND DANCE

[HAPPY HAPPY JOY JOY](http://video.yahoo.com/watch/2034814/v2165286)

**Now… getting the data into Max is easy…**

For Max you will need the [CNMAT objects](http://cnmat.berkeley.edu/downloads) (which if you don’t have, you really should anyway).

Download/unpack/move it into the Cycling ‘74 folder in Max

I assume if you went this far, you know your way around max a bit… so I will keep this short

Paste this into a new patcher:

<pre>----------begin_max5_patcher----------
2849.3oc0c00aiiaE84jeEDdeclL7aJl21tEEnEEn.s6Cscxf.Ga4DuQQJPV
Yyrcw9euhjx1bmXGRsV7COHiskLk7UGduGd4gTT+5kWL6tluVtYF3ZvmAWbw
ud4EWn2kZGWLr8EydZ9WWTMeitXypKes4teZ1GLeUW4W6z6tpY9x6lWe+1uX
8R8t6K5G4zs6bUScW87mJ0e022tdd01uo9kmVWWU1o+MPVEey5+mt3H7Uv8k
s4ktusvlc08KOWZtZlosFvWF95mm2s3g002eaa4hNSIHpSI3i5yLfCUuh6eE
7E0Q7aWdo5kO3Iprn4omJq6dCr7v75ka24yska5Ky7t0M01VtETwjgDpfGvP
rvCLUiDXl9MpXOfbbLjizEiWvTugXgAEKqtq40Q.ibbBgwsffAFYDefQJWWL
g4PCELt4glWpVV1NFjjjPjjIrARtW.Iw.jPdHAxQFUSooOpFYhm8LpFhzQ0B
XNEUSkoOpd.F8LplVncFIrLKplQSdT8VfzunZjFH4RTHAxtl1MMi.EIvzGVa
dkvymn55xEONFPjl9f5APTjOwzOTNeLMvPjIOddvcDlOgy+y02+P2H.QbwwA
QvepoZo+HI8OHRpgEDwfGX8VXhCrDRsCpKf6OnIDK+6kqFETJyCnDahRwXpO
PIoPpgRlIzVHBBTtpoYTPII8MxPLg3DjOA2rBtMJFnf640OVUNFXjk9lY1Bi
hwzQFbParF7Xc4nfQdxanY.E8rkFHwvNxypVZD4A8HgNlVZ9F5w.0RyXoGQY
PN3b7HnGEF4FovbhdDwyfrv4iIMbSJjBHKmnGyfzv4iHObRgIObdPyCej4Nl
IYgSoiJ0QA0Np9DScbUUSuEOlvWzTHEg7H3E1U3K5JR++nzd..oQM5PFzVf1
aFdl9Kx489E9LNMlfbt7Mm63fsnLAagvoGawL5U79+w3IDfw4A.yJBfyKtu+
46pAmD.9HC.6K0OOewi.3U69a1gvZZ.wZpS35Xe38PPTggakaTGAGa2SbB4V
4FuSBOPTqJ2+DRshQ4AzFBlUT+IM0LqXbVfuAgXsOa0c0eomWEe9wqZjYdhn
UOB301axkf1aeX8yfJ0qGD6XAD6HGC6Tfj9+dfQl2DQN7UTjI4EgfAKodlDl
BlQgLOfVpjE1b5SD9VjI8GkV.CaJ8SC9dJM8TfOWynmYlzaQOi9BR5bNwTSZ
KHRf3UoF8kSUbOMOf1fvqRwHMuZgHc3KKSv2PvqRDn8wFomWUb9kQuo27IiW
sHO5sYHnUGDJIUg8xr.YCBqpsNIIBdk4gBeAgT0RljzyoJwmopjLQTpuqJIU
2pFs492zCde+61SEBaPjjBPbmbI9IYBa.oP7HGJSyjNdBC2.gRKRhZxRVd.s
DYfGGzTgu7LAeEAdXPmF78jZGp3bUyDJKMiBpTlIc7LD7pCZljn399DfyCrM
HDq1hljL.FkI.bHXVsUMI8LqHH4bU1jTQshfz7n6mvvMASRVjOKKf1fvrZKb
RxvWddfuhvNASxAd0hyToSlHZUGSvDszIsCRmzdLoSPP4Yf1Izg64KjLtQyz
boCnPT.RSxLp.jgT8iLQIUjGPK1byYN0ZmH20PTpv2LYpRgEnPnchzRbFbha
IhAOC0NQZtcGYIIAeVtz8yPvqREhDxqxv4AzFDdUJluS5jTguYxTkJH7pDA2
RZljyqxNCENgmTd0LoymgfVEM.sIJrWjEHaPXUQPVpyVkkGSTpfPpxXVpxjZ
NUN7LjScBoTcLeS1txA1+Q8Zwn5VzwZkszFHQ4stIFPCZVYAIEQtymYxMHNR
xCltIXtHI8qOSt0vQEnvpaRpvWRlfubdX0MYZv2SosHJ6bU2D7vpZRryumjI
5lDDd0AcSRTbOISzMIH7p15ljJ7MSzMIH7p15ljddUxYqtIIiWMOzMIHzpC5
ljpv97P2jfvpZqaRpf27P2jfPpZoaRFjq54ptISDkpiIaxNcSZGzMo8X5ljl
kElQpaBFN7DBAE4YOVQdjjjLHCK5voCkj4kWlLa8EAYTQo6xtOQvKNSlv97f
Lnnz88dXRf2SogH7Y3MLJiZXSooY1jmIJ5ICxb3ilRR0L4VKMDjpXNYWx8oB
dY4xRXb.fWDYuT2ImTEc9sxlfjjjRplGqilxfLQSHojSMOV.XEAYdlfSNkZt
rxEG.4Rv6kiI4DpmgqTT3IjN8XO3G99kK68M1.5+86JaquFbyrO8SMqq6tY1
M0+X+UBna98p8tY8pUqT6by0f+lp..EH9AvhGJ6w99qbP2CkfUuTUApVuoCz
rBnOOa.2UV075U2Tu9ZvO1Wj+5eV8cpB+xlx198u5Zv+Frnooc4554ck6NRv
559+5speddE3yFMitB9E8A7eF6A7e87.5w2urEjpVWWtn4kZMRINvDtIJOIQ
NzCLogGnJZggLKHQH3ezGjEO0W8O+9x23Y7bSaGPX8TqvdxwMxqb7HBlN5yJ
buBVL2HqagmIkkYYOK5hx0+b4gDiMfrKmBfXd3GwBC2we4sA62TeSs54h4M0
pGwn2Tqebsp1Y6sKZppl2B9t5lNvqMsO1atfeory7kaUqU8YsbspO7Zq5b+1
Cvnjq58U86q7vmyp26Grx5GrZ6OX0Q+AqF9AqdueP8Bns4CpazQ0656zQsc1
zL76NTlpgxTssLUCk4fbODxAFmkDQ9vn1OHhrerPM8p3q7j.JGIvu6w9qs1S
4sz8FRIiz8xhPj6y+3e8Cez.VllsAepuf2pZY07oMOVVA9TUylN8NOTOMCHD
x7BB8CFMqA9XH4fvn930QMaLGzVTUe9T6+2isaZdocwVqQ2XdOENXeZuKK2z
oRVXHw8OuqcOqx7v5kKKqsiWdZ8xm07fli4HUz9ZRpU.I.xgIoVQphsMgcYS
I.mHtrIZbsIhGtSpkZwXaStp6TKotiwlPP5UHUenUKz5Ty8vIGdEaXqovjcE
BTLRXruunEaWtMGFH.IQawpsNUKF6SPKLtU7Xep3kw2lbEzpVshinMo88c5s
whuM4rtiFeaxYcGIt1jOwcEv3aStp6Dx3aStp6DwMtyG2IDN5ljqZNkv3Q1j
b4fihqCNG4QVN7DXStp5XijDGgI6xYfXdHRS3LUNC5slBS1UUKajvXw97xHC
2sc8cAkMr0oZwPer33xhnsImU7h3aStn1XwsKbZeem0cj3aSNq6vw2lbV2E2
1.X9D2QKhuM4ptiJhuM4ptiF43NOZqLt4wS8gIfRhuM4zaBGeaxo2TbYBn9v
DPJhuM4ptiHhuM4ptiDWl.ejZNtdSDeXBHj3aSN8lvw2lb5ME25N08uhaV7Q
1gmB1tdOfMq3oC8dPu0TXwNaJDFeTzo21n61HaW2FwXtU2F0acplrORdgiLL
5ijWHY7sIm5KE2lJwdDAHhtE4phCOR1V4dMHFl.aDtdjVzaMAFrS8vFIFxE6
hWQXw1a7N1vVmnAi7RAu3N7BHuD5jFeaxY7ZbSFo2g0mj1vzDXUNcoFa8WeT
PuKO2ba5OL1n5sNYy0mTUPXbjAQeZ5GgQIvpbOpHws4ciqjaGNbBrJ2CWCJA
VkyZvHOjM5GuBtmfBiLaHAdW6lzgYFng1Pu0jXxN4dgEI.Hc5zAIic9zv2ky
DkRrlOM5sNYitvqQQjGYnrvKnjk.qxY7KLxM4qcnbNa2jIvnb6VgRfU41sJx
Dv9Lw.GIoAEoHHjV2VH1ed3gsNQpmianIfP1mQ8GMkWBXodlERoZsSjxnbIL
1j4e+KAjYBfatDzaDiKgry09a6HkunJ0BUs9LePUMsuMeBDUyqqAnbJ8Lnla
aIy0fdiuYpse4uc4+Gbg7zFO
-----------end_max5_patcher-----------</pre>

Refer to the READ ME files for all of these for more info and settings.

Enjoy!

Please let me know if you do anything fun/educational/crazy with this.

I plan to post some examples shortly… been to busy getting it working to experiment yet, hahaha. I will update if you find something I missed.

cheers,

tohm

<small>This entry was posted on Wednesday, January 12th, 2011 at 6:37 pm and is filed under [blog](http://tohmjudson.com/?cat=11 "View all posts in blog"), [music](http://tohmjudson.com/?cat=12 "View all posts in music"), [performance](http://tohmjudson.com/?cat=13 "View all posts in performance"), [technology](http://tohmjudson.com/?cat=14 "View all posts in technology") and tagged with [OpenNI](http://tohmjudson.com/?tag=openni).</small>
<small>FILE ARCHIVED ON 11:31:13 Feb 9, 2011 AND RETRIEVED FROM THE INTERNET ARCHIVE ON 18:30:34 Oct 28, 2015.<small>