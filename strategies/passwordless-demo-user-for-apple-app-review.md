---
description: >-
  How to pass the Apple Store review process if your app uses passwordless
  login.
---

# Passwordless demo user for Apple App Review

When you try to publish a mobile app on the Apple AppStore, there will be an [App Review process](https://developer.apple.com/app-store/review/). You need provide a demo user account for the reviewers to access the features of the app.

However passwordless login via email/phone OTP cannot be used in the review because the reviewer do not have access to the email inbox or phone number of that demo account.

You can create a demo account with email/phone and password by turning password on temporarily. In the project portal:

1. Go to "**Authentication > Authenticators**" and turn on "**Password**"
2. In "**User Management**", press "**Add User**" in the command bar.
3. **Create the demo user** by inputing the email address and password
4. Go to "**Authentication > Authenticators**" and turn off "**Password**"
5. Now you can login as the demo user in your app with the email and password
6. Submit your app for review with the credentials.
