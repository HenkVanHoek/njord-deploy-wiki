# Welcome to the PiSelfhosting wiki!

As the name of this project suggests, it's purpose is to make the installation of all kind of services as easy as possible. 

This project was started as a simple idea to have an easy method for installing Home Assistent, Frigate and MQTT. Altough I got it working with some a seperate config program which was capable of detecting newly connected camara's. I thought the principle of a generic docker compose template for each service assisted with a configuration app for each service was born and resulted in thinking about how to get this going. PiSelfhosting concept was born.

Currently we are working on the Alpha version.
It is the phase which is defined to have an operational version working with at least 3 services.
## Dashy Service
## Portainer Service
## Traefik Service

We discovered during this development some issues which resulted in a rewrite for some parts of the code. 1 step back to get at least 2 steps forward principle.
Main reason was the problem for supporting the different environments like MacOS, Windows and Linux and the problem with developing on Windows WSL. Bad mistake. Especially for the networking detection part. 
