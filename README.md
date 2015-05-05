# SeetiTel 
*seeti: Hindi; "whistle"*

<hr />
Jack Kingsman *Core, Web, API*

Alex Choulos *Android*

Manny Amirtharaj *iOS*

All code is MIT licensed and [released on GitHub](https://github.com/SeetiTel/ "SeetiTel on GitHub").

<hr />
## Overview

SeetiTel is a multiplatform system for workers in developing nations to submit leaks and act as whistleblowers. SeetiTel allows for SMS, MMS, and voice telephony-based submissions of leaks and "whistles" - a unit of information that should be publicized securely and anonymously. This allows individuals in developing nations (where secure internet and the technical skills to anonymously use it may be lacking) to move information through existing infrastructure such as pay phones and cheap "burner" phones. There is also a native Android application, web interface, and an iOS prototype.

## Background

### Strength in Distribution
SeetiTel is built with openness and resilience through distribution in mind. The SeetiTel Core is the repository for all information in the system and can utilize `rqlite` to replicate data, allowing for a cloud of backend instances. 

The backend is accessed through an open source, well documented API, allowing native and web clients to be entirely abstracted from the Core server. This allows for any number of clients to distribute the load to any available backend instance - and the MIT licensed API allows for further client development above and beyond what we've provided.

SeetiTel Core is reached through Twilio phone numbers, which allows for one-click provisioning of new (and international, if desired) phone numbers. Simply point the Twilio number at a SeetiTel Core instance, and the number will respond to whistles sent via SMS, MMS, and voice calls - a four click process.

This modularity allows for hot swapping capability - front ends, Cores, and Twilio numbers can by dynamically scaled for a distributed and resilient application, even in the face of potentially hostile parties.
![](http://i.imgur.com/TvnKGPi.png)

### Stack
SeetiTel Core is built with node.js, using Express for http handling and a hand-written API. SeetiTel Web is build with Bootstrap and jQuery. The Android client is built adhereing to the Google Material Design standards and utilizes the `RecyclerView` and `CardView` support libraries. The Core development server is a standard VPS, with no remarkable features other than a node installation.

## Screenshots

### SeetiTel Web
![](http://i.imgur.com/w9CVvoa.png)
<hr />
![](http://i.imgur.com/iHwQbXT.png)
<hr /><hr />
### SeetiTel Android
![](http://i.imgur.com/A8tlP0T.png)
<hr />
![](http://i.imgur.com/9BHDmdB.png)
