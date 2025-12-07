---
title: 'Radial Chess'
date: "2024-12-01"
draft: false
# math: true
# katex: true
---

- [Github- Back end 🔗](https://github.com/jwhogg/Radial-Chess-Backend)
- [Github- Front end 🔗](https://github.com/jwhogg/Radial-Chess-Frontend)

<img width="60%" alt="Screenshot 2024-10-25 at 14 31 29" src="https://github.com/user-attachments/assets/eeb29645-a658-4d88-ac06-09dfc15afd10">

## Demo
<img width="60%" alt="Demo of a game" src="https://github.com/user-attachments/assets/65dc3ed1-da70-4d31-a273-349de6703df2">

Inspired by the [heorics](https://www.youtube.com/watch?v=7VSVfQcaxFY) of lichess.org's single developer, I decided to try to create a similar web-based online chess app, with matchmaking. The main goal of this project is to use my knowledge of system design to make a robust and scalable app that could theoretically handle a large number of users. This involves knowlege of infastructure tools, and overcoming dificulties such as scaling a Web-Socket app (hint: you will need sticky sessions for your load-balancer!).

Another goal of this project was to put to use my Rust knowledge, I'd been learning in my spare time and wanted to try and integrate what I knew into something practical.


## Back-end Technologies
- [Rust 🦀](https://www.rust-lang.org/) for the entire back-end
- [tokio](https://tokio.rs/) and [axum](https://github.com/tokio-rs/axum) for async and networking
- [Redis](https://redis.io/) for scalable state memory
- [JSON Web Token](https://jwt.io/introduction) for secure authentication
- [MySQL](https://www.mysql.com/) for storing persistent user data

## Front-end Technologies
- [VueJs](https://vuejs.org/) for front-end + WebSocket client
- [Vue-axios](https://www.npmjs.com/package/vue-axios) for API consumption
- [Auth0](https://auth0.com/) for secure authentication and Single Sign-On (Google accounts)
- [Vue3-Chessboard](https://github.com/qwerty084/vue3-chessboard) for chess GUI, built on Lichess

## Architecture
*Note: The project is yet to be hosted as it is under development, but these will be the technologies used:*
- [CloudFront](https://aws.amazon.com/cloudfront/) for serving the static site
- [AWS EC2](https://aws.amazon.com/ec2/) for hosting the back-end servers
- [Docker](https://www.docker.com/) for containerization
- [NGINX](https://www.f5.com/go/product/welcome-to-nginx) for load balancing
- [Redis](https://redis.io/) for state management and pub/sub


*Note- this project has since been shelved as I've had other responsibilities, but I learnt a lot and was glad to be able to deliver a working prototype.*