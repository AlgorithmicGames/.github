<!-- Keep in sync [START] -->
<!-- https://github.com/AI-Tournaments/.github/blob/main/profile/README.md -->
<!-- https://github.com/AI-Tournaments/AI-Tournaments.github.io/blob/main/README.md -->
# AI-Tournaments
[AI-Tournaments](https://ai-tournaments.github.io/) is about match making between algorithms. Users can make their own participates to any of the existing arenas, or make their own custom arena and challenge other users to join.

AI-Tournaments in an early prototype stage. See the section [Participate](#Participate) if you want to join a arena, then analyze how other have solved the arena until better documentation has been written.
## Community
Join the official [GitHub](https://github.com/orgs/AI-Tournaments/discussions/) or [Discord](https://discord.gg/jhUJNsN) community. Please read and follow the [community guide lines](https://ai-tournaments.github.io/Community/Guidelines/).
<br>[![Discord banner2](https://discord.com/api/guilds/765291928454823936/widget.png?style=banner2)](https://discord.gg/jhUJNsN)
<!-- Keep in sync [END] -->

<!-- Keep in sync [START] -->
<!-- https://github.com/AI-Tournaments/.github/blob/main/profile/README.md -->
<!-- https://github.com/AI-Tournaments/AI-Tournaments.github.io/blob/main/README.md -->
## Why Source Available?
[AI-Tournaments](https://github.com/AI-Tournaments) is not Open Source by the [Open Source Initiative's definition](https://opensource.org/docs/osd) but rather [Source Available](https://en.wikipedia.org/wiki/Source-available_software), except were a license that says otherwise is in place.
### User written JavaScript
AI-Tournaments executes user written JavaScripts in the web browser, which is usually seen as a security concern ([Cross-site scripting](https://en.wikipedia.org/wiki/Cross-site_scripting)). But the scripts are loaded into a sandbox IFrame and Web Worker to prevent just that. But the concern still remain and that's a fact that should not be hidden, that is why it is instead addressed and displayed publicly here.

But if you do find a way to break out of the sandbox and access client data or other participant scripts, please do [report it](https://github.com/AI-Tournaments/AI-Tournaments.github.io/issues/new?title=%5Bsecurity-hole%5D%20_Short_description_&body=How%20to%20reproduce:%0A1.%20First...%0A2.%20Then...)! Reporters of confirmed security holes will get a [honorable mention](https://ai-tournaments.github.io/Community/HonorableMentions/) once the hole is fixed.
### Scheduled server hosted events
A server-side events with official match results is planned, but until then client-side execution is the only way to run the arenas.
Note that [interfaces](#Interfaces) will not be able or allowed to compete.
### Arenas
The source code for AI-Tournament's [arena executor](https://github.com/AI-Tournaments/Arena-Manager) and the official arenas are available in order to make it easier to examen the "rules" and come up with optimal strategies. You are basically allowed to do what ever as long as it isn't commercial matches.
### Allowed examples
Download code from AI-Tournaments to ...
- Develop, troubleshooting or train an AI.
- Writing and recording dev-diary or tutorial.
- Have your own internal uncommercial tournaments.
- Scientific research.
  - Please do tell if something is published! 😃
- Basically anything that gives something back to the community.
### Disallowed examples
- Removing all links and references to AI-Tournaments.
- Setup a commercial competitor to AI-Tournaments.

If you have any doubts, you can [request permission here](https://github.com/AI-Tournaments/AI-Tournaments.github.io/issues/new?title=%5Bpermission-request%5D%20_Short_description_&body=Am%20I%20allowed%20to...%20?).
<!-- Keep in sync [END] -->
