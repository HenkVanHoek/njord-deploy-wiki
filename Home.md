# Welcome to the PiSelfhosting wiki!

As the name of this project suggests, it's purpose is to make the installation of all kind of services as easy as possible. 

This project was started as a simple idea to have an easy method for installing Home Assistent, Frigate and MQTT. Altough I got it working with some a seperate config program which was capable of detecting newly connected camara's. I thought the principle of a generic docker compose template for each service assisted with a configuration app for each service was born and resulted in thinking about how to get this going. PiSelfhosting concept was born.

Currently we are working on the Alpha version.
It is the phase which is defined to have an operational version working with at least 3 services.
## Homarr (Replaced Dashy)
## Portainer Service
## Pi-hole
## Traefik Service is planned as the next service
And meanwhile there is an editor which is a web ui for the metadata, the parameters and docker compose templates for the services. It's purpose is to check for port usage as it is not possible to have 2 services using one port. 

We discovered during this development some issues which resulted in a rewrite for some parts of the code. 1 step back to get at least 2 steps forward principle.

The development method is a kind of agile style development with emphasis on Test Driven Development. Also use is made of pre commit checks for linter, black and flake up to security checks with bandit.
Main reason was the problem for supporting the different environments like MacOS, Windows and Linux and the problem with developing on Windows WSL. Bad mistake. Especially for the networking detection part. 

## Configuration Data Editor
Some screenshots from the editor:
<img width="945" height="678" alt="image" src="https://github.com/user-attachments/assets/dfb514f7-6f54-4478-9965-4568ec9160a9" />
<img width="945" height="676" alt="image" src="https://github.com/user-attachments/assets/6aa53402-9733-4f42-9798-051e78da97b9" />
<img width="945" height="672" alt="image" src="https://github.com/user-attachments/assets/63cb9a8d-6fab-4181-af91-368f67c5b974" />



