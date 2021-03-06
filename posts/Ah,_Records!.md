One of the last projects I was working on before leaving for the US was
[hi](https://github.com/hellerve/hi), a minimal, performant chat system.
I'll talk about this in a later post, but right now I want to focus on a bug
that really took me by surprise. It has nothing to do with software development
and everything with operations.

## The Three Investigators in The Secret of the Mising Header

While I was on vacation my hosting provider [Webfaction](http://webfaction.com/)
informed me that they would need to perform a VM migration, which meant my sites
would be unavailable for the duration of the maintenance and the IP address
would change. Fair enough, I thought. The migration came and went, and I
checked whether everything was still in working order. It did, so I went back to
visiting distilleries and overeating. This is where you should start to get
suspicious. There was an IP change, and everything just worked? Weren't the
A records wrong now? And of course you got it exactly right, for my DNS records
are managed by another provider. But my vacation brain wasn't prepared to think
about any of that and the sites _seemed_ to be chugging quite merrily along. So
the problem was deferred until it bubbled up a week after I had returned from
the US.

The chat service uses WebSockets to distribute messages between clients
in real time. WebSockets use regular TCP connections, and its initial handshake
uses HTTP. It works like this:

1. An initial HTTP request is sent. The most important headers to look out for
   are the `Connection` header, the value of which should be `Upgrade`, and the
   `Upgrade` header, the value of which should be `websocket`. There is also a
   random key being transmitted and some metainformation, but for the sake of
   this post, we will omit that.
2. The server responds with the HTTP status code 101 (`Switching Protocols`).
   The `Upgrade` and `Connection` headers stay the same, the key will be sent
   back hashed, to identify the connection—not for security reasons.
3. The connection is now a duplex connection and messages will be sent back and
   forth using the WebSocket protocol. Yay!

This, in connection with the IP change, came back to bite me when I continued to
work on the chat application. I realized that the websocket handshake between my
browser and the server failed, and thus I couldn't connect to the chat. Weird.
The logs told me that my server found some of the headers needed for a successful
handshake were missing—`websocket: not a websocket handshake: 'websocket' token
not found in 'Upgrade' header`. A quick look into the developer console confirmed
that my browser did send that header.

This meant that the header was somehow lost in transmission, and my first guess
was that the [NGINX](https://www.nginx.com/) configuration was somehow mangling
the headers. Ironically, at this point I remembered that the migration had
happened, but instead of thinking about DNS, I guessed that the NGINX
configuration had somehow not been migrated correctly. I wrote a minimal client
and server to test my assumptions and started tweaking the controls, to no avail.
It soon became obvious that NGINX was actually fine.

At this point I was stumped and had to ask Webfaction for help. They are generally
very helpful and great, and when submitting a ticket I never feel as dumb as I
probably should. They're really patient with me, and I would wholeheartedly
recommend this hosting provider to anyone who asks.

## Burned HTTP Bridges

It didn't take long for Webfaction to find the bug—which was surprising,
since I opened the ticket on a Saturday, expecting it to be first touched on Monday.
Instead, I was able to solve it on the same day.

It turns out that Webfaction had helpfully added a reverse proxy for HTTP to point
to the old IP address, which caused most of my services to work still. The NGINX
configuration _on that machine_ however was not setup for Websocket traffic or
headers and so it threw the headers away before relaying the requests. Sneaky.
So, the error was in fact configuration-related, but the configuration of another
machine. I updated the A records and the bug went away, causing me to feel stupid.

## Write a List

One immediate takeaway from this bug is that I behave very differently in
professional and personal life. When at work, I always check what needs to be
done upfront. When on vacation, I obviously throw that right out of the window.
That's unfortunate, but leads to fun learning experiences. So, in the end, I'm
somewhat glad I ran into this bug. Next time, I will have a list of things that
need to be done before, during, and after the maintenance at hand.

I also want to give Webfaction another big shout-out: I couldn't be happier with
my experience with them, both in everyday business and in the kinds of scenarios
where I shoot myself in the foot and need a medic as quickly as possible. I host
a ton of different tools and services there and all of them were a breeze to set
up, no matter whether I'm using Python, Go, Node.js, or any other technology.

Anyway, I hope you don't think less of me for running into such a mundane bug
and that you'll stay tuned for an upcoming post on hi, the chat service.
