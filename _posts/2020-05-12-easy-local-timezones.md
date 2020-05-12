---
layout: post
title: How to easily render local timezones on a webpage without asking the user for their location
description: ""
categories: tech
tags: [frontend, javascript, tech, django]
---

Recently, due to the pandemic, I built a webpage to aggregate musician and DJ
livestreams on the web called [All Day I Stream](https://alldayistream.com). Most
streams are on Twitch, however many are on Youtube, FB or Instagram Live, or custom 
web pages. Additionally, Zoom parties around the livestream have been catching on 
in a big way, so there's been a lot of focus on coordinating those parties.

Of course, people get annoyed if you don't render the start times of the stream in their local timezone, so while 
we initially listed all the start times in EDT, one of the biggest initial complaints was for local timezone support.

The site is currently a Django webpage backed by Google App Engine. I am a lot more comfortable with Python than
Javascript so I was looking for a way to do the timezone localization server side.

I had previously mistakenly believed there were a few ways to accomplish this, none of which are great:

* **Ask the user to create an account and specify their timezone preference**
* **Require the user to provide their location to get local timezones**
* **Guess their timezone based on their IP address (not very accurate)**

However, my friend and former colleague [Chris Broadfoot](https://twitter.com/broady) pointed out there's a better way
to accomplish this: Javascript! Of course, I'm sure it's possible to do this _all_ in frontend Javacript, but I know 
Python a lot better and was hoping to leverage Python's datetime libraries to do the heavy lifiting. Fortunately, you
only need a few lines of Javascript and can then let the server do the rest of the work. However, If you have a favorite Javascript library to accomplish this, let me know on [Twitter](https://twitter.com/waprin_io).

Any timezone you serve as part of your web page should not be delivered initially, but instead be served by an AJAX call.
Before you make this AJAX call, you use Javascript to get the user's timezone or UTC offset, add that as a parameter to
the call, and then the server can use that to provide the local timezone.

# First, get the user's timezone

The key to get the user's timezone is in two Javascript functions outline in [this Stackoverflow question](https://stackoverflow.com/questions/1091372/getting-the-clients-timezone-offset-in-javascript).
The first is `new Date().getTimezoneOffset()`, which just offers the offset from UTC. This is almost always supported, but makes it difficult to 
render the user's actual timezone, since multiple timezones can have the same offset. It's also nice for the user if they see the abbreviation of their timezone
rendered (EDT, PDT for Americans, VET for a Venezuelan), which is only possible if you know the actual timezone, since if you just have the offset you have to guess.

Fortunately, there's a way to get the actual timezone that's usually supported as the second answer to that Stack Overflow answer:

`console.log(Intl.DateTimeFormat().resolvedOptions().timeZone)`

Since this is usually but not alway supported, I wrap it in a `try/catch` that falls back to `getTimezoneOffset` if it fails.

# Now render the timezone on the server

Once I have the timezone name, or the offset, I can use Python/Django's excellent datetime libraries to render the timezone in a local format:

```
    local_tz = None
    if tzInfo: # tzInfo is passed an AJAX parameter based on Intl.DateTimeFormat().resolvedOptions().timeZone
        try:
            local_tz = pytz.timezone(tzInfo)
        except Exception as e:
            print(f"failed to load timezone {tzInfo}")

    if local_tz is None: # fall back to tzOffet which was obtained by new Date().getTimezoneOffset()
        tz = 'Local' 
        # if we don't know the timezone , we can guess based on the offset
        # you have to manually fill this in with your best guess of a timezone based on offet, e.g. 240 -> EDT
        tz_mapping = { 
            'offset': 'timezone'
        }
        if tzOffset in tz_mapping: 
            tz = tz_mapping[tzOffset]
            
    if local_tz is not None:
        local_start = start_date.astimezone(local_tz)
    else:
        local_start = stream.start_date + datetime.timedelta(minutes=(-1 * tzOffset))
        # manually set timezone here based on tz offet guess
        
    start_time = utc_start.strftime("%I:%M %p") # renders as 12:30 PDT        
            
     
```

And that's it! With this approach, I can let Python and Django do the heavy lifting of timezone localization and 
render the time in each user's timezone without asking them for their location or preferences. 
