---
layout: post
title: Handling Incoming Push Notifications in AWS Amplify
date: 2020-01-28
description: "AWS Amplify provides two push notification configuration functions to configure how push notifications are handled by your app: onNotification, and onNotificationOpened."
redirect: https://medium.com/@dantasfiles/understanding-the-android-push-notification-configuration-functions-in-aws-amplify-ab97d71e048c
tags: amazon-web-services android
---

AWS Amplify provides two push notification configuration functions to configure how push notifications are handled by your app: onNotification, and onNotificationOpened

This post explores the details of when the handler functions passed to those two configuration functions will be called when an Android push notification is received by your AWS Amplify React Native app. The behavior will be different depending on whether the app is in the foreground, background, or closed, and whether the user clicks the push notification or just opens the app.

