---
title: 'Budgeting App'
date: 2024-06-042T15:52:04+01:00
draft: false
# math: true
# katex: true
---

[Github 🔗](https://github.com/jwhogg/Rails-Burndown-Budgeting-App)

On ongoing project of mine, taking inspriation from Monzo's budgeting burndown feature. I'm building this web app with Ruby-on-Rails, and using the GoCardless API to handle linking user's bank accounts to the app securely.

<img src="/images/monzo_burndown.png" alt="The inspiration for the project: monzo's 'targets' tab." width="60%">

So far, I am building the MVP, and have implemented functionality to link a bank account with the app, and to store the user's key to access their bank account data using server-side sessions, which are much more secure than cookies sesion storage.

<img src="/images/linkingaccounts.gif" alt="Process of linking bank accounts" width="80%">
The process of linking a bank account
