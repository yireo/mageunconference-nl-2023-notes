# MageUnconference NL 2023 notes

## Session: How to deal with Upgrades of Magneto - Jeffrey - Experius | part of Happy Horizon
**Notes by Jeroen Vermeulen, additional notes Luke Collymore**

Why
- [ ] Essential for security, you are responsible for keeping your customers data secure
- [ ] Do it regularly like your car's maintenance!
- [ ] Gain performance increases from PHP, MySql etc upgrades
- [ ] Regular smaller upgrades can cost less overall then larger multi version upgrades
- [ ] Servers won't support older versions of software


How - Sell / Invoice
- [ ] Sell customers a Package of hours, do upgrades from the package
- [ ] Offer a monthly subscription, if customers don't do it you will have a big upgrade in the future which will be more expensive then all small upgrades combined.
- [ ] Put it in the contract already
- [ ] Tie the upgrades to other benefits
- [ ] Scare customers what happens when you don't upgrade by telling worst case scenario stories
- [ ] 2.4.3 => 2.4.6 estimated 40 hours
- [ ] Security updates 8-16 hours
- [ ] Don't accept existing shops with a lot of legacy
- [ ] Budget for 4 quarterly releases and at least one security patches
- [ ] Consider creating dedicated upgrade teams


How - Technical
- [ ] Only security patches is an option
- [ ] After a new release wait for P1 first
- [ ] In composer.json put everything on *, see what happens
- [ ] CI/CD bot which checks all modules of customers if they are compatible to determine impact
- [ ] Dashboard with all modules of customers + state of compatibility
- [ ] Use PWA (GraphQL+NextJS) the lower impact of upgrades
- [ ] Share more components among customers
- [ ] Watch out for missing authorisation keys needed to receive the latest version of a module. Especially when you did not buy the module yourself.
- [ ] Make an inventory first, check manually for each module what the latest version is compatible with
- [ ] OTAP Street, Internal manual testing. Work out test scenario's
- [ ] DI Compile first, Static code testing


Problems when upgrading
- [ ] 3rd party modules can cause problems
- [ ] Breaking changes from tech stack PHP, ES etc upgrades
- [ ] Customisations via bespoke modules and templates overrides
- [ ] Consider waiting on -p1 patch release to miss initial bugs after upgrade release


Automated testing tools
 - [ ] [Ampersand Upgrade Helper - (step 1)](https://github.com/AmpersandHQ/ampersand-magento2-upgrade-patch-helper)
 - [ ] [Elgentos Upgrade GUI - (step 2)](https://github.com/elgentos/magento2-upgrade-gui)
 - [ ] [Rector - Instant PHP Upgrades and Automated Refactoring](https://github.com/rectorphp/rector)
 - [ ] [PHPStan - Bitexpert](https://github.com/bitExpert/phpstan-magento)
 - [ ] [PHPCS - Magento Coding Standard](https://github.com/magento/magento-coding-standard)	

 
Manual testing steps
 - [ ] Use all features of the site as a customer
 - [ ] Developer and Internal testing is important
 - [ ] Test scenarios should be well planned out 
 - [ ] Perform Cross device/platform testing

# How we got a 99 PageSpeed score (Tjitse Efdé - Vendic)
**Notes by Jeroen Vermeulen**

- Ignore Desktop in PageSpeed, only pay attention to Mobile
- Use Hyvä
- Only load stuff you really need it
    - For example load the the Soakr stuff only when the user starts typing in the search box
    - If you have a chat, show a facade (fake) chat first. When the user clicks load the real chat
    - Below the fold load everything lazy
    - SVG small icons inline
    - Hyvä has the event 'init-external-events'
        - Load Tag Manager, Analytics assets etc only when the user interacts with the page 
        - Alternative: Load GTM at start but use 'init-external-events' to trigger an event to load things like HotJar etc
    - Use native image lazy loading
- Only load what is in view 
- Lazy load big images
- Don't load any external CSS
- Replace company review ratings etc by static cached versions
- Mainly optimise homepage, categories, product pages
- Optimise from the start of the project
- The client needs to work with you, you can't just drop in external elements
- Run ImgProxy as a Microservice can resize images + convert to WebP
    - Fruitcake Magento2-Custom-Image-URL to replace image URLs
- Varnish cache
- Optimise PHP using New Relic in production
    - Find bottlenecks like Load In The Loop
- Vendic does host its sites with Savvii.com and runs HaProxy, Varnish, ImgProxy there
- Always serve fonts from your own server, not from Google
- Reduce the items in DOM, keep below 1500 items
    - Lazy load hidden nodes - keep SEO in mind
    - Alpine X-Intersect plugin triggers when a part is in view. 
    - Alpine X-If plugin

# The future of Magento - Dennis: Magento 3.0: The future of Magneto
**Notes by Jeroen Vermeulen**

Niek Verkoelen - Vendic: What is currently the most important thing in the ecosystem in Magento

Current State
- It would be very hard for Magento to drop Luma because they already had all vendors invest in PWA Studio while dropping it afterwards
- Magento is for customers who don't fit in Shopify, for bigger shops or customers with more custom needs.

Magento 3.0
- Based on PHP it is very extensible
- Open Source
- A minimal Magento
- Something like Symphony Maker Bundle. Start wit minimal environment instead of with everything.
- Less bloated
- Composable
- Generate code like Laravel Artisan Console
- Self hosted
- Microservices? => does it 
- A possibility for startups
- Keep a big ecosystem
- We cannot change everything and keep the ecosystem compatible

Do we see a future with Magento 3.0 under Adobe?
- Looks like Adobe does not seem have a clear vision
- They lost the community because of them pushing their services 
- Adobe is a subscription company, not likely they will release Magento 3.0

ShopWare
- More practical CMS
- Flow Builder for marketing automation
- API first
- Smaller ecosystem

Shopify and other SAAS
- Everything is determined by one party
- Very limited freedom


# Magento vs Mage-OS - Thomas - Creativity
**Notes by Jeroen Vermeulen**

- The future of Magento Open Source, Mage-OS, Adobe Commerce?
- How can we contribute to Magento, make it better?
- Can things co-exist?

- The target of Adobe Commerce is quite different
- It may be a problem Mage-OS deviates too much from Magento Open Source gets too big, will not be possible to use each other's code.
- It looks like Adobe is not taking very much care of Magento Open Source. Mage-OS gives us an insurance policy we are able to continue improvement.
- Adobe is creating services for everything
- Adobe bought Magento for its enterprise customers
- How can we make Mage-OS thrive and 
- Mage-OS can be a kind of extension to Magento Open Source. It is not the purpose to replace Magento Open Source.
- Maybe Mage-OS can be the innovative side, like Fedora is for Red Hat Linux
- Adobe Commerce has lots of B2B features like company roles, approval of orders, company catalog etc.
- Content staging is also a big feature of Adobe Commerce, which is quite a change because it makes the database work totally different

# DDev - Gerard
**Notes by Jeroen Vermeulen**

- Like Docker compose but with a preconfigured recipe. 
- The community provides a lot of configurations.
- Code base is mounted (Windows) or synchronised (Mac).
- OrbStack: Alternative to Docker Desktop, fixes problems with slow Docker containers on Mac.
- Alternative: Warden.io 
- When you update a container you can push it to Docker Hub or GitLab
- Buildpack is a tool to separate building and running images, so running images are smaller
- You can Scaffold to build Docker containers and push them into Kubernetes
- In PhpStorm you can commit a config with configuration for PhpStan etc

# Notes by Francis Gallagher
This was the service I mentioned: https://noibu.com/

Just dont put faith in their loss calculations. 

Secondly mentioned was the issue about the core problem that can stop high traffic real blue green deployments or just make a bad day worse (Indexer switches from Scheduled > On Save > Scheduled) 

Problem: https://github.com/magento/magento2/issues/33386

Helpful module:  https://github.com/pykettk/module-indexer-deploy-config (Not a fix, just helps ensure indexes go back to how you want them)

Just as it came up again. If you hit this and just want to get by it have a look at vendor/magento/module-indexer/Setup/Recurring.php near the end the unsub/sub line on

https://github.com/magento/magento2/blob/2.4-develop/app/code/Magento/Indexer/Setup/Recurring.php#L124

How you stop that is up to you, you can just temporarily comment it out but you must understand what it does first so you know why and when you can't get away with it.

# Notes by Nils Preuss
https://mageless.maxcluster-demo.netz98.org/ this is the demo of mageless I promised the people in the mageless talk yesterday. As it is something brought up tonight it could be not fully correctly working. Afaik filters are the only thing broken currently there.
Everything running on a small max cluster instance.

# GitHub Copilot
**Notes by Jeroen Vermeulen**

- It is very useful when you have to write predicable code
- Gives inspiration how to solve a problem 
- Type a bit, wait a couple of seconds, it starts suggesting
- Works like autocomplete, but smarter
- Use proper class/function/variable names
- It helps to start with comments (PhpDoc) then the coPilot works better
- Sometimes it produces crap
- The more well structured your project is (Magento is crap) the better it works
- It is connected to your Github account, it can access everything you can like your own projects, open source etc
- When you use it for a longer time it understands you betters
- Works in VS Code, PhpStorm and VI
- There is a sidebar panel where you can see different suggestions and you can choose
- When you want to refactor a block of code there are other AI plugins for that
- ChatGPT is great for boilerplate work, can create the structure of a new module
- ChatGPT can create tests
- ChatGPT can rewrite code, even in another language. Also try Google Bard.
- Google Copilot can help you learn you (new) ways to get things done  in a language you don't know very well
- ChatGPT will generate textbook code, not always the most optimal
- ChatGPT is great for working with remote APIs
- There is a worry entry level jobs will be replaced by AI. But: Every time language got more high level there was a


# CLI Tools
**Notes by Jeroen Vermeulen**

- ZSH custom folder for snippets
- Manage your aliases etc in a private Github repo
- 'ChezMoi.io' to share dot files among environments 
- 'Terminator' or 'Byobu' to split screen etc instead of tabs, or just use iTerm
- 'AutoJump' remembers where you go in shell and 'cd' to that folder with the 'j' command
- 'TheFuck' fixes your last command with generative AI the 'fuck' command
- LogTop to keep logging on top 
- FuzzyFinder 
- xxh-shell-zsh
- PowerLevel10K ZSH Theme
- ZSH ah my zshell 
- Fish shell
- When you forgot to use screen: press Ctrl-Z; then run `disown`
- Htop can pause and unpause processes
- 'Pkill -f' to kill a process based on the whole command line
- Commandlinefu.com 
- In VS Code and Code With Me you live share a terminal with some else
- Github Copilot for CLI, there is a waitinglist to join
- OpenCommit: GPT writes commit messages for you
- WhatTheCommit.com
- https://gogh-co.github.io/Gogh/ can switch terminal colours and adapt automatically

# Notes by Sean van Zuidam
If you're interested in learning more about design tokens in TailwindCSS config, here are the links to the tools I showed:
- https://www.figma.com/community/plugin/843461159747178978/Tokens-Studio-for-Figma-(Figma-Tokens)
- https://github.com/mooore-digital/hyva-themes-config
- https://github.com/fylgja/tailwindcss-plugin-cssprops

# Notes by Michel Heitbrink
This is the link with tailwind examples. Created by Jesse. https://play.tailwindcss.com/Q4LMWbhL3N

# Nix - Jelle / BigBridge
**Notes by Jeroen Vermeulen**

https://nixos.org/ 

How we do our toolkit at work
- Inside their agency there were lots of different solutions for local Magento development
- Started with a Git repo with centralised configs
- Nix is whole range of tooling
- Nix is a command line tool evaluating the programming language Lix
- Derivation in Nix are a kind of package
- Nix packages are like a repository, a collection of Derivations
- When you share a Nix configuration you all get the exact same package, if your computer is the same architecture
- When you use Cloudflare DNS, you can use  \*.localhost  for development domains
- Only using aliases, no other shell magic
- NixOS is a whole OS built from scratch on the Nix principles

Onboard a new developer to a shop
- Install Nix itself, /nix directory must exist
- Install workbench, which installs Nix install Newshell
- You pull the shop from Git and run the "start" command
- PHP, NodeJS, MySQL, ElasticSearch binaries all come from Nix.
- Nix already contains lots of packages
- PHP is configured to use a sendmail which redirects everything to Mailhog

Tool 'Funky': You add a .dotfunky file in your project which helps to automatically use the right binaries.

https://github.com/rectorphp/rector
Rector can refactor code to match a newer PHP version

use this installer to get nix: 
https://github.com/DeterminateSystems/nix-installer

# Notes by Jelle Siderius
https://github.com/jellesiderius/mage-db-sync

# Notes by John O'Rourke
Hahaha!  I love learning vowel sounds in other languages, so I found the Dutch ones and made this for you:

For those who missed my "how to speak like in Liverpool" (Scouse) lesson, I worked out a guide - pronounce this the dutch way:

"o" becomes "oo"
"ck" becomes "gck"
"oo" becomes "uu"
"k" becomes "g"
"ck" becomes "ch"
"t" becomes "ttj"
"the" becomes "eu"

...but do all this with the mouth wide, if you can!

I just couldn't find a sound for "a" - it's like "aa" with the mouth wide.

So you  can say using Dutch pronounciation "luugck aatj tjeu buugck!" (look at the book)

and to the words...

"hello!" becomes "ei!"
"would you like to have a fight?" becomes "ee! ee! ee! ee! joe! autjsjeidj nau!!"

# Session: Proconcloud method
**Notes by Peter Stuifzand**

- Proconcloud method is a decision making method.
- It's based on parts of Theory of Constraints (Change Matrix).
- It helps to avoid 5 decision mistakes:
  - Waste your limited attention
    - by checking if the problem is important
  - Jumping to a solution (or blaming other people)
    - By finding pros and cons for both sides: changin and not changin
    - And also, by writing the conflict for the other people, who could be yourself)
  - Only try one solution, or use a compromise
    - Instead you try 4 different options for a win-win solution
  - Ignore valid reservation from stakeholders
    - Think of the reservations stakeholders could have and improve your solutions
    - Or ask them and let them improve your solution
  - Not learning from experience
    - Create an experiment, including your assumptions about the problem and solution
    - You can run the experiment and check these assumptions to learn for the next time

Youtube video explaining the steps:

- [Evolution of ProConCloud from Franklin's ProConList & Goldratt's ChangeMatrix](https://www.youtube.com/watch?v=ORojFlF7VDU)
- [How the ProConCloud method can help anyone make better faster decisions](https://www.youtube.com/watch?v=qZVgtIATINY)
- [Success For All 2019: DrAlanBarnard Keynote - How an App can help young people make better decisions](https://www.youtube.com/watch?v=U0gtjMQELYs)

# Session: Offsite Experiences
**Notes by Simon Sprankel**

- Teambuilding ideas:
  - Build a boat / bridge
  - Escape room
  - Snowboarding / skiing
  - Hiking
  - Cleaning up the nature / doing something for the environment
- How often do you organise an offsite?
  - Often once per year
  - Some do it quarterly on a smaller (team) level, especially when working remotely
- What do you do during the offsite?
  - Work as usual, maybe only half of the day
  - Improve internal processes
  - Work on internal tools
- Ideas
  - Invite others for a smaller part of the event: clients, partners, befriended agencies, ...
  - You might want to do it close to the office to make it easier for families
  - Invite families for the last day / last dinner
  - Share financial information during the offsite
  - For bigger companies, make sure to actively mix people / groups, so that people not always hang out with the same people
  - Do something different each year / let another team organise it every year
- Advantages, especially for management:
  - Improves creativity
  - People might talk about general issues in an easy and relaxed way with each other
  - Reduces stress (less sick days)
  - Improves the team - people build relationships with their colleagues, so that they better work together
- Frank likes Bali ;-)

# Session: Local Mage-OS User Groups
**Notes by Simon Sprankel**

- FireGento kind of served as a model for Mage-OS NL
- The dutch community pretty much fell apart, also due to the Dutchento issues
- Mage-OS NL should revive the dutch Magento / Mage-OS / Adobe Commerce community
- Currently, there are no dutch Magento meetups happening, but some want to plan them again
- In Germany, local meetups are again / still happening
- The FireGento board always wanted members to organise things, whereas members expect "the club" / the board to organise things
- Always be open as a community
- Non-profits like Mage-OS NL should facilitate the community
- Non-profits like Mage-OS NL can help with organising events via marketing, communication, support, sharing experiences, ...
- Make the community great again!



# Session: API best practices

**Notes by Lau Bannenberg**

* There doesn't seem to be an existing set of best practices for integrating external APIs in a Magento application. Let's discuss.
* An API integration has two main parts (could be separate modules, or classes in a module): a client/connection part, and a service/mapper part.
  * The client takes care of connecting to the API and executing requests. But the rest of the application doesn't directly talk to the client. The client might be so generic PHP that you could drop it into a different framework (Laravel..) mostly unchanged. The client handles infrastructural stuff like authentication, pagination and rate limit backoff/retry.
  * The service is what the rest of the application interacts with.
    * It should have an interface so that the rest of the application can expect it to always have the same methods. If something in the external API changes, the service internals change, but the rest of the Magento application doesn't have to change.
    * The service knows about which endpoints on the API to call for which particular of your business needs.
    * The service maps responses back into something your application can use. So this is mapping both into framework (Magento) and business (products, orders..) logic.
* Instead of returning some array taken from the API response, it's much better to return an actual class that implements an interface, and depend on that interface. That way the rest of the application doesn't need to know all that much about the API, and if the API changes, you don't need to go hunt through your application for every bit of code that depends on the array.
  * Call it {Api}ResultInterface for example
  * This is a pretty classic value object. In PHP 8.2 it could be a readonly class, but for backward compatibility that's maybe not ideal.
  * By defining an interface, it becomes easier to later switch to maybe an entirely different API for the data you need. The interface stays the same so the rest of your application doesn't need to change. You just need to change how you initialize your value object to map the new style data to the standard format.
* Use return types
  * Avoid mixed return types like array|string to return data or a reason why the call failed; that forces the calling code to check the data type of the returned value and just creates ugly code and bugs.
  * Nullable return types such as ?ApiResult are somewhat acceptable because PHP has good syntax for those like '??'.
  * By explicitly listing return types on your service methods, calling code knows what to expect and your static analyzer can warn you that you might get a null.
  * Throwing exceptions for failures is better than mixed return types. Try/Catch for specific exceptions can still be clean code. Put the necessary "throws" docstrings on your code to help the IDE.
  * Alternatively, you could also have a FailureResult that still obeys your general ApiResultInterface. Then you force the calling code to interrogate every Result about its status though.
  * If you're trying to get some sort of collection from the API, one way of dealing with failure is to return an empty collection, but that's still the right type, to allow graceful failure. But this risks hiding the failure.
  * There's no universal answer here, consider the tradeoffs for your project.
* You should validate data coming back from the API. Who knows what's in there.
  * Data could be corrupted
  * It could be empty (your query is fine, but nothing matches it, or you've reached the end of a paginated collection)
  * It could be malicious. You're not just saving stuff to your DB without checking right?
  * The format or type could have changed (yeah, it's an API, that *shouldn't* happen, but...)
  * If you use validator classes to validate specific data types ("Dutch post code") you might be able to DI them in and reuse them in multiple projects
* You should not rely on the API connection always working
  * The other end might be down
  * Your credentials don't work anymore
  * You're rate-limited
  * It's slower than expected
  * Always plan to fail gracefully
* Take a really long hard look at how critical this API call is. Does it really need to be blocking the execution of your main task (lots of things phoning home when you log into admin panel, causing endless loading spinning... ; marketing API calls breaking customer order placement)?
  * Make things asynchronous if you can; kick side tasks into a queue
  * If the API call is not that important, give it a short timeout and try again next opportunity
  * A call failing should never break your application
  * Short timeouts and strictly limited retry is better than trying too hard
* Observers/plugins should not do API calls, and absolutely no lengthy ones. See if you can put something in a queue instead.
* More things can be made asynchronous and optimistic than you might be used to. Amazon just registers "you placed an order" and later goes to figure out if they really have enough stock for everyone that was ordering at the same time, and sends an apology if it doesn't work.
  * Asynchronous order placement is more and more possible in Magento+. Adyen is working on some exciting stuff.
* Throwing exceptions is okay, but they should be specific.
  * Use meaningful exception types and messages. No "Something went wrong" generic \Exception. Throwing a \ApiClient\ApiTimedOutException("Timed out after 10 seconds") is much more meaningful.
  * Using specific (custom) exception types enables catching specific exceptions you know how to handle.
* Logging is important but must be done carefully
  * Include all the information you need to actually diagnose an issue. Not "Could not find the product" but "Could not find product with ID X".
  * But must not be indiscriminate. Don't dump the entire response because it might include sensitive data (auth, personal information).
  * If you really have to, you can, but not on production. And if you have to on production, you should set up good filters to remove PI data. But it's hard to know for sure you covered every possibility. This is why Adyen has been removing a lot of logging actually.