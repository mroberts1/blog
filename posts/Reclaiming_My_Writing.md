I released a new tool for my blog yesterday which also marks my first project in [Elm](elm-lang.org). It's a small [WYSIWYG](https://en.wikipedia.org/wiki/WYSIWYG) [editor for Markdown files](blog.veitheller.de/blargl). I'm fairly happy with it. It's simple and efficient and doesn't get in my way. Time will tell whether I actually use it to write my posts, but I consider it to be useful, at least at the moment. And I learned a bit about Elm on the way, which is a nice byproduct of the experiment.

## The Third Newtonian Law of Motion

I can now say that I know about the buzz of the week, [Functional Reactive Programming](https://en.wikipedia.org/wiki/Functional_reactive_programming). It's an interesting concept, and I read both Evan Czaplickis [thesis](https://www.seas.harvard.edu/sites/default/files/files/archived/Czaplicki.pdf)–Evan is the inventor of Elm—and [the Tarpit paper](http://shaffner.us/cs/papers/tarpit.pdf) with gusto. The latter is a bit long, but well worth the read. All the more fascinating is how much trouble I had to get this right. I am still not completely sure whether I did it the Elm way, but the end product is decent so I'm more than happy.

Starting to program in Elm felt weird. It was not unlike that time when I first tried to program Haskell, where I learned I didn't know programming per se, but rather the tools that I have. That experience was rewarding and humbling, and I felt the same sensation when programming Elm. Of course having programmed in Haskell helped me to feel at home in the syntax, but setting up a model, events, commands, and subscriptions was not as straightforward an experience as I had hoped. And all of that [in less than 50 lines of Elm](https://github.com/hellerve/blog/blob/master/blargl/src/Blargl.elm). I did not have to fight with Markdown—Evan himself has written a library to do that for me—and so the programming I had to do was rather simple. The wiring of the components did not feel simple or natural for me, however, and I'd say that this is mostly Javascript's fault. I've been tainted.

## Cause and Effect

Still, I could see myself programming in Elm more often in the future. The tooling is great for a language that young—certainly more advanced than what we have in zepto—and once you understand the basics of ports and models it's actually relatively smooth sailing. It felt a little verbose sometimes, but I assume that's just because I'm not using the right abstractions yet. I also inlined all of the styles, which makes up more than half of the program. That I would probably do differently next time.

If you want to use the editor, feel free. And never mind the save button, it's not all that great yet. I'll fix that when I find the time.