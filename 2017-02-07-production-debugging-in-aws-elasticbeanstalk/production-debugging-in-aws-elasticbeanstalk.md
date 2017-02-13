# Production Debugging in AWS ElasticBeanstalk

Mark Campbell
Team Lead at SERMO

---

# Talk Goals

* Touch on some AWS technologies
* Operation of a system versus development
* Touch on web and rails debugging

---

# AWS ElasticBeanstalk Architecture

![inline 240%](aeb-architecture2.png)

^ 1 box = one rails server

^ Like Heroku. Show of hands?

^ Way less expensive

^ DB is AWS RDS

---

# Application Design

* Two Ruby on Rails apps (hosted with EB)
* JSON API secured by HTTPS and HTTP basic authentication
  * We'll talk about this later

---

# 'Simple' problem

Smoke testing the app before releasing it to users resulted in a lot of smoke.

---

# Lit AF is somehow not good

![inline](app-on-fire.png)

---

# Symptoms

Log in. Go to projects. User see '500' page:

![inline](500.png)

---

# Request flow

Mental model is critical for debugging!

![inline](request-flow.png)

^ Make sure that everyone understands what's going on before moving on.

---

# Common Tools

* SSH for logging in
* Rails and nginx logs for history
* Rails console to interact with the app
* curl to easily replay requests

^ Critical tools are listed above, learn them well.

---


# Debugging

* Recreating the error
* Exception tracker
* Logs

^ Don't talk about exception tracker and logs in detail

---

# Exception tracker

Caveat: some classes of exceptions are completely ignored.

Exception tracker clients (`gem sentry-raven`) have default lists.

---

# Logs

Caveat: logs don't have all data you could want.

Rule: logs will always lack the specific data you need at that point in time.

Example: *usernames and passwords*

---

# Log Locations

AWS ElasticBeanstalk default 'interesting' log locations:

* Rails: `/var/app/current/log`
* NGINX: `/var/log/nginx`
* Puma: `/var/log/puma`

^ AWS EB has logs set up for you by default and also logrotate. Very useful!

^ When first starting out, not knowing where things are on a unix system is frustrating. This list above is basically all you need for a rails app, generally.

---

# Exception that was raised

Class: `JsonApiClient::Errors::NotAuthorized`

Where from: `json_api_client` gem.

![inline](request-flow-not-authorized.png)

^ Googling it revealed that it maps to a http status code - 401 unauthorized.

^ Who is familiar with http status codes?

---

# HTTP 401 Unauthorized

^ Talk about what that means from a http point of view, i.e. we're sending the wrong username and password

---

# HTTP Basic Authentication

![inline](http-basic-browser-prompt.png)

---

# HTTP Basic Authentication (cont.)

Username and password are base64 encoded like this:

`Base64.encode64(username + ':' + password)`

In JavaScript: `btoa(username + ':' + password)`

^ Ask people to look up base64 encoding later.

---

# HTTP Basic Authentication (cont.)

Username: `Aladdin`
Password: `OpenSesame`

HTTP header generated:

`Authorization: Basic QWxhZGRpbjpPcGVuU2VzYW1l`

---

# Test with alternative methods!

Using `curl` to test makes reproducing this much easier to reproduce.

See `-u, --user <user:password>` in `man curl`

^ Talk about getting full endpoint from logs.

^ Teammates who are debugging also appreciate this

---

# `curl`ing works, wtf?

---

# Investigate other server

Dead end. Logs in Rails and NGINX don't have full credentials logged by default.

We also already know that it works!

^ Mention that redeploying to log usernames and passwords probably isn't a good idea.

---

# Investigate the header

How do we set the header in our code? Like this:

```
connection_options[:headers] = {
  'Authorization' => "Basic #{Base64.encode64(API_KEY + ':' + PASSWORD)}"
}
```

---

# Spot the bug

```
irb(main):003:0> Base64.encode64('mysecretusername:TXlTZWNyZXRVc2VybmFt...')

=> "TEZ4OVJvSi9tc3R3V3BodXpUanNkTFFlTURheFJvcmtBTExCYVdOTUZSeFFw\nUlJSR3NUVW
55WGZwTENqYnFqVzpUWGxUWldOeVpYUlZjMlZ5Ym1GdFpUcE1S\nbmc1VW05S0wyMXpkSGRYY0do
MWVsUnFjMlJNVVdWTlJHRjRVbTl5YTBGTVRF\nSmhWMDVOUmxKNFVYQlNVbEpIYzFSVmJubFlabk
JNUTJwaWNXcFg=\n"
```

---

# Realization

![inline](hipchat-realization.png)

---

# Fix

```
Base64.strict_encode64('mysecretusername:TXlTZWNyZXRVc2VybmFt...')
```

^ Why didn't this happen in staging? username and password were shorter.

---

# Smoke test!

---

# Checklists

Operation of a system is very complex.

Without a checklist, you're going to miss something.

New systems, feature, and bugs should have checklists!

---

# Lessons learned

* Checklist before system is operational
* Smoke tests are great
* Reproduce the error as simply as possible
* Mental models are critical

---

# The end.

# Any Questions?

^ One image from http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts.concepts.architecture.html
