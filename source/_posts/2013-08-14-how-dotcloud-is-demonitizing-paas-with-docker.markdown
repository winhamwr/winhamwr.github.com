---
layout: post
title: "How dotCloud Is Demonitizing PaaS With Docker"
date: 2013-08-14 15:17
comments: true
categories:
---

Anyway,
it finally clicked for me
that lightweight containerization is the missing piece in my plans
for an open source deployment tool to "demonitize" the current crop
of "git push heroku" PaaS  providers.
*evil pinkie finger*

These problems are solved or very solvable with current tools:

## Solved (or mostly-solved) problems

### Application Builders

Tools to package up your "application"
(rails, node.js, python, Java, etc)
with all of it's dependencies
and define a clear way to run that application.
All of the things that wrap around
language-specific dependency management tools:

* [bundler](http://bundler.io/) with
  [rvm](https://rvm.io/)
  or [rbenv](https://github.com/sstephenson/rbenv)
* [pip](http://www.pip-installer.org/en/latest/),
  [virtualenv](http://www.virtualenv.org/),
  [terrarium](https://github.com/PolicyStat/terrarium)
* [npm](https://npmjs.org/)
* [Java WAR files](http://en.wikipedia.org/wiki/WAR_file_format_\(Sun))

#### Current Solutions

* [Heroku Buildpacks](https://devcenter.heroku.com/articles/buildpacks)
* [buildstep](https://github.com/progrium/buildstep)

### Configuration Management

This is the level above application builds
and good config management will use an application builder as well.
Defining things like what should be installed on a machine
(packages)
and what their config files should be.

#### Current Solutions

* Chef
* Puppet
* Saltstack

### Orchestration

This is the level above Configuration Management,
which defines how chunks of config management should work together
**in motion**.
It strings together different components,
eg some web server processes,
memcached instances,
some background job workers
and a database.
Some of these even help you spread your services across pre-existing hardware
without you needing to make decisions
(provisioning across a "cluster").

#### Current Solutions

* Juju
* Cloud Foundry
* Open Shift

Flynn (discussed below) does this job,
but also aims higher.

Most of these tools consider themselves,
or at least market themselves,
as a PaaS in a box.
Most provide at least some of the "Heroku experience" for developers,
but currently have fairly fundamental flaws
that severely limit their potential
to disrupt the current status quo.
But that's a large topic in itself.

#### Note on Cloud Foundry

I reserve the right to be completely wrong about Cloud Foundry.
They're at least [experimenting](https://github.com/cloudfoundry/bosh-lite)
with Docker for the tool that deploys Cloud Foundry.
I might just not be smart enough
to [understand Cloud Foundry](http://docs.cloudfoundry.com/docs/running/bosh/components/).
Heck,
I don't really even understand
the [tool](https://github.com/cloudfoundry/bosh) they wrote
to deploy Cloud Foundry itself!?
I'm told by someone I trust who kind of understands it
that the architecture is really cool.
It also looks like basically everything
is undergoing a major V2/NG rewrite,
so maybe they'll get more hackable,
more composable,
and more ops-friendly
before Flynn does it's thing.
I hope it happens.

### Do it in the cloud: Infrastructure (as a service)

This piece is optional,
and largely orthogonal to the other needs,
but is something that almost everyone could use.
You can stop here if you just want to run your application in a colo
with a fixed number of servers.
That makes sense for very few people though,
and makes high availability
and load-aware scaling much more expensive and/or impossible.

Plus,
even my mom knows that "The Cloud" is awesome.

#### Current Solutions

* AWS
* Google Compute Engine
* Rackspace Cloud
* Other folks trying to provide public [Open Stack](http://www.openstack.org/) clouds

## Not (yet) solved problems

### One-step, Production-aware Deploys

This is the `$ git push heroku` part.
A developer runs one command
and all of those other pieces in the stack dance as appropriate
so that your application changes
without your users noticing.
You'll need:

#### Key Requirements

* Load-balancer juggling for zero-downtime deploys
* Automated health checks
* Rollbacks
* Backing services managed automatically
* Scaling up and down via one bullet-proof command (or API)
* Easy application High Availability
* Easy ops "Best Practices"
  * Monitoring/Alerting
  * Metrics
  * Log Aggregation
  * Service Registration

The proprietary PaaS providers use this as their respective secret sauces.

#### Requirements that Can Be Met

* Staged deploys enforcing HA requirements
* Datacenter awareness
* Ability to optimize hardware usage
* Dev can implement backing services
  using open source recipes
  with close to the Heroku services experience
* Ops can create backing services
  with their familiar tools
* Managed backing services
  with persistent disk support
  and integrated backup/restore

#### Emerging solutions

##### Dokku

[Dokku](https://github.com/progrium/dokku)

The Docker powered mini-Heroku.
This is a toy-ish proof of concept powered by Docker.

##### Flynn

[Flynn](https://flynn.io/)

* $80k+ in funding
* Staffed by super-smart people
  (including the author of Dokku)
* Aiming to be the thing that
  the Orchestration tools should have been.
* Not aiming at solving the infrastructure provisioning problem.

##### Neckbeard

[Neckbeard](https://github.com/winhamwr/neckbeard)

My project that really doesn't deserve to be mentioned in the same category,
but is the open-sourcing
of an internal tool
that solves the problems Flynn aims to solve.
With the announcement of Flynn,
I'd be very,
very happy
to rewrite Neckbeard as something powered by Flynn.
From my reading of the [Flynn Spec](https://github.com/flynn/flynn-spec),
I would still need:
* IaaS helpers:
  Automatically provision ec2 instances,
  mount EBS volumes
* Datacenter-aware HA:
  Don't put the whole service in one Availability Zone
* Use the Flynn API to implement staged rollouts

## Configuration Management and Orchestration still sucks

Even with Chef/Puppet/Saltstack
and the proliferation of open source,
reusable code
(eg. Chef Cookbooks)
based around things like
MySQL,
Memcached,
and Nginx,
there's still no such thing as
an off-the-shelve MySQL high-availability setup.
There's no
"Here's how you configure Redis to survive losing a datacenter
with no interruption or data loss."
There's no
"run this command to add another memcached node."
^1

Even more difficult,
try mixing and matching these various services
on machines that aren't dedicated to that purpose!

Heroku and other PaaS providers punt on this problem
by letting companies sell you [Backing Services](http://12factor.net/backing-services)
that do the hard stuff
which you can consume over APIs.
That's a great business move
as long as there are no alternatives for people other than
"either hire someone really smart
who knows how to make MySQL high-availability her bitch,
or spend a couple years learning about it in production."
Pay an X% markup over infrastructure price
(plus a chunk to Heroku)
 to not need to worry about that?

Hells yeah I will!

## Enter Docker

This is where Docker comes in!

It's difficult and time-consuming
to learn MySQL well enough to do an awesome HA setup,
but that knowledge is easily shared
if someone else needs an identical setup.
The problem is that no setups are identical.

### We're all Unique Snowflakes

Everyone needs to customize things to:

1. Keep service A from breaking service B
  before they even start.
  "Shit.
  My Redis package upgrades a library that mysql uses."
2. Keep service A from breaking service B occasionally in production.
  "Balls.
  A uwsgi process hit 400MB in a request
  and RabbitMQ ran out of memory and crashed."
3. Keep services X and Y working together after Y fails over.
4. Restore service Y with backed up data
  and make service X aware of the change.

### You're not Special

Docker,
via [Linux Containers](http://en.wikipedia.org/wiki/LXC),
 allows complete isolation
so that everyone's service X looks the same.
It does this with requiring heavy virtualization,
so you can actually use it outside of development.
This means that your Chef Cookbook
(or whatever configuration management slash orchestration tool)
only needs care about a limited set of possibilities.

1. Service A and B are isolated.
  You can't put yourself in dependency hell.
  No more coordinating users,
  groups
  and permissions.
2. You can place strict boxes around resources
  so that service A can't
  hog all of service B's RAM.
3. (and 4)
  Since the services are in containers,
  I can use any container-aware config management recipes
  and be sure they work in my environment.
  Even better,
  I can test the failure modes on my laptop
  or in a Vagrant config
  running on my laptop.

## Existing Tools + Docker + ??? = Awesome

Now that Docker is a thing,
the last ingredient towards
The Solution exists.
Flynn,
or whatever wins in the FOSS marketplace of ideas,
can string together Docker plus the myriad existing FOSS tools
and build a whole that is much greater than the sum of its parts.
This kind of tool has several huge advantages over existing
and future
commercial PaaS products that will completely change the game.

### Advantage: Easier Problem

There are a lot of PaaS providers
with a lot of dedicated development resources.
Heroku and dotCloud in particular
have some amazing developers who do amazing work.
Docker wouldn't even exist
if dotCloud hadn't developed and open-sourced it.

But these companies and projects are solving problems
that are much more difficult.
and other public PaaS providers

With this solid core in place,
the consta

## Footnotes

1: Orchestration tools like Juju aim to provide this
with hooks to define and consume services
and hooks to handle change events
but that only gives you a framework
to solve the problem yourself.
Even with example Juju charms,
for example,
you have the same problem as with "reusable" Chef Cookbooks.
