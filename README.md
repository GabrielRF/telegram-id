# How to get an id to use on Telegram Messenger

###### The ultimate guide

* [Attention](#attention)
* [Telegram Web](#telegram-web)
  * [User ID](#web-user-id)
  * [Group ID](#web-group-id)
  * [Channel ID](#web-channel-id)
* [Telegram-CLI](#telegram-cli)
  * [User ID](#cli-user-id)
  * [Group ID](#cli-group-id)
  * [Channel ID](#cli-channel-id)
* [Telegram-App](#telegram-app)
  * [User ID](#app-user-id)
  * [Group ID](#app-group-id)
  * [Channel ID](#app-channel-id)

---

## Attention

##### This guide aims on bot developers. If you don't develop Telegram Chatbots or don't use Telegram CLI, this guide is not for you. Don't expect to get phone numbers or to join groups by their id. Both are impossible.

---

## Telegram Web

Available on https://web.telegram.org/?legacy=1#/login (have to use the legacy Telegram web client)

Follow the steps displayed to log in the app.

### Web User ID

It's not possible to find the user ID using this method. So, the easiest way to do it is talking to [@userinfobot](https://telegram.me/userinfobot). If you need to find somebody else's ID, forward a message to the bot.

###### _This bot is not mine! Use it on your own risk!_

### Web Group ID

Click on the group you want and see the url displayed on your browser.

If it's a __public__ group, you can simply use it's `@name` as an id.

If it's __private group__, the url must be like:
```
https://web.telegram.org/#/im?p=g331054
```
If this is the case, then the group ID is `-331054`. Always negative!

For __private super groups__ the url must be like:
```
https://web.telegram.org/#/im?p=s1041843721_16434430556517118330
```
If this is the case, then the group ID whois be `1041843721`. But it's important to know that __super group IDs__ are always a 13 characters negative integer, so the correct ID is `-1001041843721`.


### Web Channel ID

Click on the channel you want and see the url displayed on your browser.

If it's a __public__ channel, the ID is `@name` of the channel.

If it's a __private channel__ then the url must be similar to:
```
https://web.telegram.org/#/im?p=c1018013852_555990343349619165
```

If this is the case, then the channel ID would be `1018013852`. It's important to know that channel's IDs are always negative and 13 characters long! So add `-100` to it, making the correct ID `-1001018013852`.

## Telegram-CLI

The best way I found to get ids is using Telegram-CLI. 

It's available on https://github.com/vysheng/tg 

Install and run it. I recommend using bot mode `-b`, but it's optional.

Run `Telegram CLI`:

```
bin/telegram-cli -k tg-server.pub -b
```

Wait for it do load and then paste a bot token.

The output must be similar to this:

```
root@prod:/usr/src/tg# bin/telegram-cli -k tg-server.pub -b
change_user_group: can't find the user telegramd to switch to
Telegram-cli version 1.4.0, Copyright (C) 2013-2015 Vitaly Valtman
Telegram-cli comes with ABSOLUTELY NO WARRANTY; for details type `show_license'.
This is free software, and you are welcome to redistribute it
under certain conditions; type `show_license' for details.
Telegram-cli uses libtgl version 2.1.0
Telegram-cli includes software developed by the OpenSSL Project
for use in the OpenSSL Toolkit. (http://www.openssl.org/)
I: config dir=[/root/.telegram-cli]
[/root/.telegram-cli] created
[/root/.telegram-cli/downloads] created
hash: 
```

### CLI User ID

To get a user id, ask the user to send any message do the bot and observe it on `Telegram CLI` window.

The message must appear similar to this:

```
[11:07]  Gabriel R F »»» /start
```

Then, on `Telegram CLI`, type:

```
user_info Gabriel_R_F
```

Note that spaces are replaced by `_`.

The output will be something like this:

```
User Gabriel R F @GabrielRF (#9083329):
        phone: (null)
        offline (was online recently)
```

There you go! The user id, on this example, is `9083329`.

### CLI Group ID

Add the bot to the group. On `Telegram CLI`, a message will be printed.

```
[11:12]  test Gabriel R F added user test
```

Then, on `Telegram CLI`, type

```
chat_info test
```

Where `test` is the group's name. Note that spaces are replaced by `_`.

The output on `Telegram CLI` will be similar to:

```
Chat test updated admin members
Chat test (id 148228539) members:
                test invited by Gabriel R F at [2016/03/29 11:12:30]
                Gabriel R F invited by Gabriel R F at [2016/03/29 11:11:18] admin
```

So, the id for the example group is `-148228539`. 

Group ids are always a __negative integer__, so remember to add the `-` while using it on the Telegram API.

### CLI Channel ID

Finally, to get a channel id, add the bot as a channel `administrator`.

On `Telegram CLI` type:

```
channel_info test
```

where `test` is the channel's name. The output must be like this:

```
Channel test (id 1035716040):
                2 participants, 2 admins, 0 kicked
```

Here is the trick. Every channel id is a __13 characters negative integer__. So the id for this channel is `-1001035716040` and not `1035716040` as printed.

## Telegram App

You can use the app directly to generate a direct link to the message and it will contain the group/channel information.

### App User ID

It is not possible to get user ID from the app itself. Have to get it from a [bot](#web-user-id) or [CLI](#cli-group-id)

### App Group ID

Tap/click on the group you want and hold/right click on a message. Copy the message link.

If it's a __public__ group, you can simply use it's `@name` as an id.

If it's __private group__, it is not possible to get a link. Have to use [CLI](#cli-group-id) or [Web](#web-group-id) method

For __private super groups__ the link must be like:
```
https://t.me/c/1041843721/200
```
If this is the case, then the group ID whois be `1041843721`. But it's important to know that __super group IDs__ are always a 13 characters negative integer, so the correct ID is `-1001041843721`.

### App Channel ID

Tap/click on the channel you want and hold/right click on a message. Copy the message link.

If it's a __public__ channel, the ID is `@name` of the group.

If it's a __private channel__ then the url must be similar to:
```
https://t.me/c/1018013852/193
```

If this is the case, then the channel ID would be `1018013852`. It's important to know that channel's IDs are always negative and 13 characters long! So add `-100` to it, making the correct ID `-1001018013852`.

### Questions?

Talk to me on Telegram Messenger! [@GabrielRF](http://telegram.me/GabrielRF)
