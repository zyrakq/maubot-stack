# Maubot Plugin Setup Guide

This guide covers the common setup steps required for configuring maubot plugins with Conduit homeserver.

## Prerequisites

- Running Conduit homeserver
- Admin access to Conduit
- Maubot instance configured and running

## Setup Steps

### 1. Create Bot User

Create a new user for the bot in the admin room using Conduit admin commands:

```mxc
@conduit:server_name create-user <username> <password>
```

Example:

```mxc
@conduit:matrix.ax create-user rss-bot secure_password_123
```

### 2. Get Access Token and Device ID

Use the provided HTTP request template to obtain access token and device ID:

1. Update the `.env` file with your bot credentials:

   ```env
   MATRIX_HOST=https://your-homeserver.com
   MATRIX_BOT_USERNAME=@bot-username:your-homeserver.com
   MATRIX_BOT_PASSWORD=bot_password
   ```

2. Execute the request in `access-token.http`:

   ```http
   POST {{$dotenv MATRIX_HOST}}/_matrix/client/r0/login  HTTP/1.1
   Content-Type: application/json
   
   {
     "type": "m.login.password",
     "user": "{{$dotenv MATRIX_BOT_USERNAME}}", 
     "password": "{{$dotenv MATRIX_BOT_PASSWORD}}"
   }
   ```

3. Save the `access_token` and `device_id` from the response for maubot configuration.

### 3. Add Bot to Target Room

1. Invite the bot user to the room where it should operate
2. Ensure the bot user accepts the invitation and joins the room
3. Grant appropriate permissions to the bot user in the room

### 4. Configure Bot in Maubot

1. Access the maubot web interface
2. Create a new client with the obtained access token and device ID
3. Upload and configure the desired plugin
4. Create a bot instance linking the client and plugin

## Next Steps

After completing these common setup steps, refer to the specific plugin documentation for plugin-specific configuration commands and usage instructions.
