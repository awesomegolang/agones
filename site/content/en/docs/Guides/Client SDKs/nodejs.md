---
title: "Node.js Game Server Client SDK"
linkTitle: "Node.js"
date: 2019-02-24T15:56:57Z
publishDate: 2019-04-01
weight: 50
description: "This is the Node.js version of the Agones Game Server Client SDK."
---

Check the [Client SDK Documentation]({{< relref "_index.md" >}}) for more details on each of the SDK functions and how to run the SDK locally.

## Download

Download the source {{< ghlink href="sdks/nodejs" >}}directly from Github{{< /ghlink >}}.

## Prerequisites

- Node.js >= 10.13.0

## Usage

Add the agones dependency to `package.json`, replacing with the download location:

```json
"dependencies": {
  "agones": "./lib/agones"
  ...
}
```

To begin working with the SDK, create an instance of it. This will open a connection to the SDK server.

```javascript
const AgonesSDK = require('agones');

let agonesSDK = new AgonesSDK();
```

To send a [health check]({{< relref "_index.md#health" >}}) ping call `health()`.

```javascript
agonesSDK.health();
```

To mark the game server as [ready to receive player connections]({{< relref "_index.md#ready" >}}), call the async method `ready()`. The result will be an empty object in this case.

```javascript
let result = await agonesSDK.ready();
```

Similarly `shutdown()`, `setAnnotation(key, value)` and `setLabel(key, value)` are async methods that perform an action and return an empty result.

To get [details of the backing GameServer]({{< relref "_index.md#gameserver" >}}) call the async method `getGameServer()`. The result will be an object representing `GameServer` defined in {{< ghlink href="sdk.proto" >}}`sdk.proto`{{< /ghlink >}}.

```javascript
let result = await agonesSDK.getGameServer();
```

To get [updates on the backing GameServer]({{< relref "_index.md#watchgameserver-function-gameserver" >}}) as they happen, call `watchGameServer(callback)`. The callback will be called with a parameter matching the result of `getGameServer()`.

```javascript
agonesSDK.watchGameServer((result) => {
	console.log('watch', result);
});
```

For more information, please read the [SDK Overview]({{< relref "_index.md" >}}), check out {{< ghlink href="sdks/nodejs/src/agonesSDK.js" >}}agonesSDK.js{{< /ghlink >}} and also look at the {{< ghlink href="examples/nodejs-simple" >}}Node.js example{{< / >}}.
