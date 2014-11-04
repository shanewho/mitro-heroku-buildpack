mitro-heroku-buildpack
======================
A heroku buildpack for the Mitro password manager.

> **Note:** This is a work in progress

## Deploy to Heroku
[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy?template=https://github.com/shanewho/mitro/tree/heroku-button)

> This button currently uses a my experimental fork, not the official Mitro repo, it needs an app.json for it to work with the Heroku button.

## Do it manually

```
git clone https://github.com/mitro-co/mitro.git
heroku create
heroku addons add heroku-postgresql:hobby-dev
heroku config:set RANDOM_KEY=$(openssl rand -base64 256)
heroku config:set BUILDPACK_URL=https://github.com/shanewho/mitro-heroku-buildpack.git
```

## Configuring the client
Once your server is sucessfully installed, you will have an app similar to `https://mighty-mountain-8942.herokuapp.com/`. If you visit that url you should get a 404 page with a message at the bottom that says 'Powered by Jetty://'. That means it is working correctly (ignore the 404).

To set the custom server url, you need to visit the preferences page. This url may contain random text, so the easiest way to find it is to click the _Sign Up_ button (in the extension), then change the url from `signup.html` to `preferences.html`. 

> **Hint:** Chrome's url would look something like this: 
>
> chrome-extension://jcfojsudcibamjjsubmksclfffpdisuj/html/preferences.html

Put your Heroku hostname in the Server hostname field (**Don't put the https:// or trailing slash**). It should look like this: 

`mighty-mountain-8942.herokuapp.com`

You are all set, sign up with a new account and you are ready to go.

> #Just kidding, the mailer still needs to be set up for this to work for real... working on that....

## For the paranoid

- I am not a security professional, I do not know all the security risks involved in this setup
- This uses Heroku's free SSL (https://yourapp.heroku.com). You will have a secure connection between your browser and Heroku's servers. The link between Heroku's server (their HTTP router) and the Mitro server is not secure unless you setup *real* SSL with your own certs (i.e., costs money).
- The key used for signing things is based on the RANDOM_KEY value set on your app's config (it is an SHA-1 hash of that key). Make sure RANDOM_KEY is set to something random and unique. Make sure nobody gets access to this value.


## For the extra paranoid

- The buildpack downloads Ant from archive.apache.org and Java from Amazon S3 (the same binaries as Heroku's official Java buildpack)
- The buildpack includes a pre-built *unzip* not included in Heroku's base image
