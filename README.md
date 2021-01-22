<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [IDeal](#ideal)
    - [Tenets](#tenets)
- [Design](#design)
- [How-To](#how-to)
    - [Use](#use)
        - [Via Network](#via-network)
        - [As local demon](#as-local-demon)
        - [As a library](#as-a-library)
    - [Deploy](#deploy)
        - [Docker](#docker)
        - [Demon](#demon)
    - [Monitor](#monitor)
        - [Metrics](#metrics)
        - [Logs](#logs)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# IDeal

*NOTE*: The project is in its initial state and does not work yet. The following describes V1 state of things and until
that milestone is achieved, some or all features described on this page might not be available. See the state of IDeal
features [here](https://github.com/oantoshchenko/IDeal/projects/1)

IDeal is a service and/or a Rust library that provides unique IDs, fast and reliably. Think
[Twitter Snowflake](https://blog.twitter.com/engineering/en_us/a/2010/announcing-snowflake.html) that is easy to deploy,
monitor, maintain and that you also can configure ID parameters, or provide your own code to generate completely custom
one.

The problem IDeal is solving is when you, for instance, have a large system and need to generate primary keys for your
data entries, but your storage does not have this capability, and you can't rely on any sort of randomly generated IDs
because you need those IDs to be sequential for instance or you are concerned about collision (yes even UUIDs do
collide).

At this moment there is no easy solution to this problem, so you have to:

1. Use a database with this capability, simply autoincrement field in your typical *relational DB*.

   **Pros**
    1. If you store data in this DB use the IDs it gives (why are you even here?)

   **Cons**
    1. You have to maintain relational DB cluster, depending on the vendor, most likely with master-master replication
       for high availability. This is complicated.
    1. Relational databases do not scale horizontally, that is, the only way you can get more throughput is by buying or
       renting more powerful hardware, eventually you will hit the limit. There are also laws of physics, where there is
       only so much information can be passed over one wire.

1. Generate *Random ID*.

   **Pros**
    1. It is super easy. You do not have to maintain any specific service or demon for it, just do it in place. If
       things in a "Cons" section below are not your concerns, that is what you should do!

   **Cons**
    1. If ID collision (that is where you randomly generate the same ID more than once) is a concern for the system,
       this approach might be an unacceptable risk. Collision chance is proportional to the usage of the system i.e.
       number of IDs generated. Even though it sounds appealing that the chance of ID collision is minuscule, it is
       still a chance.
    1. To reduce chance of collision you would want to generate a large enough ID. It is not a problem for a system with
       relatively number of IDs to generate. If you are dealing with large volume every bit matters.
    1. If you need to be able to make any sense of the ID, as in you want to be able to sort by ID within some margin of
       error, you can not do that with random IDs.

## Tenets

Here are the principals that IDeal is built around:

1. **Fast**. The whole purpose of IDeal is to be fast, as fast as it gets, if there is a way to make it faster, we
   should.
1. **Reliable**. As IDeal will fill the critical part of the infrastructure, users should not be worried that it might
   fail. Obviously, everything eventually fails, but given there is a redundancy of instances, fail-over, automatic
   recovery and monitoring should make it as close to 100% reliable as possible.
1. **Convenient**. It does not matter what is the model under which you want to use IDeal, as a separate cluster, a
   local demon, a library; it has to be easy to install/configure/run/monitor. Weather like JSON over HTTP(S), Protobuf,
   Graphql IDeal will speak your language. It should slide into existing infrastructure or code base as knife through
   butter.
1. **Flexible**. IDeal will not dictate how you run it or use it, you should. Therefore it is build so that the user can
   decide whether to run it as a separate service, a side-car, a local demon process, or as a part of code base as a
   plug in library. This concern extends to format of IDs it vends, where and how it emits metrics and logs etc.

# Design

Design documentation is located [here](https://github.com/oantoshchenko/IDeal/blob/main/doc/DESIGN.md)

# How-To

## Use

### Via Network

### As local demon

### As a library

## Deploy

### Docker

### Demon

## Monitor

### Metrics

### Logs
