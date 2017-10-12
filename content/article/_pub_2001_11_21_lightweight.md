{
   "image" : null,
   "description" : " What happens if you get a bunch of academic computer scientists and implementors of languages such as Perl, Python, Smalltalk and Curl, and lock them into a room for a day? Bringing together the academic and commercial sides of...",
   "authors" : [
      "simon-cozens"
   ],
   "thumbnail" : null,
   "draft" : null,
   "title" : "Lightweight Languages",
   "tags" : [
      "lightweight-languages-conference-mit-ai-research-academic"
   ],
   "slug" : "/pub/2001/11/21/lightweight",
   "date" : "2001-11-21T00:00:00-08:00",
   "categories" : "community"
}





What happens if you get a bunch of academic computer scientists and
implementors of languages such as Perl, Python, Smalltalk and Curl, and
lock them into a room for a day? Bringing together the academic and
commercial sides of language design and implementation was the
interesting premise behind last weekend's Lightweight Languages
Workshop, [LL1](http://ll1.mit.edu), at the AI Lab at MIT, and I'm happy
to say that it wasn't the great flame-fest you might imagine.

While there were the occasional jibes from all sides, (and mainly in our
direction) it was a good-natured and enjoyable event. The one-day
workshop began with a keynote by Olin Shivers, associate professor of
computing at Georgia Tech, on how "Lambda" was the ultimate little
language. He was, of course, teaching us about the Joys of Scheme. Olin
showed us how we could use Scheme as a basis for implementing
domain-specific languages, such as awk, and by embedding these languages
in Scheme, one would have not just the power of the original language,
but also the implementation language available as well. The alert reader
will remember that this is something Larry spoke about in the State of
the Onion this year with regard to Perl 6, and something that Damian
Conway and Leon Brocard have been working on in Perl 5.

Olin demonstrated the power of his "embedding" technique by calling from
Scheme to Awk and from Awk back into Scheme in the same routine. He's
even written a [Scheme shell](http://www.swiss.ai.mit.edu/ftpdir/scsh)
along the same lines, but there was some disagreement as to whether or
not being able to do shell-like things with Scheme syntax means you have
a Scheme shell. Olin also brushed aside suggestions that writing Awk,
Scheme and Shell in the same syntax in the same function might be
potentially confusing, saying that it had never tripped him up.

Next came an enlightening panel discussion on the merits of [the
Worse-Is-Better
philosophy](http://www.dreamsongs.com/WorseIsBetter.html); that is, the
idea, that doing it right is not as important as doing it right now. I
spoke first, explaining how Parrot development has to strike a balance
between being correct, maintainable and fast, and ended by asking why
doing the right thing is almost always the opposite of doing the fast
thing; Jeremy Hylton, one of the Python developers and a really nice
guy, replied that Python did not have this problem - for them,
correctness and maintainability were more important than performance,
giving them more flexibility in terms of doing it Right.

Dan Weinreb piped up with the idea that programming implementation tends
to be driven by managerial paranoia; thankfully, this is something that
both the open-source language implementation community and the academic
community are pretty much immune from. Nevertheless, the pressure to
release can have adverse affects on future performance, as illustrated
by Guy Steele, one of the designers on Java, who told us a sad story
about the dangers of Worse Is Better - by putting some vital component
of Java (I think it was tail recursion, but it might have been something
else) off in order to get release 1.0 out of the door, it made it much
harder to implement later on. This resonated with the experience that
Python implementors had adding lexical scoping. This rapidly caused a
degeneration into whether a language without lexical scoping or the
lambda operator can be said to be properly thought out.

Joe Marshall gave a short talk on one element of the initial
implementation of the Rebol programming language. Rebol 1.0 was slightly
different from the "network programming language" that Rebol is today -
it was essentially Scheme with the brackets filed off. He explained that
in his original Scheme implementation, he used a terribly complicated
trick to avoid outgrowing the stack; something that was completely
rewritten in the next implementation. Again we found that
maintainability was more important in the long run.

Jeremy Hylton then gave his presentation, on the design and
implementation of Python. It was amusing but, at least to me, not
entirely surprising, that Jeremy was the one developer at the conference
that Dan Sugalski and I had most in common with. The implementation
teams of Perl and Python are facing very much the same problems and
approaching them in only very slightly different ways. That is, compared
with many of the other approaches we saw presented, at least.

Then it was our turn. We were running very late by this point, so I
skipped over most of my talk; Dan explained what a lightweight language
usually needed from its interpreter, and how Parrot was planning to
provide that. David Simmons, one of the developers of SmallScript, a
"scripting" Smalltalk implementation, challenged us on the viability of
JIT compiling Parrot code, something we were interested in after looking
at the [Mono project](http://www.go-mono.com)'s JIT compiler.

We had been intrigued all day by the title of Shriram Krishnamurthi's
talk, "The Swine Before Perl." We didn't know whether that referred to
us or to Jeremy, who was talking before us. In the event, Shriram
delivered a wonderfully interesting presentation about Scheme, and how
he could apply "laziness, impatience and hubris" to Scheme programming.
He mentioned a Scheme Web server that served dynamic pages many times
faster than Apache/mod\_perl, and a way of manipulating Scheme macros to
provide a pre-compiled state-machine generator. He countered criticisms
that Scheme is just lots of insane silly parentheses by demonstrating
how XML was just lots of insane silly angle brackets. A fair point well
made.

Waldemar Horwat lead us through some of the more important design
decisions involved in JavaScript version 2.0. No, don't laugh, it's a
much more fully featured language than you'd think. His main point was,
unsurpisingly, something else that Larry had picked up on in his State
of the Onion talk; that modules need to provide ways of encoding the
version of their API so as to protect their namespace from subclasses.
That's to say, if there's a Perl module `Foo` and you subclass it to
`Foo::Advanced` by adding a `frobnitz` method, then what happens when
the original author of `Foo` produces the next version of `Foo` that
already has a `frobnitz` method? Waldemar's solution was to use
version-specific namespaces that only expose certain subsets of the
whole API if a particular version number is asked for. This allows
dependent modules to be future-proofed.

Christopher Barber gave a talk on Curl, a bizarre little language that
fills the same sort of niche as Flash. David Simmons spoke about
SmallScript and his work porting Smalltalk to the Microsoft CLR; he had
high hopes for the way Microsoft .NET was panning out. Jonathan
Bachrach, one of the AI Labs researchers gave a clever talk, which I
missed due to being out in the corridors debating the finer points of
threading and continuations with a Scheme hacker. I returned to see him
explain a efficient but highly difficult to follow method of determining
whether two classes are the same; he also said that his language
compiles down to C and the C compiler is executed on the fly, since it's
faster to call GCC than to start up your own virtual machine. Paul
Graham rounded off the talks by talking about his new dialect of Lisp,
which he called Arc. Arc is designed to be a language for "good
programmers" only, and gets away without taking the shortcuts and
safeguards that you need if you're trying to be accessible. His
presentation was very entertaining, and I have high hopes for his little
language.

As I've indicated, the interest of the workshop was as much what was
going on outside the talks as well; Dan and I got to meet a load of
interesting and clever people, and it was challenging for us to discuss
our ideas with them - especially since we didn't always see eye to eye
with our academic counterparts. Sadly, few people seemed to have heard
much about [Ruby](http://www.ruby-lang.org/), something they will
probably come to regret in time. Dan seemed to have picked up a few more
interesting technical tips, such as a way to collect reference count
loops without walking all of the objects in a heap. Oh, and we found
that you should pour liquid nitrogen into containers first rather than
trying to make ice cream by directly pouring it into a mix of milk and
butter. And that the ice-cream so produced is exceptionally tasty.

But seriously, what did we learn? I think we learned that many problems
that we're facing in terms of Perl implementation right now have already
been thoroughly researched and dealt with as many as 30 years ago; but
we also learned that if we want to get at this research, then we need to
do a lot of digging. The academic community is good at solving tricky
problems like threading, continuations, despatch and the like, but not
very interested in working out all the implications. To bring an
academic success to commercial fruition requires one, as Olin Shivers
puts it, "to become Larry Wall for a year" - to take care of all the
gritty implementation details, and that's not the sort of thing that
gets a PhD.

So the impetus is on us as serious language implementors to take the
time to look into and understand the current state of the art in VM
research to avoid re-inventing the wheel. Conferences such as LL1, and
the mailing list that has been established as a result of it, are a
useful way for us to find out what's going on and exchange experience
with the academic community, and I look forward intently to the next
one!

*O'Reilly & Associates was proud to be a co-sponsor of the Lightweight
Languages Workshop.*

