#Core Web App Quickstart

##Features
- [AspNetCore 1.0](https://docs.asp.net/en/latest/)
    - https Kestrel (uncomment Code for https)
- Thinktecture IdentityServer4
    - [AspNetIdentity](https://github.com/IdentityServer/IdentityServer4.AspNetIdentity)
    - [EntityFrameworkStorage](https://github.com/IdentityServer/IdentityServer4.Samples/tree/dev/Quickstarts/8_EntityFrameworkStorage)
    - Social Logins (Google, Twitter)
- [Swagger](http://swagger.io/)
	- Swagger is a simple yet powerful representation of your RESTful API 
    - IdentityServer OAuth Integration
- Unit Tests based on [XUnit](https://xunit.github.io/docs/getting-started-dotnet-core.html)

##Test Drive

![Console](https://github.com/ChrisRichner/CoreWebApp.Quickstart/blob/master/readme/console.PNG?raw=true "Console")

- Open CoreWebApp.Quickstart.sln
- Set CoreWebApp as the startup project
- Choose CoreWebApp (Kestrel) as your debug configuration. Alternatively you can still use IIS Express for debugging
- Hit F5 to build and start debugging
- The console window starts and kestrel serves the API and STS at http://localhost:5000

##Login
![Spa](https://github.com/ChrisRichner/CoreWebApp.Quickstart/blob/master/readme/spa.PNG?raw=true "Spa")

- Start your favorite browser and open http://localhost:5000
- Click the *Login With Profile and Access Token* button
- After the STS MVC Site has loaded click *Register*
- Provide a valid email (must not exist, but be valid foramtted) and a complex password
- Click *Register* button
- Now you're back on the index.html page, still not logged in
- Click the *Login With Profile and Access Token* button again
- Click *Yes, Allow" on the consent page
- You're back at the index.html page, this time you've got a valid ID and Access Token
- Click *Call Service* button to call the *IdentityController*
- Check out the *Ajax Result*
- Congrats, you've called the protected API with an Access Token provided by the STS

##Security Token Service (STS)
- Open http://localhost:5000/.well-known/openid-configuration
- Check out the sts configuraton

##Postman
![Postman](https://github.com/ChrisRichner/CoreWebApp.Quickstart/blob/master/readme/postman.PNG?raw=true "Postman")
- Start [Postman](https://www.getpostman.com/)
- Add a new request Tab
- Set the request url to *GET* http://localhost:5000/api/v1/Identity
- Switch to Authorization Child Tab
- Choose *OAuth 2.0* as the value for *Type*
- Click the orange button *Get New Access Token*
- Fill in 
 - Token Name: Code
 - Auth Url: http://localhost:5000/connect/authorize
 - Access Token Url: http://localhost:5000/connect/token
 - Client ID: Postman
 - Client Secret: secret
 - Scope: api1
 - Grant Type: Authorization Code
- Click orange button *Request Token*
- STS Login Page pops up
- Enter your login credentials
- Click *Login* button
- Select the new Token in the *Existing Tokens* list
- Set *Add token to* value to *Header*
- Click the orange *Use Token* button
- Congrats, you've called the protected API with an Access Token provided by the STS from Postman

##Swagger
![Swagger](https://github.com/ChrisRichner/CoreWebApp.Quickstart/blob/master/readme/swagger.PNG?raw=true "Swagger")
- Open http://localhost:5000/swagger/ui
- Open *Identity*
- Open the *GET /api/v1/Identity* action
- Click *Try it out!* Button
- You get a 401 response code because you can't call a protected API without an Access Token
- Click *Authorize* button in the top banner next to *Explore* button
- Choose *api1* and click *Authorize*
- The implicit flow takes you to the STS Login Page, in case you're already signed in the redirect happens very fast
- Click *Try it out!* Button again
- This time you get a 200 response code. The response body shows the result returned from the protected API 
- Congrats, you've called the protected API from the Swagger UI Page with an Access Token provided by the STS
