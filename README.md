# Permutu Showcase

This is a quick showcase of my diploma project. My goal was to implement Permutu strategy game ([permutu.pl](http://permutu.pl/)) as a web platform. Permutu was originally created by Bartosz Żółtak. My role was to only implement the rules as a computer program.

> **Source code must be kept private** due to copyright reasons and may be shared on demand for recruitment purposes only.

## Architecture

I decided to divide the platform into three backend microservices, and use two separate frontend modules.

For development purposes, I created a Docker ecosystem to easily host whole platform.

### Backend microservices

1. **Auth microservice**

   Written in Golang. Keeps all the authorization data in PostgreSQL database. Authorizes and authenticates users using JWT Tokens shared by httpOnly cookie.

2. **Gameplay microservice**

   Written in NodeJS + ExpressJS. Uses SocketIO to communicate with frontend. Implements all Permutu rules and manages a system of _rooms_, where players can take a part in the game. All the data is kept in Redis database.

   Players can create, join, leave a _room_. Rooms are separated from each other so players can take part in multiple games at a time. Logic of the game is completely separated from frontend. All the data about a current state game is shared by SocketIO.

3. **Userdata microservice**

   Written in NodeJS + ExpressJS. Keeps all data about users, especially history of their previous gameplays in a MongoDB database.

Basic concept of architecture is shown on image below:

![Architecture](https://github.com/mwvabes/permutu-showcase/blob/main/img/architecture.png?raw=true)

### Frontend modules

Both of them are written using NextJS with i18n. TailwindCSS takes responsibility for neat UI, which was designed all by myself.

1. **Auth frontend**

   The only module user sees when not logged in. UI lets user to create an account or sign in. After logging in, the user is redirected to Game Frontend.

2. **Game frontend**

   All of the action takes place here. The app is developed to show all currently created rooms, lets user to join them and take a part in the game. The platform implements a chat module in rooms and connects with all of the backend microservices, especially with a _gameplay microservice_ using SocketIO.

---

## A little bit of how the app looks like

![](https://github.com/mwvabes/permutu-showcase/blob/main/img/front-1.png?raw=true)

![](https://github.com/mwvabes/permutu-showcase/blob/main/img/front-2.png?raw=true)

![](https://github.com/mwvabes/permutu-showcase/blob/main/img/front-3.png?raw=true)

![](https://github.com/mwvabes/permutu-showcase/blob/main/img/front-4.png?raw=true)

![](https://github.com/mwvabes/permutu-showcase/blob/main/img/front-5.png?raw=true)

![](https://github.com/mwvabes/permutu-showcase/blob/main/img/front-6.png?raw=true)
