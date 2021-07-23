# twitch-oauth-passport

Passport strategy for Tiwtch OAuth

## Installation

Install the package via npm: `npm install twitch-oauth-passport`

## Usage

#### Requirements

To use this module, you will need a [Twitch Developer Account](https://dev.twitch.tv) . Then create an application and retrieve/fill out the following: clientID, clientSecret, and redirect URIs (enter your redirect URIs).

#### Configuration

Initialize the strategy as follows:

```js
const TwitchStrategy = require('twitch-oauth-passport').Strategy;
passport.use(new TwitchStrategy({
    clientID: "<client id>",
    clientSecret: "<client secret>",
    callbackURL: "<callback url>"
}, function(accessToken, refreshToken, profile, done) {
    User.findOrCreate({ twitchId: profile.data.id }, function(err, user) {
        return done(err, user);
}}));
```

#### Authenticate Requests

Use `passport.authenticate()` to authunicate the requests.

For example, you could implement it with [Express](http://expressjs.com/) like this:

```js
app.get("/login", passport.authenticate("twitch"));

app.get(
  "/callback",
  passport.authenticate("twitch", { failureRedirect: "/login" }),
  function (req, res) {
    res.redirect("/"); //redirect on successful authentication
  }
);
```

## Disclaimer

This repository is NOT developed or endorsed by Twitch. This library is here to help users easily integrate Twitch's OAuth API to their Node.js projects. All questions about the API should be taken to [Twitch Support](https://help.twitch.tv/s/?language=en_US) and all questions about this library should be taken to [milanmdev](mailto:milanmdev@gmail.com).
