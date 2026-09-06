# Algorithmic Games

[Algorithmic Games](https://Algorithmic.Games/) is a platform for competitive programming and match making between algorithms. Users can make their own participants to compete in any of the existing arenas, or make their own custom arena and challenge other users to join. Algorithmic Games was previously known as "AI-Tournaments", where "_AI_" in the name refers to playing against the computer on old video games, like "_Hard AI_" or "_Hard CPU_".

<!-- Other platforms:
// LinkedIn
Algorithmic Games is a platform for competitive programming and match making between algorithms. Users can make their own participates to compete in any of the existing arenas, or make their own custom arena and challenge other users to join. First prototype was done some time before 2016, but all source history from that time is lost. In 2020 a new fresh start took place.
-->

See the section [Participate](#Participate) if you want to join an arena, then analyze how others have solved the arena until better documentation has been written.

## Community

If you want to join the discussions, head on over to the <a href="https://algorithmic.games/Community/Official/" target="_blank">Community handbook</a> and read where we are.

## Participate

### Participant

To join an arena, [create a public GitHub repository](https://github.com/AlgorithmicGames/Participant-Template) from the participant template and add three topics:

1. `AlgorithmicGames`
2. `AlgorithmicGames-Participant`
3. The arena you are entering, written as `Owner--Repository` (replace the slash in the arena’s GitHub name with two hyphens). For `AlgorithmicGames/Arena-Kalaha` that is `AlgorithmicGames--Arena-Kalaha`.

Put your algorithm in a file named `participant.js` in the repository root.

If you tag a repository `AlgorithmicGames-retired`, it will no longer show up in the participant list.

**Name shown in matches.** The label comes from your GitHub repository name (your account plus the repo name), not from a separate title field. Naming the repository `Easy` under your account is enough; in Kalaha it would show as something like `YourAccount/Easy`.

It's possible to use prefix `AlgorithmicGames-Participant{-ArenaName}-` on your repository names so your participant repos sort together on GitHub (`AlgorithmicGames-Participant-Kalaha-Easy`, `AlgorithmicGames-Participant-Kalaha-Random`, and so on). That prefix is only for your own organization. On the arena page the site trims the shared part for that arena, so `ChrisAcrobat/AlgorithmicGames-Participant-Kalaha-Easy` can appear as `ChrisAcrobat/Easy` instead of having multiple participants named `AlgorithmicGames-Participant-Kalaha-`.

### Publish an arena

To publish a new arena on the site, [create a public GitHub repository](https://github.com/AlgorithmicGames/Arena-Template). Good examples are [Arena-Worm](https://github.com/AlgorithmicGames/Arena-Worm) and [Arena-Kalaha](https://github.com/AlgorithmicGames/Arena-Kalaha).

Your repository needs at least:

- `arena.js`, which defines the game rules
- `properties.json`, which describes settings, team limits, and where the replay page lives
- Optional folders `replay/` and `interface/` for watching matches and human play

Add the topics `AlgorithmicGames` and `AlgorithmicGames-Arena-v1`, then create a **GitHub release**. The site loads published arenas from the latest release, not from an unpublished branch.

When others write participants for your arena, they use your arena topic in the same `Owner--Repository` form (for example `YourName--My-Arena`).

### Develop environment

Use this while building an arena or participant before everything is ready to be discovered on the site.

On the [Setups](https://algorithmic.games/Setups) page you can paste URLs to your arena, replay page, and participants or human interfaces (typically `raw.githubusercontent.com` links to files in your GitHub repositories) and run test matches.

Your code can use `console.log`, `console.warn`, `console.error`, `console.info`, `console.debug`, and `console.table`. During normal matches those messages are ignored. In Setups, choose the `participant-with-console` type if you want console output saved in the match log while testing.

<b>Setups fields</b>

| Key                               | Description                                                                                                                             | Example                                                                                                                                                                                                                              |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| arena.url                         | Link to the arena files.<br>⚠️ Do not link directly to `arena.js` , but to it's parent.                                                 | `"https://raw.githubusercontent.com/AlgorithmicGames/Arena-Worm/<release-tag>/"`                                                                                                                                                     |
| arena.name<br><i>Optional</i>     | Name shown in the list.<br>Defaults to the URL if empty.                                                                                | `"Arena-Worm"`                                                                                                                                                                                                                       |
| arena.replay                      | Link to the replay page.                                                                                                                | `"https://raw.githubusercontent.com/AlgorithmicGames/Arena-Worm/<release-tag>/replay/"`                                                                                                                                              |
| arena.settings<br><i>Optional</i> | Starting settings for the match.                                                                                                        | `{"general":{"seed":"example"}}`                                                                                                                                                                                                     |
| joinables                         | Who joins the test match.<br>Each entry is a participant URL, or an object with `url` and optional `name`, `team`, `color`, and `type`. | `["https://raw.githubusercontent.com/YourAccount/Your-Participant/main/participant.js",{"url":"https://raw.githubusercontent.com/AlgorithmicGames/Arena-Worm/<release-tag>/interface/","name":"Human","type":"interface","team":1}]` |

Setups also offers extra controls to help you test and debug before release.

#### Joinable types

Each entry in `joinables` is either a participant URL or an object with a `type` field:

| `type`                                         | Meaning                                                                                                                                                                  |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `participant`                                  | Default. Loads `participant.js` the same way as on the live site.                                                                                                        |
| `participant-with-console`                     | Same as `participant`, but saves `console.*` output to the match log while testing.                                                                                      |
| `un-sandboxed-participant` (not yet supported) | Old Setups label only. Your code still runs in the same isolated environment as other participants.                                                                      |
| `interface`                                    | Opens a web page on your computer for a human player. Uses [`InterfaceHelper.js`](https://algorithmic.games/InterfaceHelper.js).                                         |
| `interface-p2p`                                | Human player joins from their own browser. You get a shareable link (and QR code) they open at `/join`; the interface page does not open automatically on your computer. |

#### Participant scripts

You put your algorithm in `participant.js` in your repository ([Participant template](https://github.com/AlgorithmicGames/Participant-Template)). The arena loads that file when you join a match.

Your script talks to the arena with `onmessage` and `postMessage`. The first message is usually setup: settings, opponents, and similar data. After that, each message is something the arena wants you to act on (often in `message.data`). Reply with `postMessage(...)` when you are done thinking; the match waits for that answer before it moves on.

A common pattern is to handle setup once, then handle every later message the same way:

```javascript
onmessage = (init) => {
	// use init once (settings, opponents, …)
	onmessage = (message) => {
		const data = message.data
		postMessage({/* your reply */})
	}
}
```

You can keep variables in your file between messages if you need to remember state from one turn to the next.

#### Interface

An [interface](https://github.com/AlgorithmicGames/Interface-Template) is a normal web page for human players or custom graphics. It uses [`InterfaceHelper.js`](https://algorithmic.games/InterfaceHelper.js) instead of `participant.js`.

Arenas can list built-in human interfaces in `properties.json` under `header.defaultHumanInterfaces` (see Kalaha and Worm). In Setups, set `"type": "interface"` or `"interface-p2p"` on the joinable entry.

When the page is ready, the match sends settings and opponent information. Game messages arrive on `worker.onMessage`; reply with `message.respond(...)`. If the arena adds another worker on the same page, your `workerAdded` callback runs again. When a worker is removed, `worker.onKilled` runs.

Load `InterfaceHelper.js`, register your handlers, then tell the match you are ready:

```javascript
InterfaceHelper.onInit((init, workerAdded) => {
	const settings = init.settings
	const opponents = init.opponents
	workerAdded((worker) => {
		worker.onMessage = (message) => message.respond({/* … */})
		worker.onKilled = () => {/* slot torn down */}
	})
})
InterfaceHelper.signalReady()
```

### Private repositories

Read [here](https://github.com/sponsors/ChrisAcrobat/).

## Arena dependencies

To load libraries (for example physics engines) into an arena, copy the files into the arena repository and list them under `header.dependencies` in `properties.json`. Paths are resolved relative to the arena folder. Dependencies are loaded in listed order before `arena.js` runs.

Object entries are treated as ES modules and wrapped onto the given global `name` unless `"module": false`. Plain string entries are executed as classic scripts.

```json
{
	"header": {
		"dependencies": [
			{ "name": "_cannon", "path": "cannon-es.ext.js" },
			"other/exampleLib.js"
		]
	}
}
```

## Participant file header

The `participant.js` optional file header has to be valid JSON otherwise it is omitted. The header can be placed anywhere in the file, but at the top is recommended as a standardization.

```JavaScript
/**
{}
**/
```

```JavaScript
/**{}**/
```

```JavaScript
/**{
	"example": true
}**/
```

### Participant dependencies

To load libraries into a participant, copy the files to the repository and add them to the file header. The files have to be referenced locally. Dependencies are loaded in listed order.

```JavaScript
/**{
	"dependencies": [
		"exampleLib.js",
		"other/exampleLib.js"
	]
}**/
```

<!-- TODO: Rewrite/uncomment when mutator are a thing.
### Mutators
Mutator are participant functions provided by the arena that does not affect participants execution time. -->

## Special thanks

- engine262<br> Algorithmic Games uses [engine262](https://github.com/engine262/engine262) to run arena and participant code safely and consistently between matches.
- JSON Editor<br> Algorithmic Games uses [JSON Editor](https://github.com/josdejong/jsoneditor/) by [Jos de Jong](https://github.com/josdejong), powered by [Ace (Ajax.org Cloud9 Editor)](https://github.com/ajaxorg/ace/) and [Ajv JSON schema validator](https://github.com/ajv-validator/ajv/), for editing, rendering and validating JSON.
- seedrandom<br> Algorithmic Games uses [seedrandom](https://github.com/davidbau/seedrandom) by [David Bau](https://github.com/davidbau) for overriding `Math.random()` to generate repeatable numbers.

## User written JavaScript

Algorithmic Games runs arena and participant code in an isolated JavaScript environment in your browser. Human interface pages are separate and only exchange messages with the match. This limits what user-written code can reach, but no system is perfect.

If you find a way to break out of the participant isolation and read other people’s data, please [report it](https://github.com/AlgorithmicGames/AlgorithmicGames.github.io/issues/new?title=%5Bsecurity-hole%5D%20_Short_description_&body=How%20to%20reproduce:%0A1.%20First...%0A2.%20Then...)! Confirmed reports are listed on the [honorable mentions](https://Algorithmic.Games/Community/HonorableMentions/) page once the issue is fixed.

# Post scriptum

If Algorithmic Games happens to be used in any scientific research, please do tell if something is published! 😃

If you have any doubts, you can [request permission here](https://github.com/AlgorithmicGames/AlgorithmicGames.github.io/issues/new?title=%5Bpermission-request%5D%20_Short_description_&body=Am%20I%20allowed%20to...%20?)<!-- or contact [E-MAIL ADDRESS PENDING]. -->.
