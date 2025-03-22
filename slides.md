---
theme: envek
# progressbar settings for envek theme
talkDurationMinutes: 25
progressBarStartSlide: 2

title: Ruby in Japan vs the World
titleTemplate: '%s - Osaka Web Designers and Developers Meetup'

# https://sli.dev/features/drawing
drawings:
  persist: false

# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true

# Current slide settings
layout: cover
class: text-left
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
---

# Ruby in Japan vs the World

<div class="absolute bottom-0 left-0 w-full py-5 px-12 grid grid-cols-2 justify-items-stretch items-end gap-4">
  <div class="text-left">
    Andrey Novikov, Evil Martians<br />
    <small><a href="https://owddm.com/">Osaka Web Designers and Developers Meetup</a></small><br />
    <small><time datetime="2025-03-22">22 March 2025</time></small>
  </div>

  <div class="w-28 h-28 scaled-image justify-self-end">
    <a href="https://evilmartians.com/"><img alt="Evil Martians" src="/images/01_Evil-Martians_Logo_v2.1_RGB.svg" class="block dark:hidden" /><img alt="Evil Martians" src="/images/02_Evil-Martians_Logo_v2.1_RGB_for-Dark-BG.svg" class="hidden dark:block" /></a>
  </div>
</div>

<div class="absolute top-0 left-0 w-full scaled-image h-36 p-4 text-center">
<a href="https://owddm.com/" class=""><img alt="Osaka Web Designers and Developers Meetup" src="/images/owddm-outline@1x.png" class="block mx-auto" /></a>
</div>

<style>
  a {
    border-bottom: none !important;
  }

  h1 {
    text-align: center;
    margin-top: 1em;
    font-size: 320% !important;
  }
</style>

---
class: annotated-list
layout: image-right
image: /images/andrey-cub.jpg
---

# About me

- I'm Andrey

- @Envek on GitHub and everywhere

- Back-end engineer at Evil Martians

- Ruby, Go, PostgreSQL, Docker, k8s…

- Living in Suita, Osaka for 2 years

- Love to ride mopeds, motorcycles, and cars over Japan

---

<a href="https://evilmartians.com/?utm_source=owddm&utm_medium=slides&utm_campaign=ruby-in-japan-vs-world">
<LightOrDark>
  <template #light>
    <img alt="Evil Martians" src="/images/01_Evil-Martians_Logo_v2.1_RGB.svg" class="block object-contain text-center m-auto max-h-100" />
  </template>
  <template #dark>
    <img alt="Evil Martians" src="/images/02_Evil-Martians_Logo_v2.1_RGB_for-Dark-BG.svg" class="block object-contain text-center m-auto max-h-100" />
  </template>
</LightOrDark>
</a>
<p class="text-2xl text-center"><a href="https://evilmartians.com">evilmartians.com</a></p>
<p class="text-xl text-center"><a href="https://evilmartians.jp/">evilmartians.jp</a></p>
<div class="absolute bottom-32px left-32px rotate-10 text-2xl">邪悪な火星人？</div>
<div class="absolute bottom-32px right-32px rotate-350 text-2xl">イービルマーシャンズ！</div>


---

<a href="https://evilmartians.com/services/backend-development?utm_source=owddm&utm_medium=slides&utm_campaign=ruby-in-japan-vs-world">
<img alt="Ruby Martians" src="/images/Evil-Martians_Logo_Ruby.svg" class="block object-contain text-center m-auto my--20 max-h-140 w-full" />
</a>




---

# Ruby

A programmer's best friend

```ruby
# Output "I love Ruby"
say = "I love Ruby"
puts say

# Output "I *LOVE* RUBY"
say['love'] = "*love*"
puts say.upcase

# Output "I *love* Ruby"
# five times
5.times { puts say }
```

<qr-code url="https://www.ruby-lang.org/en/" caption="ruby-lang.org" class="w-36 absolute bottom-48px right-60px" />


---
class: annotated-list
---

# Ruby

- Ruby is a general-purpose programming language, interpreted and high-level

  You need an interpreter, you don't have to understand how it works under the hood.

- Object-oriented yet functional, influenced by Perl and Smalltalk

  Everything is an object, even numbers and functions. No primitive types.

- Designed for programmer productivity and readability

  Care less about runtime performance, more about developer happiness.

- Highly dynamic: you can change almost everything at runtime

  It is called monkey patching: amend classes, redefine methods, reassign constants.

- Created by Yukihiro Matsumoto in 1995

  So it was born in Japan! And still developed by mostly Japanese core team 🇯🇵


---

## Object-oriented

Everything is an object, even numbers and functions. No primitive types.

Example: numeric overloads for [`ActiveSupport::Duration`](https://api.rubyonrails.org/classes/ActiveSupport/Duration.html)

<div class="grid grid-cols-[45%_55%] gap-4 ">
<div>

```ruby
1.month + 5.minutes
# => 1 month and 5 minutes

(1.month + 5.minutes).class
# => ActiveSupport::Duration

Time.current + 1.month
# => 2025-04-22 15:00:00 +0900
```
</div>


```ruby
# Reopen Numeric class
class Numeric

  # Define month method
  def month
    ActiveSupport::Duration.days(self)
  end
end
```
</div>

See [`activesupport/lib/active_support/core_ext/numeric/time.rb`](https://github.com/rails/rails/blob/e9d7ca5e0b834ff2ce3d43965deac670ff8ac790/activesupport/lib/active_support/core_ext/numeric/time.rb) in Ruby on Rails.

<!--
Here is also an example of monkey patching: we reopen `Numeric` class and define `month` method that returns `ActiveSupport::Duration` object.
-->

---

## Functional

Callable blocks (procs and lambdas) with closures

```ruby
# Define a lambda
y, l = 1, ->(x) { x + y }

# Call it
l.call(2) # => 3

# Use it for collection transformation
[1, 2, 3].map(&l).    # => [2, 3, 4]
          reduce(&:+) # => 9
```

More about this in [Threads, callbacks, and execution context in Ruby](https://envek.github.io/rubyconfau-threads-callbacks/) 

<qr-code url="https://envek.github.io/rubyconfau-threads-callbacks/" caption="Threads, callbacks… talk" class="w-36 absolute bottom-48px right-60px" />

<!--
Ruby has a lot of functional programming features, like blocks, procs, and lambdas. They are used for callbacks, collection transformations, and more.

Blocks are very idiomatic for the language. In Ruby for loops are rarely used, instead, we use `each` or `map` that accept blocks to iterate over collections.
-->

---
layout: two-cols-header
class: annotated-list
---

## Pros and cons

::left::

### Pros


 - Easy and quick to start with

   Non-steep learning curve

 - Readable and expressive

   Almost like English

 - A lot of ready libraries

   “There is a gem for that”

 - Nice and active community

   [MINASWAN](https://en.wiktionary.org/wiki/MINASWAN): Matz is nice and so we are nice

::right::

### Cons

 - Slow runtime performance

   Not the best for CPU-bound tasks

 - Poor parallelism due to GVL

   GVL: Global VM Lock restricts parallelism, but works well for I/O-bound tasks

 - Memory footprint

 - Debugging might be hard

   Monkey patching can make code hard to understand



---
layout: cover
---

# Brief history of Ruby


---

## Early days of Ruby (1993-2005)

- 1993: Matz started working on Ruby
- 1995: Ruby 0.95 released
- 1996: Ruby 1.0 released
- 2002: First English book about Ruby published
- 2003: Ruby 1.8 released

Ruby was mostly known in Japan and didn't have much traction.

---

## Big bang: Ruby on Rails

2005: DHH released famous “Blog in 15 minutes” video

<Youtube id="Gzj723LkRJY" height="720" class="w-full max-h-80" />

Everyone: 🤯

<qr-code url="https://youtu.be/Gzj723LkRJY" caption="Blog in 15 minutes" class="w-36 absolute bottom-48px right-60px" />

<!-- Matz might not like it, but without this event Ruby would probably stay as a niche scripting language -->

---
class: annotated-list
---

## Ruby on Rails

Highly opinionated web framework made possible by Ruby dynamic nature

- Convention over configuration

  Introspection and metaprogramming to reduce boilerplate

- No explicit requires for application code

  Everything is autoloaded, filenames are derived from class names

- Active Record

  ORM that maps database tables to Ruby objects and introspects database schema

That all allowed really rapid development of web applications!

---
class: annotated-list
---

## Boom of startups on Ruby on Rails

- <logos-twitter class="float-left text-5xl mx-2 w-16" /> Twitter (early days)

  Probably was fully rewritten to another tech stack after a few years.

- <logos-github-icon class="float-left text-5xl mx-2 w-16" /> GitHub

  Still uses Ruby on Rails, backports a lot of features to Rails itself.

- <logos-shopify class="float-left text-5xl mx-2 w-16" /> Shopify

  Runs on Ruby on Rails, manages to serve million RPS on Black Friday.

- <logos-airbnb-icon class="float-left text-5xl mx-2 w-16" /> Airbnb

  Started with Ruby on Rails, but now uses a lot of other technologies.

- <logos-heroku-icon class="float-left text-5xl mx-2 w-16" /> Heroku

  Ruby on Rails was the first supported language on Heroku.

<style>
  ul { list-style-type: none; }
</style>

---

## Great boost for Ruby itself

- Ruby 1.9 (2007)

  - YARV: move from interpretation to bytecode compilation

  - Native threads

  - Sane character encoding support

  - Syntax changes for hashes, lambdas


---
class: annotated-list
---

## Alternative Rubies

- MRI (Matz's Ruby Interpreter) - The original Ruby implementation written on C.

- TruffleRuby - A high performance implementation built on the GraalVM.

- JRuby - The Ruby Programming Language on the JVM

  Java libraries can be called directly, but C-extensions are not supported.

- mruby - lightweight partial implementation for embedded usage.

- Artichoke - Bundle Ruby applications into a single WASM binary, Ruby implementation in Rust.

and more: https://github.com/codicoscepticos/ruby-implementations

<qr-code url="https://github.com/codicoscepticos/ruby-implementations" caption="Ruby implementations" class="w-36 absolute bottom-48px right-60px" />

---
class: annotated-list
---

## Great tools from Ruby community

Level of user experience provided by Ruby itself inspired the community to create great tools, that inspired other communities.

- Bundler — dependency manager with lockfile

  Inspired Cargo, CocoaPods

- RSpec — testing framework

  Inspired Jest, Mocha

- RVM and Rbenv — Ruby version managers

  Inspired pyenv, nvm, asdf, and mise-en-place

- Capistrano — deployment tool for old server days

  Inspired many deploy tools like Ansistrano on top of Ansible

---

# Evil Martians founded (2006)

<img alt="Evil Martians" src="/images/Evil-Martians_Logo_Product-Development.svg" class="block object-contain text-center m-auto my--20 max-h-140 w-full" />

<!-- Ah, it was a great time to be a Ruby developer! -->

---

## Ruby outside of web development

- [Homebrew](https://brew.sh) – package manager for macOS (and Linux) 

- Chef and Puppet – configuration management tools

- Vagrant – virtual machine management

- [DragonRuby](https://dragonruby.org) – game development

---

## Is Ruby dying? (2015-2020)

<iframe src="https://isrubydead.com" class="w-full h-90" />

It felt stagnant, but it was not dying.

<qr-code url="https://isrubydead.com" caption="isrubydead.com" class="w-36 absolute bottom-70px right-60px" />

---

## The pandemic: Ruby's second wind

Why lockdowns and Ruby are a perfect match?

- Ruby is great for prototyping

- Ruby is great for small teams

- Ruby is great for remote work

---

## Second rise of Ruby and Rails

- Ruby 3 (2020): 

  - Ractors: lightweight concurrency

  - Fibers: cooperative multitasking

  - Type definitions and checking with RBS

  - Ruby 3x3: Ruby 3.0 is 3 times faster than Ruby 2.0 (thanks to JIT)

  - Syntax changes: pattern matching, deconstructions, …

  - …and many more changes: [Ruby Evolution](https://rubyreferences.github.io/rubychanges/evolution.html)

- Rails 7 (2021) and 8 (2024): one-man-band framework for modern web development

  - Hotwire: modern, HTML-over-the-wire approach

  - Turbo: fast, seamless navigation

<qr-code url="https://rubyreferences.github.io/rubychanges/evolution.html" caption="Ruby Evolution" class="w-36 absolute bottom-148px right-60px" />

---

## Present day

Ruby is still a great language for new startups:

<a href="https://evilmartians.com/chronicles/startups-on-rails-in-2024-my-keynote-at-railsconf">
<img src="https://evilmartians.com/social-cards/chronicles/startups-on-rails-in-2024-my-keynote-at-railsconf.jpg" alt="Startups on Rails in 2024" class="block object-contain text-center m-auto max-h-80 mt-20 w-full" />
</a>

<qr-code url="https://evilmartians.com/chronicles/startups-on-rails-in-2024-my-keynote-at-railsconf" caption="Startups on Rails in 2024" class="w-36 absolute bottom-48px right-60px" />

---
layout: cover
---

# Ruby in Japan

How Ruby is different in Japan compared to the rest of the world?

---
class: annotated-list
---

## Is Ruby popular in Japan?

<div class="grid grid-cols-[50%_50%] gap-4">

<div>

### Yes…

 - Every 10th Ruby developer is in Japan[^1]

 - Biggest Ruby conferences are in Japan

   RubyKaigi: 1500+ attendees in 2024

   Kaigi on Rails: 700+ attendees in 2024

 - And a lot of regional Ruby conferences and meetups
</div>
<div>

### but

 - Ruby is behind Python, Java, and Go[^2]

   Ranked 8th in popularity (21th worldwide by [TIOBE](https://www.tiobe.com/tiobe-index/))

 - And isn't highest paid one too

   With salaries ranked 9th from ¥4.1M per year

</div>
</div>

[^1]: https://www.jetbrains.com/lp/devecosystem-2023/ruby/
[^2]: https://www.tokhimo.com/post/popular-programming-languages-in-japan-2022-1

---
class: annotated-list
---

## Ruby in Japanese companies

- [Cookpad](https://cookpad.com/) – recipe sharing platform

- [SmartHR](https://smarthr.jp) – HR platform

- [Money Forward](https://moneyforward.com) – personal finance management

- [RIZAP](https://www.rizap.jp) – unmanned gyms [chocoZAP](https://chocozap.jp/)

- [ANDPAD](https://andpad.co.jp) – construction management platform

- [Timee](https://timee.co.jp) – scheduling platform for gig workers

- [STORES](https://stores.fun/) – e-commerce platform

- [Qiita](https://qiita.com) - tech blogging platform

- [KOMOJU](https://komoju.com) – payment gateway for cross-border e-commerce

<qr-code url="https://rubykaigi.org/2025/sponsors/" caption="RubyKaigi sponsors" class="w-36 absolute bottom-48px right-60px" />

<!--
Just take a look at sponsor list for [RubyKaigi](https://rubykaigi.org/2025/sponsors/) and [Kaigi on Rails](https://kaigionrails.org/2024/sponsors/)!
-->
---
class: annotated-list
---

## Ruby usage diversity in Japan

Not only web development!

 - mRuby for embedded systems
 
   From keyboards ([KeebKaigi](https://keebkaigi.org)) to satellites

 - Popular for educational purposes 
 
   Often taught in schools and universities.
   
   Also [SmalRuby](https://smalruby.app) – visual Ruby programming for kids.

 - Collaborations with government

   E.g. [Ruby City MATSUE](https://www.city.matsue.lg.jp/sangyo_business/sangyoshinko/RubyCityMATSUE/index.html)

---
layout: two-cols-header
class: annotated-list
---

# Let's go Ruby?

::left::

Read books and docs:

- [Ruby Quickstart](https://www.ruby-lang.org/en/documentation/quickstart/) on the official site

  and [in-browser Ruby Playground](https://try.ruby-lang.org) 

- [Programming Ruby](https://pragprog.com/titles/ruby5/programming-ruby-3-3-5th-edition/) aka “Pickaxe book”

- [Agile Web Development with Rails](https://pragprog.com/titles/rails8/agile-web-development-with-rails-8/)

- [Practical Object-Oriented Design Ruby](https://www.poodr.com)

- [Layered design for RoR applications](https://www.packtpub.com/en-us/product/layered-design-for-ruby-on-rails-applications-9781801813785)

  Martian book with recipes for growing apps

- [Ruby under a microscope](https://patshaughnessy.net/ruby-under-a-microscope)

  for in-depth understanding of how Ruby works


::right::

Attend meetups and conferences:

  - [RubyKaigi](https://rubykaigi.org)
  - [Kaigi on Rails](https://kaigionrails.org)

And local ones too!

  - [Kyobashi.rb](https://kyobashirb.connpass.com) meetup
  - [Kansai RubyKaigi #08](https://regional.rubykaigi.org/kansai08/) conference
  - [Naniwa.rb](https://naniwarb.doorkeeper.jp/) meetup
  - [Ruby Tuesday](https://ruby-tuesday.doorkeeper.jp/) meetup (usually online)
  - … (that list isn't exhaustive!)

<!-- Meet-ups are on Japanese of course -->

---
layout: cover
---

# Thank you!

<div class="grid grid-cols-[8rem_3fr_4fr] mt-3 gap-2">

<div class="justify-self-start">
<img alt="Andrey Novikov" src="https://secure.gravatar.com/avatar/d0e95abdd0aed671ebd0920c16d393d4?s=512" class="w-32 h-32 object-contain" />
</div>

<ul class="list-none">
<li><a href="https://github.com/Envek"><logos-github-icon class="dark:invert" /> @Envek</a></li>
<li><a href="https://twitter.com/Envek"><logos-twitter /> @Envek</a></li>
<li><a href="https://mastodon.social/@Envek"><logos-mastodon-icon /> @Envek<span class="text-sm tracking-tight">@mastodon.social</span></a></li>
<li><a href="https://bsky.app/profile/envek.bsky.social"><logos-bluesky />  @envek<span class="text-sm tracking-tight">.bsky.social</span></a></li>
</ul>

<div>
<qr-code url="https://github.com/Envek" caption="github.com/Envek" class="w-32 mt-2" />
</div>

<div class="justify-self-start">
<a href="https://evilmartians.com/"><img alt="Evil Martians" src="/images/01_Evil-Martians_Logo_v2.1_RGB.svg" class="w-32 h-32 object-contain block dark:hidden" /><img alt="Evil Martians" src="/images/02_Evil-Martians_Logo_v2.1_RGB_for-Dark-BG.svg" class="w-32 h-32 object-contain hidden dark:block" /></a>
</div>

<div>

- <logos-github-icon class="dark:invert" /> [@evilmartians](https://github.com/evilmartians?utm_source=owddm&utm_medium=slides&utm_campaign=ruby-in-japan-vs-world)
- <logos-twitter /> [@evilmartians](https://twitter.com/evilmartians/?utm_source=owddm&utm_medium=slides&utm_campaign=ruby-in-japan-vs-world)
- <logos-mastodon-icon /> [@evilmartians<span class="text-sm tracking-tight">@mastodon.social</span>](https://mastodon.social/@evilmartians?utm_source=owddm&utm_medium=slides&utm_campaign=ruby-in-japan-vs-world)
- <logos-bluesky /> [@evilmartians.com](https://bsky.app/profile/evilmartians.com?utm_source=owddm&utm_medium=slides&utm_campaign=ruby-in-japan-vs-world)
</div>

<div>
<qr-code url="https://evilmartians.com/" caption="evilmartians.com" class="w-32 my-2" />
</div>

<div class="col-span-3">

Our awesome blog: <span v-mark.orange class="font-bold">[evilmartians.com/chronicles](https://evilmartians.com/chronicles/?utm_source=owddm&utm_medium=slides&utm_campaign=ruby-in-japan-vs-world)</span>!

These slides are here: [envek.github.io/owddm-ruby-in-japan-vs-world](https://envek.github.io/owddm-ruby-in-japan-vs-world/)

<PoweredBySlidev absolute right-10 bottom-23 text />

<qr-code url="https://envek.github.io/owddm-ruby-in-japan-vs-world/" caption="Slides are here" class="w-50 absolute bottom-200px right-40px" />

</div>
</div>

<style>
  h1 { margin-bottom: 0; }
  ul a { border-bottom: none !important; }
  ul { list-style-type: none !important; }
  ul li { margin-left: 0; padding-left: 0; }
  p { margin-top: 0; }
</style>
