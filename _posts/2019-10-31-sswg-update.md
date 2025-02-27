---
layout: post
published: true
date: 2019-10-31 10:00:00
title: SSWG Annual Update
author: tanner
---

The [Swift Server Work Group]({{ site.url }}/server/) (SSWG) set out [12 months ago](https://forums.swift.org/t/next-steps-for-the-swift-server-work-group/15816) to begin defining and prioritizing new efforts to address the needs of the Swift server community. Since then, we've been busy meeting regularly, working with the community, defining guidelines, writing Swift packages, voting on proposals, posting in the forums, and much more. We feel that we've made significant progress toward those goals we set out last year and we'd like to share a high-level update with you today.

## Incubation Process

We believe that a healthy open source ecosystem relies heavily on the quality of its packages. Because of this, our biggest focus has been on a proposal process for packages (somewhat similar to Swift Evolution) that we call the [Incubation Process](https://github.com/swift-server/sswg/blob/master/process/incubation.md). This process defines how someone with an existing Swift package or new idea can get feedback, follow best practices, and eventually be included in the official Swift server package index. 

The incubation process is chock-full of well-considered guidelines and requirements around things like concurrency, testing, and code style. The SSWG is working continuously to improve the Incubation Process and its recommendations. Two ammendments to the process have already been proposed and accepted.

While we want code quality high, we are also cognizant of keeping the barrier to entry as low as possible. To make the incubation process simple and accessible, we use the Swift forums. Pitching your idea or package (the first step of the Incubation Process) is done by creating a new post in the Server > Pitches category.

Once a package has completed the incubation process and been accepted by the SSWG, it will be listed on the Swift server package index. Accepted packages will undergo regular review to ensure they still meet qualifying standards. While still in its humble beginnings, we hope this index will grow to be an invaluable asset to Swift programmers. 

## Libraries

[Nine proposals](https://github.com/swift-server/sswg/tree/master/proposals) have been accepted via the Incubation Process so far. These packages are being adopted rapidly by upcoming versions of popular server-side Swift frameworks like [Vapor 4](https://github.com/vapor/vapor) and [Kitura](https://github.com/ibm-swift/kitura). 

### SwiftNIO

- Accepted: 9/7/2018
- Author: Apple ([@apple](https://github.com/apple/))
- Code: [github.com/apple/swift-nio](https://github.com/apple/swift-nio)

> Event-driven network application framework for high performance protocol servers & clients, non-blocking.

This package is at the heart of the Swift server ecosystem. It provides a common API for network communication that is highly extensible and efficient. Most packages that do networking will either be built on SwiftNIO directly or provide some wrappers for convenient interoperation.

### SwiftLog

- Accepted: 2/7/2019
- Author: Johannes Weiss ([@weissi](https://github.com/weissi/))
- Code: [github.com/apple/swift-log](https://github.com/apple/swift-log)

> A Logging API for Swift 

This universal logging API can be used by any package that would like to output logs, but doesn't want to worry about which specific logging implementation to use. By using SwiftLog, your package lets the end user choose how to accumulate the information. 

Since success of a logging API depends heavily on adoption, the SSWG prioritized development of this package to ensure quality and early availability. 

### SwiftMetrics

- Accepted: 4/4/2019
- Author: Tomer Doron ([@tomerd](https://github.com/tomerd/))
- Code: [github.com/apple/swift-metrics](https://github.com/apple/swift-metrics)

> A Metrics API for Swift

SwiftMetrics provides a universal API for metrics. This allows packages to report structured information using meters like gauges, timers, counters, and more. Just like SwiftLog, packages that use the SwiftMetrics API give the end user the freedom to choose which metrics implementation is used. 

### PostgresNIO

- Accepted: 5/16/2019
- Author: Tanner Nelson ([@tanner0101](https://github.com/tanner0101/))
- Code: [github.com/vapor/postgres-nio](https://github.com/vapor/postgres-nio)

> Non-blocking, event-driven Swift client for PostgreSQL.

PostgresNIO is the first database driver to be approved by the SSWG (with many more to come). This Postgres client was built from the ground up on SwiftNIO 2 following best practices as outlined by the Incubation Process. 

Using SwiftNIO natively makes this Postgres client much more efficient to run alongside a SwiftNIO HTTP server when compared to a blocking, C-based approach. 

### rediStack

- Accepted: 6/27/2019
- Author: Nathan Harris ([@mordil](https://github.com/mordil))
- Code: [github.com/Mordil/swift-redi-stack](https://github.com/Mordil/swift-redi-stack)

> Non-blocking, event-driven Swift client for Redis. 

Shortly after the Postgres client came RediStack, a Redis client. This package is also built natively on SwiftNIO 2 and takes great care to follow best practices. Given the simplistic nature of Redis' RESP protocol, this package makes a great example project for anyone interested in making their own database driver. 

### AsyncHTTPClient

- Accepted: 6/27/2019
- Author: Artem Redkin ([@artemredkin](https://github.com/artemredkin))
- Code: [github.com/swift-server/async-http-client](https://github.com/swift-server/async-http-client)

> HTTP client library built on SwiftNIO

This package provides an efficient and easy-to-use alternative to `URLSession` for Swift server applications. AsyncHTTPClient can be used more efficiently alongside other SwiftNIO-based packages when compared to Linux's [cURL](https://curl.haxx.se)-based `URLSession`. This package supports streaming bodies, proxying, cookie parsing, and more. 

### APNSwift

- Accepted: 6/27/2019
- Author: Kyle Browning ([@kylebrowning](https://github.com/kylebrowning))
- Code: [github.com/kylebrowning/APNSwift](https://github.com/kylebrowning/APNSwift)

> An HTTP/2 APNS library built on swift-nio

This package makes sending push notifications via APNS easy. It provides a simple API that handles the HTTP/2 connection, payload encoding, and JWT signature creation using ECDSA behind the scenes.

### StatsdClient

- Accepted: 8/8/2019
- Author: Tomer Doron ([@tomerd](https://github.com/tomerd/))
- Code: [github.com/apple/swift-statsd-client](https://github.com/apple/swift-statsd-client)

> Metrics backend for swift-metrics that uses the statsd protocol.

This package allows the Swift Metrics API to output data to aggregation servers using the statsd protocol. 

### Prometheus

- Accepted: 8/8/2019
- Author: Jari ([@MrLotU](https://github.com/MrLotU/))
- Code: [github.com/MrLotU/SwiftPrometheus/](https://github.com/MrLotU/SwiftPrometheus/)

> Client-side Prometheus library in Swift 

This package allows the Swift Metrics API to output data to Prometheus. 

## Tooling

Beyond package incubation, the SSWG is also focused on improving Swift and its tooling on Linux. 

### Docker

Official Swift images are now available via [Docker hub](https://hub.docker.com/_/swift) for Swift 3, 4, and 5 on Ubuntu 16.04 (Xenial) and Ubuntu 18.04 (Bionic). New images are created whenever a new version of Swift is released. In addition to the normal images with everything you need to build and run Swift, there are now "slim" images that contain only what is required to run Swift. These are great for reducing final container size with multi-stage build Docker builds. Checkout the [Swift Docker repo](https://github.com/apple/swift-docker) for more information.

### Swift Backtrace

- Author: Ian Partridge ([@ianpartridge](https://github.com/ianpartridge))
- Code: [github.com/ianpartridge/swift-backtrace](https://github.com/ianpartridge/swift-backtrace)

This package provides support for automatically printing crash backtraces of Swift programs on Linux. Backtraces are generated by a builtin C library [libbacktrace](https://github.com/ianlancetaylor/libbacktrace) and demangled using a private Swift runtime call. We hope to improve the implementation by adopting [SE-0262](https://github.com/apple/swift-evolution/blob/master/proposals/0262-demangle.md) when it is approved. We are also working with the Swift core team to discuss the benefits of merging this functionality into the Swift standard library. 

### Linux Patch Releases

Starting with [Swift 4.2.2](https://forums.swift.org/t/announcing-swift-4-2-2-and-monthly-swift-4-2-x-dot-releases-for-linux/20148), Linux now receives monthly patch releases containing bug fixes. Each patch release receives a review manager responsible for merging patches during a three-week window. After this window closes, the patch is finalized and released on Swift.org. This means that Linux servers will get much faster access than before to bug fixes and improvements in Swift and its core libraries. 

## Future: Focus Areas for 2020

Going forward, our main focus will continue to be on adding new packages to our index. There is a plethora of packages we'd like to see in 2020. Outside of packages, we hope to continue improving Swift and its tooling on servers.

If any of the new focus areas listed below pique your interest, we highly encourage you to get involved. If you are not sure where to begin, consider posting in the [Server section](https://forums.swift.org/c/server) of the Swift forums with your questions or ideas. You can also consider more formally [pitching](https://github.com/swift-server/sswg/blob/master/process/incubation.md#pitch) your idea to the work group. Check out our [Incubation Process](https://github.com/swift-server/sswg/blob/master/process/incubation.md) which describes how to pitch, propose, and submit packages to our index.

### Database Drivers and Storage Clients

The SSWG has accepted client implementations for [Postgres](https://github.com/vapor/nio-postgres) and [Redis](https://github.com/mordil/swift-redis-nio-client).

Work is being done toward proposing MongoDB clients using both [MongoKitten](https://forums.swift.org/t/mongodb-client-using-swiftnio/24666) and the [MongoDB C Driver](https://github.com/mongodb/mongo-swift-driver).

Vapor is planning to pitch two more of its database drivers, [MySQLNIO](https://github.com/vapor/mysql-nio) and [SQLiteNIO](https://github.com/vapor/sqlite-nio).

But there are many more databases out there! Zookeeper, Cassandra, and Kafka to name a small few. We highly encourage anyone with expertise in a database driver to consider getting involved. 

### Distributed Tracing

The first two [pillars of observability](https://www.oreilly.com/library/view/distributed-systems-observability/9781492033431/ch04.html) have been accepted: [swift-log](https://github.com/apple/swift-log) and [swift-metrics](https://github.com/apple/swift-metrics). Now we need the final piece: tracing. There have been exciting developments in tracing in recent times, such as OpenTracing [joining the CNCF](https://www.cncf.io/blog/2016/10/11/opentracing-joins-the-cloud-native-computing-foundation/). If you are interested in helping design the future of distributed tracing in Swift, we'd love to hear from you.

### Connection Pooling

Vapor's [AsyncKit](https://github.com/vapor/async-kit/blob/master/Sources/AsyncKit/ConnectionPool.swift) package, [AsyncHTTPClient](https://github.com/swift-server/async-http-client/pull/105), and others are working on connection pool implementations. There are lots of interesting questions coming up already around concurrency and performance. Can there be one connection pool to rule them all, or should there be many separate ones that follow well considered best practices? If you have ideas on how connection pooling in Swift should work, let's combine forces.

### OpenAPI

[Kitura](https://github.com/IBM-Swift/Kitura-OpenAPI) has had support for OpenAPI for a while now and [Vapor](https://github.com/vapor/open-api) is beginning to explore the space. We believe there is room here for a shared library. Something that integrates deeply with the SSWG's accepted solutions for logging, metrics, and tracing is especially important. If you are interested in OpenAPI, consider getting involved. 

### Linux Distros

Swift currently offers prebuilt toolchains for Ubuntu. There are many other distros out there and we'd love to see them supported officially. The process for adding a new Linux distro to Swift is not clear at the moment. We think that can be improved. The community could help by identifying which Linux distros are important and contributing reliable build scripts. In a perfect world, we could make this entire system self serve. Does this sound interesting to you? If so, reach out to us.  

### Deployment Guides

Getting your applicaton production-ready can be a daunting process. There are the simple things, like remembering to use `-c release`, and the harder things, like writing code that is [horizontally scalable](https://12factor.net/concurrency). Once your app is in production, how do you deal with things like leaks and crashes? 

There are lots of things we could do to make this process easier: code templates, how-to guides, information on best practices, etc. If this seems interesting to you, we'd love to hear your ideas.

### Showing Adoption 

"Is server-side Swift production ready?"

YES!

Swift on server is being used in production everywhere by huge and small companies alike. We need to do a better job of showing people this. How can we collect this information? How can we amplify success stories? If you have any ideas, let us know. 

### And Much More...

Swift on the server is growing quickly and there's way more that the SSWG wants to do than we can fit on this list. If you have a great idea that wasn't listed here, let us know about it on the [Swift forums](https://forums.swift.org/c/server).  There is also a [matching post](https://forums.swift.org/t/sswg-annual-update-october-31-2019/30367) for this blog post on the Swift forums if you have specific questions or comments!
