# Tinfoil

> **Warning**: Tinfoil is in <ins>alpha</ins>. This means that not all of the Discord API is currently supported. It is recommended against using Tinfoil currently, as breaking changes are frequent.

**Tinfoil is a small and lightweight wrapper for Discord's REST and Gateway API, written in Typescript and designed with scalability in mind.**

Tinfoil leaves a lot of stuff up to the user, allowing for more fine-tuned control over how your bot interacts with the API. It is best to think of Tinfoil more like a general utilities library for working with Discord's API, rather than a feature-complete library, such as [discord.js](https://discord.js.org). Tinfoil is focused more on providing features relating to load balancing and operating bots at scale, rather than high-level development.

You can find the documentation at [tinfoil.dev](https://tinfoil.dev).

## Getting Started
You can install Tinfoil with one of the commands below, depending on what package manager you are using:
```
// Install commmands coming soon
```

A simple bot example:
```ts
import { Client } from "tinfoil";

const bot = new Client(process.env.BOT_TOKEN as string);
console.log(await bot.users.me.get()) // Logs bot information
```

## Scaling

Tinfoil provides APIs to easily control scaling for sharded bots, including load balancing, cluster management, global app state management, easy shard-to-shard communication, and additional utility functions. You can bring your own cluster technology by defining functions to be executed when your app scales up and down.

Tinfoil has a built-in load balancer for sharded gateway connections that prioritizes equal distribution across nodes. If any shards are experiencing significant load, Tinfoil will essentially split their load in half by reassigning their shard IDs. Tinfoil will scale your application without taking any shards offline for a significant amount of time. In order to save resources, if load is significantly reduced on a specific shard, Tinfoil will scale your app down automatically by merging its load into another shard and taking it offline. Shards are grouped together into Shard Collections, which are just actual processes or containers (depending on what you are using for your cluster). Tinfoil also handles max concurrency for you, so shards are started quickly in the event of a restart.

You can define your cluster manager with the `ShardNetworkManager` class. The cluster manager lets you define what happens when your application needs to add or remove shards. You can also pass custom settings via the `options` paramater, including breakpoints for when your app should scale up or down.

**Tinfoil's scaling APIs and load balancer are still under development**, and are not fully available at this time.

## Contributing

Please open an [issue](https://github.com/bremea/tinfoil/issues/new) with any bug reports, or a [pull request](https://github.com/bremea/tinfoil/compare) to merge something you worked on.

------------

Join our [Discord server](https://discord.gg/CXhCTscDfc) for support and updates!
