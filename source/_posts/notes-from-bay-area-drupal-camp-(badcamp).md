title: Notes from Bay Area Drupal Camp (BADcamp)
date: 2013-10-30 03:59:24
tags:
- BADcamp
- drupal
- cms
- php
- software
- unconference
- open source
- community
- share
- talks
---

## Non-Profit Summit

Came in late. Marsh Arts Center in Berkeley has terrible wifi service for an event where apparently some folks want to be connected to the internet.

### Tech Soup Global
Caught the post-lunch keynote, 30 min talk. Pretty interesting hearing about the work of a progressive team inside of a large global non-profit. In sum, if you believe you can deliver, push ahead and build the world you want to work in, even if it rides against the stream.

Really interesting content, slides are perfect notes for this circumstance, will link here. 

### CRM breakout

*Metaphor for CRM:* it is like writing an outline for a novel&mdash;enough detail, but not too much.

Recommend: build the tiniest possible thing and starting to use it and help it grow.

{% blockquote %}
The most important thing about planning a CRM project is being *un-sentimental* about the organizational needs. Do not elevate 'wants' to 'needs' while also not demoting 'needs' to 'wants'.
{% endblockquote %}

Listen for moments of surprise and encourage those. Identify warning signs early and catch them ASAP, early, without being paranoid. 

Need to change from Technology Advocate to Subject-Matter Expert in your organization (recognize this).

Recognize that this stuff is only interesting to technologists / nerds, not to everyone!

!! Opportunity case: TI Alumni have this issue of older folks not needing some fancy things they see as young and unnecessary. On the other hand, they want to see what a new system will look like before pursuing it. Unofortunately, as the tech person has to say, if we could show you what it would look like&mdash;we would have built it already! SO, what is the use case?
!!! The user wants to build a *real* mock-up using an actual crm instance, [wordpress.com](http://wordpress.com/)-style. This leaves the opportunity for running a simple, blog-style CRM, then upgrading for freemium features, and ultimately to move to independent instances, development contracts, etc. 
!!! Need to investigate pantheon, aws, other drupal hosting (and cloud hosting) services to determine how to hack this with an MVP.

#### What about modularity&mdash;why drupal at all?

If you are using drupal as a brochureware, why would you bother integrating CRM? Probably you should not, unless you are doing *actual* interaction with your user, such as doing event registration, etc.

#### Technologies

* Springboard
* Blackbaud? (Convio ancestor)
* Salesforce (force.com)
* Red Hen (built FDBD, for-drupal-by-drupalers, vs civicrm)
* CiviCRM

## Bay Area Video Coalition (BAVC)

Jennifer Gilmen and Mark Hellar.

Community center in San Francisco. Support independent media, including a public access tv station&mdash;which motivated the move to drupal in the first place some years ago.

Center of Investigative Reporting \& them are interested in measuring impact.

Part of documentary filmmaker coop called New Day Films, want to use drupal + salesforce, etc.

At the center of quite a number of different kinds of orgs. From cities to youth programs, independent producers, public meda, companies, etc.

Bid on SF public access TV station some years ago. AT\&T rigged the laws to choke major city contracts for public access. Funding was going down to $170,000 / year, which is nothing! Not much to support all the good work they were doing there already.

Wanted to provide a lot of functionality for the public broadcast station, was possible due to work from the  Denver Open Media project. Needs more development!!! Contact them.

!! Side-note... It seems like the advantage of the html5 side of the web is that folks can access the full stack of the application and can therefore reproduce issues and do bug-fixing. However, when you have server-side software, there is a limitation to reproduce the same applications in order to actually work on them in the abstract. Some systems try to address this in some fashion that allow you to more closely reproduce the sites and applications *as they may exist in the wild* but usually it is a pain in the ass! E.g. django has fixtures, drupal has site archetypes (erg, what is the technical name for this?).
!!! So how to fix this? Unclear, is there a standard or simple way to make your site, private, safe, yet clonable?

Lots of discussion of webforms and integrating with salseforce using springboard. This is boring. Is this really the state of the art on the web for independent and public media coalitions? What is the next-generation of this type of work?

Honky-dory that program folks can interoperate with this system fairly elegantly&mdash;the state of the art is perhaps (not restricted but) shaped by the use of folks who are going to be implenenting programs and working on services provided by non-profits, etc.

* Perhaps it is /using/ data, visualizing it, and allowing *complex interaction*. 
    * What does "complex interaction" look like? 
        * doing lots of things with the data, storing states, allowing it to interoperate with other sources and services, being able to share and then build a review/comment layer on top of this.
    * This is perhaps why I am very interested in using drupal as a back-end to some javascript engines like knockout.js.

BAVC has a program for documentary filmmakers to publish and share content, which automatically gets archived in the internet archive&mdash;stored in "Community Media" archive.

Ideally, folks should be able to upload content to their local library, ship it to BAVC, publish to the website, and archive it with Internet Archive&mdash;*automagically*.

Created a website for city and county of San Francisco, [GoConnectSF](http://goconnectsf.org/) with youth center digital filmmaking programs.

If you want to see code email markh@bavc.org, for programs, email jennifer@bavc.org.

## Drupal 8 Security

Presentation formatted in Ubuntu font ;)

Drupal.org acts as a security gateway to drupal modules, but as modules move to github/etc, we'll see the security landscape.

Examples of systems having their repositories compromised in the last couple of years:

### Versioning

* FreeBSD compromised with third-party packages in conversion between cvs to subversion.
    * Took a while to find out what had been changed due to central cvs control mechanism
* Linux Kernel: This happened a few years ago to Linux as well
    * Luckily, with git it was relatively easier to determine if something had been tampered with

### API
Drupal - Uses PHP, Procedural hook system > modularity: PSR/Symfony (paradigm)

* Emphasis for Drupal is to put more emphasis on the Services module, need to keep eye on REST security moving forward.
* Comparative examples outline differences

### Django vs. Drupal
"The fact that Django is so object-oriented inherently reduces th epotential for vulnerabilities (even by mistake) that are often seen in other procedural code because data will typically travel through a single common layer (or class) whereby data can be cleaned, security checks conducted, etc."

Movement to Object Oriented model in Drupal 8, as part of a move to professionalize PHP.

Speaker: "Often compared to a field of Anarchy, where things act their own way."

* php == "anarchy"

Lookup: "PHP: The Right Way", www.php-fig.org

Dries Buytaert article on PHP over Java for Drupal

* More approachable for amateur programmers.
* Also, audience of Drupal did not include conservative bodies like Governments
    * However, since, these adopters have come.
* Opportunity to standardize and professionalize the application, without becoming rigid.

### API Security
All have methods for filtering dangerous content.

* Drupal
    * Filters on output rather than input! Same as WordPress, unlike others
    * Input filters (t(), check_plain, filter_xss, db_query); entities; form tokens; autho cookies; password hashing & salting (SHA512), Twig
    * Twig is a new Drupal 8 templating framework&mdash;a dangerous attack vector.
        * US Government found that majority of security vulnerabilities live in templates!
    * Some good database abstraction which sort of serves as an ORM.
* WordPress
    * Filters (wp_filter_kses(), $wpdb)

### Security Management

Drupal has the most active security infrastructure, especially comparative to WordPress.

* Security Team exists to:
    * Resolve issues
    * Assist module maintainers
    * Documentation
    * Responsible disclosure
    * Secure coding guide
    * Provide full project review for drupal.org modules. (this security vector).
        * Seems like it's possible to resolve this "github" issue by piping endpoints.
* WordPress
    * Does have a security team, but they take a background role
    * Many folks seeking to do security for work
    * Don't set up monitoring, but they stop the hackers pre-emptively.

!Idea: Java vs. PHP: Security Implications of Language Choice for Web Applications - James Walden (Northern Kentucky University). 

* [freshmeat.net](http://freshmeat.net)

A lot of focus over the years on WordPress plugins

* 20% of top plugins, including majority of ecommerce plugins had serious vulnerabilities
    * Researchers found that open source community did not take responsibility for security of community developments.

### Community Comparison

Essentially, there are trade-offs between platforms from a security perspective, e.g. "ease of use" versus centralized management.

### Security Issue: Drupal Core

Some Recent Vulnerabilities

Drupal:

* Image module
    * Not checking whether a valid token was used to create an image derivative (could create on the fly, execute a DoS attack)
* Context module
    * Not a sufficient check whether you had access&mdash;could gain access.

WordPress

* eCommerce plugin
    * Many issues with XSS
    * insufficient level of content filtering with wp_kses_post()
    * In another point, had not checked for proper permissions to allow only ordering of published items.

### Compliance

FISMA, standards for government bodies

PCI, credit card standards

Lots of toggles to form compliance:

### Roles & Permissions

Drupal:

* Very granular, but very complex that can generate vulnerabilities
* However, this is possible to manage better with OA and WorkBench modules.

WordPress has more separation of administrative layer.

### Federated Identity & Multi-Factor Authentication

Drupal

* OpenID, OAuth, LDAP, Google Authenticator, TFA/SmS, YubiKey, Duo, wikid, SAML: NIH Login, CAS,: OMB MAX, PIV
* Features expanding for authentication
* SAML and CAS are secure authentication protocols for many government agencies.

### Vulnerability Assessment

Drupal

* security review, coder/secure code review, dpscan, security scanner

### Hardening

Drupal

* Hardened Drupal, Guardr, Paranoia
    * Guardr install profile activiates many helpful
    * Acquia maintains a great overview of security modules with Drupal Scout

WordPress

* Integrated security plugins (Better WPSecurity, BulletProof Security), Secure WordPress.A

### Continuous Monitoring

* By default, you often get a wealth of data which is difficult to filter
* Collecting lots of data, but watching the important stuff allows capability of reducing threats and addressing attacks.
w 
* A lot of security modules are at a nascent stage.


### Hosting Platforms and Environment

Drupal

* LAMP: Apache/Nginx/IIs, Mysql/Maria/PostgreSQL/MSSQL/Oracle, PHP 5.3
* Follow fork to MariaDB
    * Oracle was becoming less transparent in terms of security

### Drupal.org Security Incident

* Breach of drupal.org, compromised
* Had to reset passwords
* Third-party software breached: undisclosed
* With drupal, you never walk alone.
    * Depending on Apache, Cash, Chef, Solar, Maria, Linux, etc.

### Security Ninja

* Only possibly by effectively understanding the other components to become a *Security Rockstar*!


## Why users are irrational and what we can do about it

### Heuristics
"Ferrari drivers are erratic, look out!"

Help us make decisions really quickly -- "rules of thumb" 

### Cognitive Biases

When we have a heuristic that is in some fashion illogical or erroneous

#### Example

Different ways of displaying the expanded form of 9! yields different incorrect results

* Starting with 1 gives ~500
* Starting with 9 gives ~4200
* Total is ~ 36,000?

Humans have a bias toward initial data for instance.

#### Inspirational White Dudes

* Khaneman
* Tversky
* Thaler
* Slovic
* Arielly
    * More down-to-earth, also good TED talks on irrationality

Do we trust these folks? They are pioneers in psychology, which is convenient since there are supposedly controlled empirical experiments

* Pioneers of usability research /before/ it existed.

Many Biases

#### Common Types

* Confirmation bias
    * Will gravitate to data that confirms existing beliefs
    * Ex: searching for "the right solution" online can simply yield the same /incorrect/ solution
        * Designers also say, 51% are better (but is there really significance?) often in usability testing
        * Careful of body language to encourage confirmation (leaning in with a tester)
    * Approaches
        * Provide answers, not raw data; provide anecdotes, not statistics; observe users not metrics
* Congruence bias
    * People rely on direct hypothesis testing rather than indirect testing.
    * Drupal is a perfect example of this bias. There are many ways to do things, surprising sometimes.
    * Surveyed all the customers, so therefore this is what we should do (but what about the other users?)
    * Designers don't look outside of the sphere of work (pick between 3 options--but what about outside the scope?)
    * Approaches
        * Keep eyes out for strange pathways, unnecessary solutions
        * Encourage stakeholders to broaden the base, compare against competitors and similar products, look cross-industry
        * Designers should test against competition, not within merely available options
* Curse of Knowledge
    * !RAMPANT in the Drupal community
    * Assume huge amounts of knowledge for the users for language and nomenclature
        * Not everyone knows what a *node* is!
    * Assumption that search box is always in upper right corner
    * Language like "boolean, float, integer" for fields UI&mdash;really inaccessible vocabulary
    * Designers may adopt "new icons" or new images, but is it necessarily understandable to your user?
        * Be careful venturing out into new territory, at least use some other affordance to encourage users to break pattern
    * Approaches
        * Users should use ubiquitous patterns wherever possible
        * Use video to capture contextual inquiry to put usage in perspective
        * Test patterns you already consider "established"
* Illusion of Correlation
    * Misinterpreting coincidental events for causal relationships.
    * Users explain that one action necessarily generates another response, but may not be the case.
    * Seeing sales or traffic go down after launch of new site&mdash;maybe there are other factors
    * Changing the design and finding that it tests more poorly.
    * Approaches
        * Ensure feedback is limited to the user's task to allow them to construct causal relations where appropriate, and not the opposite
        * Focus the question. Sales went down, but what else happened, what was going on?
        * Designers should limit the variables to ensure less convolution.
* Loss Aversion
    * Folks strongly prefer avoiding losses over acquiring gains
    * Another, sub-bias is: memory of pleasant events fades quickly, versus unpleasant fading slowly.
    * Users may feel connected to things they have made, don't want to lose them
    * Stakeholders don't want to feel like they've wasted investment by throwing code away.
        * aka "Sunk Cost Fallacy" - spent all this time working on it, so the newness "loses" all that previous investment.
        * The issue with this is not asessing the development in the context of time, that overall there are opportunities to build new things that will take less times.
        * !"Your only have the future, the past doesn't exist!"
    * Designers get stuck to carefully-crafted elements (e.g. skeumorphic button) that add unnecessary dependency
        * Emotional attachment, rather than ephemeral things
    * Approaches
        * Can use loss aversion in ethical and transparent ways to drive stickiness
        * Encourage stakeholders to assess future costs, rather than only past cost
        * Designers need a Zen approach to have emotional detachment&mdash;move on, create something new.
* [List of Cognitive Biases](http://en.wikipedia.org/wiki/List_of_Cognitive_Biases)
    * Many more!

!Anchors can encourage the user to make a choice that seems reasonable in context, rather than actual cost and value (e.g. three options, middle highlighted). 

#### Ethical Considerations

* may not be illegal or necessarily wrong, but it could be unethical.
* Check out the [](Dark Patterns Library):
    * Already opted-in to receiving spam emails after signing up for something.
    * This has been used for good&mdash;organ donors in Europe, opt-out system.
    * Way more organs available in Europe

! Metric: Consider whether your use of biases, patterns, etc in a way that is aligned with the needs of your user.

### Design Patterns
Acquia is assembling a design patterns document. One of them:

* I'm worthy of your trust
    * I say what I mean and I do what I say. It's not in my nature to trick, conceal, handwave, or manipulate. My success is directly aligned with yours and your good opinion is invaluable

### Questions

Sunk-Cost Fallacy Strategies

* Do an actual calculation of support cost
* However, another cognitive bias to frustrate this
    * Folks have a tendency to value near-term costs over long-term costs. 


## Data Management Applications with Drupal as your Framework

!Tripal - Genomics in Drupal

* Generic Model Organism Database - DB schema

Kept building data apps, so eventually decided to make it more modular, reusable.

Saw drupal, has nice features:

* User, roles, auth
* Forms, data handling, etc

### Data development

Chose to write data application without CCK, so this is all in code.

* Existing built-in schema update and <code>drush make</code>
* Data source/uplink:
    * Links to outside data sources with financial info and academic data
* Upload/import w/ cron and batch
* Create read-only data mirrors

Chose drupal to make highly modular design

Use case requires granular access control for each module

Can have as many or few roles as you need, granular permissions

In terms of content access, can use built-in realms and grants

Uses Content and Forms features to develop platform

Advantage of Drupal is "aspect-oriented" paradigm rather than MVC

* Flexibility is integral, things change on a regular term
* The module handles everything concerning the particular aspect
    * The alumni module handles the fields, the submission, form handling, etc.
* Usage of hooks (actions) as callbacks through the standard process

## Demo Framework

Keeping it simple, this is fairly simple (though lengthy) install:

[Demo Framework](https://drupal.org/project/df)

This is a way to showcase a site to potential customers quickly, not just describe drupal features.

Acquia is behind it, but committed to community involvement and open source--it already is open source.

To work with a client, ended up developing a new use case for a proper, thinner framework based on DF for sites:

[Lightning](https://drupal.org/project/lightning)

!Basically, as far as I can tell, this project is a low-level closely drupal-integrated solution for making a data application


## Project Prophylaxis

A *prophylactic* is a mechanism to prevent the transmission of disease.

*Practicing Project Prophylaxis* is the practice of using legally protectie measures when working with clients by contract.

### Exposed

You can feel exposed as a developer, designer, engineer, or even member of a new business.

Crowd is mostly shop owners / directors. A few contractors. One "other".

### Client Relationship

Consider the relationship through the entire lifecycle of the process.

> *Choose clients wisely*

Tips:

* Know your skills / comfort zone
* Align personalities / mission
* Understand what success looks like
** Have metrics for success?

Often, go through discovery phase, work on spec (for pay), allow room for alternative vendors.
> *Interestingly, this is never the case.*

If you're crafting a contract, you'll be agreeing to deliverables. Discovery phase gives a chance to get a feel for client and scope.
> All those present are agile, so this is a consistent process

**Q:** How detailed is that spec?

**A:** Depends. Outline as:

* UX Artefacts
* WireFrames
* Assets
* Tech Strategy
* Information / content

Use a boiler plate contract that effectively agrees that the client will pay. The deliverables are specified out in particular. Some use a time & materials contract--hourly work, in good faith in estimates, but the client can derail at any time with crazy requests. If you're not really strict about that you can run through their budget with half a project. This is important for your record. You may be legally protected, but you have a business obligation to right somehow.

The message here:

> *There's a lot of gray area*

Every client is different, need to foster the relationship while also using the same protections across.

### Negotiation and contracts

Scopes of Work can be 20 pages long! These aren't necessary, detestable. As long as you have an understanding going forward, not everything has to be in the Scope of Work, you'll have good legal protection.

A good lawyer is going to write a boilerplate contract in your best favor. When you go in to signing someone else's contract, be aware that they want to have an edge, have terms that are in their favor.

* Negotiation tips:
    * Confidence
        * Most clients feel like they're being wrong or mean, have to be comfortable being matter-of-fact. Ask for stuff, and say "No".
    * Strawmen
        * Talk to someone else to get feedback in the middle of a negotiation
    * Advocates
        * Most important factor&mdash;need to connect with your advocate to make it through e.g. "procurement"
* Battle of the Forms:
    * Proposals, SOWs, MSAs, POs, yadda yadda...
    * Be careful because MSA language may supercede SOW terms about when/how to get paid.
    * Do search for "indemn" strike out indemnification against you.
    * Also warranties and representations
    * Don't assign rights of your toolkit to the client! (Careful of the "open source" clauses)
* Contract Basics
    * Money (Approvals and satisfaction), liability (reps/warranties and indemnity), and Rights (don't "assign" your toolkit
* Money
    * "Posession is 9/10ths of th elaw."

Majority of Gabe's clients are using fixed-pay. Number one concern is scope creep versus milestone and deliverable. Some of his biggest clients use fairly generic language.

Be careful of acceptance statements and satisfaction language.
> "Full discretion" besides "reasonable discretion"?

Difference between a SOW and Terms&mdash;the simplicity of individual words like "sole"

### Getting it Done

* Discover and set expectations: communication, risks, requirements
* Meet expectations: Build it well, product reviews
* Manage expectations: status, scope control
* Invoice early and often
* Be consistent, proactive, and reinforce value
* Write it down.

Metaphor: the same way you pay attention to your servers you should pay attention to your contracts&mdash;you can get hacked.

Agreeing to it in writing&mdash;*you've got a contract!*

!Arbitration can be *gamed*
> Example: one of Gabe's clients had a client that extended the cost quite a bit, making it expensive.

**BIG LEVER:** Put an attorney's fees clause in the contract, so you can argue for $30k-$40k contracts.

### Clients Gone Wild

* Challenge: protecting clients from themselves--stakes are high!
* Contracts in Agile work, when to use change order? SOW?
* Manage expectations while protecting yourself in T&M: keep focused on MVP and remember your backlog
    * Can use the backlog as a good metaphor and communications tool with clients. Use this feedback speedily!
* Stay strong
* Non-payments, silent treatment, rude behavior

### Firing Clients

Trying to be **partners** with all of your clients, on the *survivor island*.

When there is **animosity** get away as fast as you can.

!Know what **indemnity** means! Pay your lawyer some money now to save you tons later!

### Conclusion

* Choose your clients with discretion
* Always wear a contract
* Make sure it fits
* Foster the relationship
* Be the stable one
* Communicate

If you have to... __*Walk Away*__
