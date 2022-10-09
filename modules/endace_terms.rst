Key Terms
^^^^^^^^^

A TL;DR page for y'all to use as a refresher during the day if you wish.

*Just my definitions n quick thoughts*

**Notes**

* Its better to say "I'm sorry, I don't understand what your asking about" versus trying to umm and ahh your way through it I think
* Your interviewers are nice people, don't be scared. Remember, its just a conversation
* You don't have to get everything right, its an internship. You are there to learn. They care more about your problem solving skills and how you talk/work through the problems they ask rather then simply being able to answer niche questions
* Bathrooms are in the stairs, you will need a key card to get back onto the floor. If you get stuck, go back down the ground floor and go back up the elevator to the 6th floor because that route doesn't require a keycard
* Everyone at the company is really nice, if you get lost or anything you can literally ask anyone and they will help you
* If everything is overwhelming and you just need some space, I recommend going to level 4 and going out onto the car park/roof area. Its a nice view, fresh air and away from people. Just tell Kat before you pop out and she will be **more then accommodating**
* I don't care if you name drop me or discuss me with colleagues if it comes up
* If you get lost or anything happens feel free to call me. I am doing nothing all day and can make sure you make it back to everyone else either myself or by getting in contact with people at work whose number I have
* If your locked out, go near reception and just use the door bell and someone will eventually come and then ask them to get you back to the other applicants


Both
====

Terms
-----

* Client: A consumer, for example you
* Server: A producer, for example the code that serves ``elearn.waikato.ac.nz``
* Swagger / Open API: The industry standard for documenting API's in a simplistic way for both client and server developers
* Python: An interpreted language with numerous use cases
* Web frameworks: Software packages to facilitate easier creation of webservers, key Python ones are ``Flask``, ``Django`` and ``FastAPI``
* APIS: Application programming interface, a structured way for one program to offer data and its services to end clients in a programmatic way. Think of an API like the waiters in a restaurant, they liase between the kitchen and the tables
* Proxy / Reverse Proxy: Used to route incoming web requests to the correct application on the server which should handle them. I.e. used to run multiple websites on a single server / IP address. Key examples are ``Nginx`` and ``Apache``
* Docker: Simple containerization which simplifies deployment processes by making re-usable containers for any given software
* HTTP Status codes:
    - Status codes are a simple, standard way to tell the result of a request without fuss
    - 100-199: Information, just keep on trackin
    - 200-299: Success, your request worked fine
    - 300-399: Redirect, your request looks valid but you made it to the wrong url / the resource has moved to some place else
    - 400-499: You fucked up, your request is invalid, you lack permissions to do this action, the request resource doesnt exist, etc
    - 500-599: The server fucked up, your request was probably fine but the server threw an error somewhere and died during the processing of it

Questions
---------

* What is the difference between HTML and HTTP?
    HTML is a markup language for displaying content to end users while HTTP is a transport protocol used to state how data should be transferred between computers over a network.


Endace Terms
------------

* Probe: Endace's core product. This is a physical device you slot into your datacenter racks. It essentially sits on the edge of your business network and records packets for usage in investigations later on

Product Types
*************

* Probe: This is the device which does the actual packet capture
* Investigation Manager: This device essentially aggregates the data from multiple probes at once for usage in whatever you want
* CMS: Connect probes and issue commands to as many or few devices you want at once. Essentially just a form of centralized control

Hannah
======

Traffic Relay in VM's


If you talk to Andreas (Mohawk man, currently has dyed hair) and your comfortable, totally bring up the fact you talked to him at the NZCSC. It will reinforce the belief in you as well as reinforce the idea that your truly interested in things because you follow up on them and it was a positive prior interaction. Note if he doesn't remember immediately just say you were with the woman with Ethan and you were asking for his opinions on career growth and just general advice.

Terms
-----

* HTTP: Non encrypted connections
* HTTPS: Encrypted connections using TLS
* TLS: Transport layer security, designed to provide secure communication over networks
* DNS: Domain name system, used to map domains ``google.com`` to the IP address the request should actually go as such as ``158.69.161.70``
* Wireshark: A program used to view and interact with saved network captures

Questions
---------

* What is a vm?
    A virtualized machine often ran by a company such as a AWS or Google cloud where you don't own the hardware but basically just rent it out.
* Why do you think we want this?
    - Cloud is where the software world is trending towards
    - Cloud based deployments offer quicker turn around times compared to needing physical hardware
    - Smaller footprint as well, adding onto the above point
* What is a file format used for storing packet data?
    ``pcap``, you should google it



Chris
=====

Load testing | Power management

Terms
-----

* Manual testing: Literally that, no automation and just testing things by hand
* Automation testing: Writing reusable tests you run with a programming language
* ROBOT: A markup like language for writing automated tests. I'd recommend googling it
* Regression testing: Tests written to test that new software changes don't break old features/things

Questions
---------

* Why do we want want to test things?
    I mean, you can answer this one.
* Why do we want automated tests?
    Manual testing takes significantly more time and is prone to human error. Automated tests are the same every time they are run, can be done in parallel, etc
* Why do we want power management?
    - Saves costs for machines not in use
    - Makes the machine last longer because its not in usage 24/7 being worn down
* Why do we want load testing?
    Software behaves differently under various loads, so its useful to test in all scenarios as it better mirrors how the end client uses the product

