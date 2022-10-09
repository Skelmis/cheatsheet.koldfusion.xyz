Key Terms
^^^^^^^^^

A TL;DR page for y'all to use as a refresher during the day if you wish.

*Just my definitions n quick thoughts*

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


