# OSO Documentation

Contains the documentation and wiki of the oso project.
Every repository in the organization will link to oso-docs as it contains the [CONTRIBUTING.md](CONTRIBUTING.md) and the [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).

## Supported devices
The currently supported devices are listed below
* [Smartphone (Android/iOS)](#smartphone-androidios)
* [Flic Button](#flic-button)
* [ReachFar Tracker RF-V18](#reachfar-tracker-rf-v18)
* [NanoTracker](#nanotracker)

We aim to incorporate more devices as the development goes further.
If you have an idea on which device we should look into next, just write us.
If the requested device fits, we try to get our hands on it so we can make it work with the backend.

## Configuration
Every device has its own way to send data, it may use TCP with its own protocol or HTTP.
It may be that several configuration steps have to be done before a device can communicate with this backend. 

### Smartphone (Android/iOS)
We provide an app written in React Native so you are able to send emergencies with your Smartphone.

### Flic Button
The Flic Button works in conjunction with the Smartphone over Bluetooth.

We provide a seamless integration of the Flic Button in our Smartphone app. Thus the same app can be used.<br> 
By clicking on the Button for instance an emergency is automatically sent to the backend.

>For more information about the Flic Button visit<br>
https://flic.io/ 

### ReachFar Tracker RF-V18
To be able to use the Reachfar Tracker it needs a sim card to make and receive phone calls.
Mobile data needs to be enabled in order to send out emergencies.

Afterwards the Tracker only needs to know how to connect to our server. This will be done via SMS-configuration.<br>
All configration-SMS have the format <Param>,<Param>,...#. It is mandatory to use only lower-case letters and to not add any whitespace or other character whatsoever. A message is only valid, if the Tracker sends a confirmation-SMS back. This can take up to 5 Minutes. If no confirmation is received the SMS was invalid and ignored.
   
First a master needs to be assigned via the message<br>
``<password>,sos1#``

where the &lt;password&gt; is the devices password (by default '123456')<br>
and the number from which the message has been sent will be configured to be the master number. This is the only message that can be sent by any number - all further configurations need to be sent by this master number.

Afterwards the server will be announced to the Tracker via<br>
``surl,<url>,port,<port>#``

where &lt;url&gt; is the url to the server<br>
and &lt;port&gt; is the port to connect to

The protocol for configuring a Reachfar Tracker with our provided Server/System would be
```
--> Tracker: 123456,sos1#
<-- Tracker: <number> has been set for master number successfully.
--> Tracker: surl,app.ososystem.de,port,9999#
<-- Tracker: surl:app.ososystem.de;port:9999.;OK!
```

For more information about the ReachFar Tracker or the SMS-configuration visit<br>
http://www.reachfargps.com/products/RF-V18.html<br>
https://www.my-gps.org/145-Reachfar-RFV16-SMS-configuration-Manual<br>
https://www.my-gps.org/146-Reachfar-RFV16-SMS-configuration

### NanoTracker
>Documentation is following soon.

For more information about the NanoTracker visit<br>
https://www.roundsolutions.com/de/10630-nanotracker-world-s-smallest-gps-und-gprs-tracking-device

---

## Roadmap
We try to build a platform where people in need have a tool to communicate effortlessly about needing help. This kind of task is not trivial to implement if we want to maintain a quality of standard. There are many things to consider.

* We have to ensure that we will have a resilient infrastructure which is able to handle failures
* We have to ensure that the exchange of messages is reliable and as fast as possible
* We want to provide an open interface and not setting a limit e.g. on supporting certain devices

And many more :raised_hands:

Granted that we are not that many people so far and most of us are contributing to this in our freetime (when not working) we still have a goal with the OSO project in mind. And the more help we can get, the better it is going to be.

### Currently development goals
* Decomposition of the backend monolith to a microservices architecture (by the principles of DDD)
* Providing a versioned infrastructure which includes a whole environment for the OSO project and can be hosted by anyone
* Publishing a writeup of our open source journey describing how we approached so far

### OSO is not the only one
As we recently noticed there are some projects which show similarities to ours.
Here are two for example
* https://www.vivatar.com/
* https://wayguard.de/

This is by far no deal breaker. It only shows clearly that there is a need for projects in this domain. :couple_with_heart:

As we are handling senstive data we want to provide total transparency which is only possible with an open source approach.

### Future development goals
Here is a quick writeup outlining our future goals
* We want to host the OSO project as a service which can be used by everyone (free of course)
* Providing smartphone apps for help-providers and help-requesters (for Android and iOS)
* Supporting more devices
