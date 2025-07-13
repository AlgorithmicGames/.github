# Algorithmic Games
[Algorithmic Games](https://Algorithmic.Games/) is a platform for competitive programming and match making between algorithms. Users can make their own participates to compete in any of the existing arenas, or make their own custom arena and challenge other users to join. Algorithmic Games was previously know as "AI-Tournaments", where "_AI_" in the name refers to playing against the computer on old video games, like "_Hard AI_" or "_Hard CPU_".
<!-- Other platforms:
// LinkedIn
Algorithmic Games is a platform for competitive programming and match making between algorithms. Users can make their own participates to compete in any of the existing arenas, or make their own custom arena and challenge other users to join. First prototype was done some time before 2016, but all source history from that time is lost. In 2020 a new fresh start took place.
-->

Algorithmic Games in an early prototype stage. See the section [Participate](#Participate) if you want to join a arena, then analyze how other have solved the arena until better documentation has been written.
## Community
If you want to you join the discussions, head on over to the <a href="https://algorithmic.games/Community/Official/" target="_blank">Community handbook</a> and read where we are.

## Participate
To participate in a Arena you need to [create a public GitHub repository](https://github.com/AlgorithmicGames/Participant-Template) and apply three topics: `Algorithmic-Games`, `Algorithmic-Games-Participant` and the full repository name of the arena (`ExampleAuthor--ExampleArena`). The repository also has to have a file in root called `participant.js`, this is the file that will be called to the arena. The repository's name will represent the participants name, except if it starts with `Algorithmic-Games-Participant-` then that part is omitted.
### Private repositories
Currently not supported.
<!-- Keep in sync [START] -->
<!-- 👆 When supported. -->
<!-- https://github.com/AlgorithmicGames/.github/blob/main/profile/README.md -->
<!--
Participating with private repositories is only available to monthly [sponsors](https://github.com/sponsors/ChrisAcrobat) and selected members only due to the extra backend cost. Add [Algorithmic Games participant](https://github.com/apps/algorithmic-games-participant) to your repository to unlock the feature.<br>
Note that you can always use any participant source in the [Develop environment](#develop-environment) without sponsorship.
-->
<!-- Keep in sync [END] -->

### Develop environment
<i>For both developing arenas and participants.</i><br>
Supported console logs:
- log
- warn
- error
- info
- debug
- table

In [Local development setups](https://Algorithmic.Games/Dev/) you can add the URLs to the arena (`arena.js` along with the arenas replay page) and participants to test with before publishing them in GitHub.

<b>Explanation</b>
| Key | Description | Example |
| --- | --- | --- |
| arena.url | URL to a arena.<br>⚠️ Do not include `arena.js`. | `"http://127.0.0.1:8080/Community-Arena/"` or `"https://raw.githubusercontent.com/AlgorithmicGames/Worm-Arena/main/"` |
| arena.name<br><i>Optional</i> | Displayed name.<br>Name defaults to URL if left empty. | `"New-Community-Arena"` |
| arena.replay | URL to replay view. | `"http://127.0.0.1:8080/Community-Arena-Replay/"` |
| arena.settings<br><i>Optional</i> | Prefigured settings. | `{"general":{"seed":"example"}}` |
| participants | Adds participants.<br>Array with either a url string to script or a JSON object per participant. | `["http://127.0.0.1:8080/Community-Arena-Test-Participants/participant-1.js",{"url":"http://127.0.0.1:8080/Community-Arena-Test-Participants/participant-2.js","name":"Temp-Participant","team":1}]` |

The development environment also includes some extra dials and features to help with quality assurance.

#### Participant
Participant's URLs can be written in different forms. An _ordinary_ URL is interpreted in the default sealed sandbox, but URLs that starts with a question mark (`?`) is executed in the browser and can be debugged by the javascript's [`debugger`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/debugger) command. Be aware that results can differ between the sealed sandbox and the browser, much in the same way results can differ between different browser vendors.
#### Interface
If you need more freedom for debugging or would like to train a neural network you should investigate using an interface, which's URLs starts with a exclamation mark (`!`). The main difference between an [Interface](https://github.com/AlgorithmicGames/Interface-Template) and a [Participant](https://github.com/AlgorithmicGames/Participant-Template) is that interfaces opens up a separate web page and sidestep all participant's restrictions. The main use case for interfaces is to get better insight during a running match, for example by allowing Human vs Participant and even Human vs Human matches.
#### Break before first message
By appending a question mark (`?`) after the first special character (`??` or `!?`) the arena will insert a break point just before the first message is posted to the participant or interface so that JavaScript debuggers can be used to step inside along with the first message.

## File header
The `arena.js` and `participant.js` optional file header has to be valid Json otherwise it is omitted. The header can be placed anywhere in the file, but at the top is recommended as a standardization.
``` JavaScript
/**
{}
**/
```
``` JavaScript
/**{}**/
```
``` JavaScript
/**{
	"example": true
}**/
```
### Dependencies
To load libraries like jQuery and others, copy the files to the repository and add them to the file header. The files has to be referenced locally. The sources are imported assigned order.
``` JavaScript
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
- engine262<br>
Algorithmic Games uses [engine262](https://github.com/engine262/engine262) for sandboxing matches and execute then deterministically.
- JSON Editor<br>
Algorithmic Games uses [JSON Editor](https://github.com/josdejong/jsoneditor/) by [Jos de Jong](https://github.com/josdejong), powered by [Ace (Ajax.org Cloud9 Editor)](https://github.com/ajaxorg/ace/) and [Ajv JSON schema validator](https://github.com/ajv-validator/ajv/), for editing, rendering and validating JSON.
- seedrandom<br>
Algorithmic Games uses [seedrandom](https://github.com/davidbau/seedrandom) by [David Bau](https://github.com/davidbau) for overriding `Math.random()` to generate repeatable numbers.
- Supabase<br>
Algorithmic Games uses Edge Functions by [Supabase](https://github.com/supabase/supabase) for serverless [backend](https://github.com/AlgorithmicGames/Backend).

## Why Source Available?
[Algorithmic Games](https://github.com/AlgorithmicGames) is not Open Source by the [Open Source Initiative's definition](https://opensource.org/docs/osd) but rather [Source Available](https://en.wikipedia.org/wiki/Source-available_software), except were a license that says otherwise is in place. This might change when Algorithmic Games leaves the prototype stage, the decision has not yet been made.
### User written JavaScript
Algorithmic Games executes user written JavaScripts in the web browser, which is usually seen as a security concern ([Cross-site scripting](https://en.wikipedia.org/wiki/Cross-site_scripting)). But the scripts are loaded into a sandbox IFrame and Web Worker to prevent just that. But the concern still remain and that's a fact that should not be hidden, that is why it is instead addressed and displayed publicly here.

But if you do find a way to break out of the sandbox and access client data or other participant scripts, please do [report it](https://github.com/AlgorithmicGames/AlgorithmicGames.github.io/issues/new?title=%5Bsecurity-hole%5D%20_Short_description_&body=How%20to%20reproduce:%0A1.%20First...%0A2.%20Then...)! Reporters of confirmed security holes will get a [honorable mention](https://Algorithmic.Games/Community/HonorableMentions/) once the hole is fixed.
### Scheduled server hosted events
A server-side events with official match results is planned, but until then client-side execution is the only way to run the arenas.
Note that [interfaces](#Interfaces) will not be able or allowed to compete.
### Arenas
The source code for AI-Tournament's [arena executor](https://github.com/AlgorithmicGames/Arena-Manager) and the official arenas are available in order to make it easier to examen the "rules" and come up with optimal strategies. You are basically allowed to do what ever as long as it isn't commercial matches.
### Allowed examples
Download code from Algorithmic Games to ...
- Develop, troubleshooting or train an AI.
- Writing and recording dev-diary or tutorial.
- Have your own internal non-profit tournaments.
- Scientific research.
  - Please do tell if something is published! 😃

Basically anything that gives something back to the community.
### Disallowed examples
- Removing all links and references to Algorithmic Games.
- Setup a commercial competitor to Algorithmic Games.
- Private tournaments for benchmarking user performance.<!-- Contact [E-MAIL ADDRESS PENDING] for solution offering. -->

If you have any doubts, you can [request permission here](https://github.com/AlgorithmicGames/AlgorithmicGames.github.io/issues/new?title=%5Bpermission-request%5D%20_Short_description_&body=Am%20I%20allowed%20to...%20?)<!-- or contact [E-MAIL ADDRESS PENDING]. -->.
