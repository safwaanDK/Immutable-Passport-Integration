## Immutable Passport Integration Guide (README.md)

---

### 1. **Creating a Simple Application**

To start, you can either create a new application or clone a simple application from a repository. For this guide, we'll create a basic Node.js application.

```bash
mkdir passport-integration
cd passport-integration
npm init -y
```

### 2. **Registering the Application on Immutable Developer Hub**

- Visit the Immutable Developer Hub.
- Create a new project and set up a testnet environment.
- Navigate to the Passport config screen.
- Create a passport client for your environment.
- Note down the `Client ID` and `Client Secret`.

### 3. **Installing and Initialising the Passport Client**

Install the Immutable SDK:

```bash
npm install -D @imtbl/sdk
```

Initialise the Passport client in your application:

```javascript
const { config, passport } = require('@imtbl/sdk');

const passportInstance = new passport.Passport({
  baseConfig: new config.ImmutableConfiguration({
    environment: config.Environment.PRODUCTION,
  }),
  clientId: '<YOUR_CLIENT_ID>',
  redirectUri: 'https://example.com/callback',
  logoutRedirectUri: 'https://example.com/logout',
  audience: 'platform_api',
  scope: 'openid offline_access email transact'
});
```

### 4. **Logging in a User with Passport**

To log in a user:

```javascript
passportInstance.login();
```

### 5. **Displaying Tokens and User's Nickname**

After successful authentication, display the tokens:

```javascript
const idToken = await passportInstance.getIdToken();
const accessToken = await passportInstance.getAccessToken();
const userNickname = await passportInstance.getUserNickname();

console.log(`ID Token: ${idToken}`);
console.log(`Access Token: ${accessToken}`);
console.log(`User Nickname: ${userNickname}`);
```

### 6. **Logging out a User**

To log out a user:

```javascript
passportInstance.logout();
```

### 7. **Initiate a Transaction from Passport**

To initiate a transaction:

```javascript
const transaction = await passportInstance.sendTransaction({
  to: '<RECIPIENT_ADDRESS>',
  value: '0x0', // Placeholder string
  data: '0x0'  // Placeholder string
});

console.log(`Transaction Hash: ${transaction.hash}`);
```

---



This guide provides a comprehensive overview of integrating Immutable Passport into an application. Always refer to the official Immutable documentation for more details and updates.
