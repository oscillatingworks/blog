---
layout: post
title: Building SQLite clusters with rqlite
date: 2015-03-26 00:00:00
description: Small, comprehensive, Raft-based clustering middleware for SQLite databases.
author: oscillatingworks
hn-discussion:
tags:
- raft
- sqlite
- iot
- paxos
- distributed consensus
---

Today our compass lead us into direction of [`rqlite`]. It is a small, comprehensive, [Raft]-based
clustering middleware for [SQLite](https://sqlite.org/) databases. Someone could ask
who the hell would need SQLite cluster, but first things first.

## Raft

`rqlite` is using Raft [consensus protocol] to perform replication among SQLite database nodes.
In short Raft is an alternative to [Paxos], which is hardly understood among population including ourselves.
In general Raft ensures that if any state machine applies some operation as the `nth command`, no other
state machine will ever apply a different `nth command`. This leads to consistency among distributed
state machines and it's something `rqlite` guaranties among SQLite nodes - consistency and partition
tolerance - CP among [CAP].

## Use cases

Now we know more or less what `rqlite` is and how does it work. But let's answer most important question -
who and why would need it? To answer above questions lets first go back to official SQLite manifesto:

> SQLite is a good fit for use in cellphones, set-top boxes, televisions, game consoles,
  cameras, watches, kitchen appliances, thermostats, automobiles, machine tools, airplanes,
  remote sensors, drones, medical devices, and robots: the "internet of things"

Exactly, kitchen appliances, thermostats, remote sensor, drones, robots - Internet Of Things -
is it not what is hot right now and according to many predictions will be next big thing?
We bet it will.

Currently while implementing IoT solutions you usually use some cloud based data feed and sync mechanisms,
i.e [firebase], [relayr], but sooner or later your sensors will need to share some data/state
only among each other, without need to synchronize it over the public network, which is
faster, cheaper and more reliable.

## Limitations

The biggest limitation of the above solution is a blocking nature of the Raft protocol -
the save is committed if majority of nodes agree on this.
So probably `rqlite` won't be good for huge sensor networks, replicating data among all of
them. Typical use case here could be some mission critical sensor system where consistency
might be the main requirement. For example some group of sensors (few / dozen) which work
together based on some consistent state / data shared among each other. Data between them needs
to be replicated and consistent, so others can immediately take over the responsibility from
the sensor which died (warm standby).

## Hands on

Due to its simplicity, SQLite is perfect to be run on almost any type of connected device.
Together with `rqlite` it can give IoT makers solution to sync any type of data locally.
Due to this opportunity, we strongly believe that `rqlite` is a very promising, still fresh, but active project.
Among that it is implemented in [Go], another new big thing in the world of programming languages.
It is really hard to find good reasons not to contribute to this small, yet already interesting project.
And we plan to do it. Let's see how far we can go. We'll keep you updated.

[`rqlite`]: https://github.com/otoolep/`rqlite`
[Raft]: https://raftconsensus.github.io/
[consensus protocol]: http://en.wikipedia.org/wiki/Consensus_%28computer_science%29
[Paxos]: http://en.wikipedia.org/wiki/Paxos_%28computer_science%29
[CAP]: http://de.wikipedia.org/wiki/CAP-Theorem
[firebase]: https://www.firebase.com/
[relayr]: https://relayr.io/
[Go]: https://golang.org/
