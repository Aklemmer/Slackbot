# slackbox
Spotify playlist collaboration through Slack. Brought to you by the lovely people at [Benchmark](http://benchmark.co.uk).

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

Simply create a Slash Command, such as `/jukebox`, which accepts a track name (also the artist too for a less fuzzy search) to add to a pre-defined Spotify playlist:

    /jukebox Bell Biv DeVoe – Poison

##Installation

###Slack

####Slash Command

Slash commands allow for private functions within Slack which will **not** show up in chat history.

First you'll want to create your Slack Slash Command, which you can do by going to your [Slash Commands page](https://my.slack.com/services/new/slash-commands).

####Outgoing WebHook

Outgoing webhooks allow data to be exported from Slack channels. Using an outgoing webhook means song additions will be public so users will know when songs are requested and who requested them.

First you'll want to create your Outgoing Webhook, which you can do by going to your [Outgoing WebHooks page](https://my.slack.com/services/new/outgoing-webhook).

Outgoing WebHooks work best with a trigger word. This way only messages with the trigger word (or words) will be parsed and added.

**NOTE:** You may only use slash commands _or_ outgoing webhooks. The Slack Token environment variable can only be set once so it needs to be the token from this or the slash command.

####Common

During setup, have your slash command or outgoing webhook submit a POST to your app's `/store` endpoint, e.g. `https://app-name.herokuapp.com/store`.

Make a note of the `token` (either from the slash command or outgoing webhook), as you'll need it later to help guard against cross-site request forgery.

###Spotify

Head over to [Spotify's Developer Site](http://developer.spotify.com) and create a new Application. Make sure you add whatever slackbox's callback URI as a valid callback URI. If you're running locally, this will be `http://localhost:5000/callback` or on Heroku `https://app-name.herokuapp.com/callback`

Make a note of the `key`, `secret` and `callback URI` too, as you'll need these later as well.

Also, don't forget to make a playlist. If you do this through [Spotify's web interface](http://play.spotify.com) then the `playlist identifier` will be the last segment of the URI - make a note of this too! If there's a better way of finding this out, we're all ears. If you do this through the app, right-click the playlist to get it's web URL and again, you need the last segment of the URI.

###Environment variables

Once you've cloned slackbox or hit the "Deploy with Heroku" button you'll need to setup the following environment variables. These can either be stored in a `.env` or set up as config variables in Heroku.

* `SLACK_TOKEN` - The token from Slack's Slash Command.
* `SLACK_OUTGOING` - True if using [Slack Outgoing WebHooks](https://my.slack.com/services/new/outgoing-webhook), false if using [Slack Slash Commands](https://my.slack.com/services/new/slash-commands)
* `SPOTIFY_KEY` - Your Spotify application key (a.k.a Client ID).
* `SPOTIFY_SECRET` - Your Spotify application secret (a.k.a Client Secret).
* `SPOTIFY_USERNAME` - Your Spotify username.
* `SPOTIFY_PLAYLIST_ID` - Your playlist identifier.
* `SPOTIFY_REDIRECT_URI` - URI to redirect to once your user has allowed the application's permissions.

###Authentication

Visit your slackbox's home page to authenticate yourself with Spotify and you should be all set!
