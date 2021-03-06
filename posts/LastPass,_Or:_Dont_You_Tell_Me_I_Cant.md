One of my current clients is forcing me to use LastPass. I find it generally
terrible, but I guess it makes sense for their use case. I had to deal with
some unexpected form prefills that led me to log in with the company account
where I didn’t want to, but other than that the friction level is low.

Today I want to talk to you about a promise that LastPass is making to their
users—one that it cannot possibly keep—, and obviously breaks. Then let’s talk
a bit about “regular users”, responsibility, and the one thing I would change
in my industry if I could only pick one.

## “You are not permitted to view the password”

LastPass is a password manager. It has a team feature, meaning there are these
things called “shared sites” that multiple people can have access to. This is
well and good and old news.

A few days ago, I needed to access a password for a service that uses the same
credentials on the command line as on the web, and I clicked on the appropriate
account. I saw all of the info about the account, including a password text
field with what was ostensibly my password in it, represented by a series of
dots—you know the type. There is an eye on the right side that reveals the
password, and I clicked it. But LastPass told me that, with these credentials
belonging to a shared site, I’ve lost my right to actually _see_ the password.

![](/assets/popup.png)
<div class="figure-label">Fig. 1: Really?</div>

This struck me as odd. With the password having to be prefilled into forms and
such, how would they ensure I wasn’t able to see the password? Maybe there is
some twisted way of making it hard for the user to get it, but if they fill it
into text fields in my browser, surely it must be there _at some point_, right?

Of course they don’t protect that password. They can’t. Thus, when I change the
`type` property of the input field from `password` to `text`, I can see the
password. The promise they just made—that I was not permitted to view it—is
broken.

Of course this is not your CVE-level stuff. It turns out that the last item on
their [FAQ for security reports](https://lastpass.com/support_security.php#securityfaqs)
tells me that this is known. It is telling that all of the truly
customer-facing lingo is that of permissions and security, while their
technical FAQ is a tad more factual. It is a little sad that you have to
know HTML to be taken seriously.

## You cannot handle the truth

Our industry is used to coddling users. We don’t take them seriously; we treat
them like toddlers, and you don’t give toddlers power tools. So what we give
them are shiny things that make the appearance of working well—if there is an
error, it is rarely propagated further up than into a console that is, by
default, tucked away neatly into the nooks and crannies of the system. If it is
caught at all, that is.

This is a decision that I find regrettable, because it is not empowering to the
user, quite the opposite. But it is understandable, at least: we are faced with
an onslaught of errors every day, and sometimes it is hard to differentiate
between those that are benign and those that are indicative of serious damage.
It would take an edifice akin to the human immune system to classify and tackle
those problems and only show the users the kinds of problems that they might be
interested in knowing about, such as severe engine failure. Ain’t nobody got
time for that.

Where it gets really nasty, then, is when marketing is involved. Now, don’t get
me wrong: marketing well done can be beautiful, even though it will always be
about selling things. But it has a choice to make, and that is to be truthful or
to sugarcoat. Outright lie is uncommon. If you look back at Figure 1, you will
realize that while the popup says I’m “not permitted” to see the password, it
doesn’t say I’m not able to. It creates a false sense of security, by playing
an intuition about what the sentence _should_ mean against the reality of what
it indeed does stand for. It’s a shame that we think we have to resort to these
sorts of nasty tricks to make our products sell, instead of being upfront about
what they can and cannot do.

This is not about LastPass. Every day you’re told a tiny half-truth like that,
no matter if you’re technically literate or not. If you happen to be
tech-literate, though, you might be able to catch your tools pretending.

## Fin

I don’t know what this means. Be honest, I guess? When I write about systems,
when I communicate ideas, one of my primary concerns is to talk about some of
the drawbacks I can think of. What I want is to spread knowledge and get
feedback, and if whatever I’m talking about is worth its salt, adoption. I
would love to see the application of this principle in larger parts of the
tech industry, and the market in general, even if that idea is mine. I don’t
know how it would, if done well, affect sales, but I do know that people have
repeatedly told me they are grateful for the openness with which I
communicate—without “openness” being used as a codeword for outright vitriol.

Maybe that’s the big idea that I have, the one grand spark each of us gets,
and, if we find it, we spend our lives pursuing its adoption into the
mainstream. And I threw it away by making it a sour blog post.
