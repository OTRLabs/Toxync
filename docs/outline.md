The primary purpose of this application is to serve as an instant messaging application for

- sending quick messages between users of the [Conti-platform]() as well as Tox as a whole
- sharing files
- Getting quick updates in a notification / ping / pager fashion, typically linking to something within the Conti platform
- Potentially, a final form of authentication, similar to SMS OTP codes for
- select SOCKS proxy to prevent IP leakage to Tox friends (promoting use of mixnets)
- Quick programmatically generated GIFs

## anti-goals

- I have no intention of developing live video/audio chat capabilities. That is a glaring operational security risk.

## we will see features:

- screen sharing? Seems risky.

## Securing the application

**make sure we aggressively sanitize any and all messages coming from external sources:** 

we need to be 100% positive that you can not just run, say JavaScript with some kind of SSTI via a message.

I don’t think that’s actually possible. Because wails says it renders the app natively & doesn’t use a browser. But I assume JS could still run in this environment as well if not properly sanitized so we Must make every effort to be on top of that

**Securing User data at rest**:

Ok, honestly. This stems from the Signal drama, where on some platforms (I know windows off the top of my head), the signal desktop app were not encrypting user messages on the device when at rest. 

My opinion on the subject: 

On some level, I see the Signal Devs side in not implementing the code because honestly if someone had already compromised my desktop that deep I am not especially concerned about… what was it an SQLite db or something? Seems more likely that the average attacker would spin up a VNC server and just use the desktop but I am kinda talking out of my ass here.

Especially because on the other hand, the fix did not seem to be absurdly complicated & signal is used by people who’s lives depend on maintaining their messages privacy, who could easily have their devices physically compromised 

Also I’m sorry I just kinda find the idea of having state of the art quantum resistant encryption for the transport layer & then it getting there & the dev being like ok fuck u ur on ur own

# Comparing & Contrasting against “secure instant messaging apps”

## standard Tox

- encryption: Tox uses the cryptographic primitives present in the [NaCl crypto library](http://nacl.cr.yp.to/index.html), via [libsodium](https://github.com/jedisct1/libsodium). Specifically, Tox employs [curve25519](https://en.wikipedia.org/wiki/Curve25519) for its key exchanges, [xsalsa20](https://download.libsodium.org/doc/advanced/xsalsa20.html) for symmetric encryption, and [poly1305](https://en.wikipedia.org/wiki/Poly1305) for MACs.
- architecture: peer to peer
- Routing: onion for users who are not your friend. Direct* P2P connection with your tox Frienfs

## toxync enhancements

- Built in Tox proxy manager. Makes getting set up with a variety of mix nets easier.

# competing secure messengers

I’m going to get this out of the way right now:

Any of these  messenger applications/ services that has a blockchain as a part of its ecosystem is automatically lost in the sauce. 

Oxen as an organization is cool, and assuming they are not a honeypot by the Australian Feds, they have done some cool research and provided cool services.

Generally speaking my criticism of these apps Comes down to “they are doing too much & not getting enough from it”

Like there is (in my opinion)

### Session Messenger

- owned by: Oxen
- Routing: clients use 3 hop onion routing to mask their connection to the session network which runs on Lokinet
- Cons: has a blockchain attached to it

### Synapse Home server

- **routing**: uses matrix protocol. Fairly flexible