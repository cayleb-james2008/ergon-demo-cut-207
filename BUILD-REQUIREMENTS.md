# BUILD REQUIREMENTS — the 7 NEEDS BUILD scenes (Ticket 206 / m-0338, film editor)

**These are build requirements, not footage. They are NOT in the cut.** The delivered film
(`ergon-demo-cut-6m20.mp4`) contains only the 14 FILMABLE NOW scenes. Each row below names the scene
that cannot be filmed today, the missing piece from the ticket's readiness record, and what must be
built before the scene can be shot as a real end-to-end run — no staging, no mocking, no faked call,
no voice where no speech-to-text exists.

Provenance: scene ids, titles and per-scene gaps follow `work/worker-1/SCENE-PACKAGE.md` §5, derived
from the ticket contract (Slack ts `1794496083.339809`) and the graded artefact record named there.
The ticket lists five missing-piece phrases across seven scenes; rows 19 and 20 carry the ticket's
`phone cannot reach a live backend` phrase and the derived specific gap is named after the em dash
(the package marks both as DERIVED, not quoted from the readiness record).

| Scene | Act | Title | Missing piece | Build requirement |
|---|---|---|---|---|
| 05 | Act 1 Setup | Your agent in your pocket, live | phone cannot reach a live backend | A hosted Ergon API + agent runtime reachable over the network from the real phone client, with phone authentication as the employee and the client wired to it. Done when the phone completes a real thread turn against the hosted backend. |
| 08 | Act 2 One warehouse day | Say it, don't type it | no speech-to-text | On-device or hosted speech-to-text feeding the composer, with the transcript shown and editable before send. Done when a spoken request produces the same flow as the typed one, with the STT engine and model named. |
| 10 | Act 2 One warehouse day | The warehouse board on main | warehouse board not on main | Merge the warehouse board into the product main build so one build/serve command produces app and board from main, one manifest binds both, and the in-app board loads the same-build board behind the app's auth. Done on a cold checkout of main. |
| 12 | Act 3 What everyone else sees | The crew's Tasks inbox | no Tasks inbox | A shared crew Tasks inbox on top of the owner's decision inbox: jobs assigned to a crew land as tasks a crew member can see and act on (accept, comment, complete), on demo identities. Done when a second demo identity acts on an assigned job and the owner side reflects it. |
| 14 | Act 3 What everyone else sees | A real call | calling is legacy Twilio only | The product's calling capability on the current stack — a live outbound call placed by the agent with call control and outcome capture, replacing the legacy Twilio-only path, on a consented test line. Done when the agent places a live call and the outcome is written back to the job card. |
| 19 | Act 4 Capabilities | The agent keeps working | derived: no live agent runtime — the agent does not keep working between sessions, and tasks never complete by themselves | A hosted agent runtime plus a task-advance loop so queued work progresses while the window is closed and tasks complete without the owner's sign-off, with notifications. Done when the app is closed, the runtime completes a queued task, and the reopened app shows the new state with a real timestamp. |
| 20 | Act 4 Capabilities | Authority is real | derived: no backend behind a grant or a decision — a granted scope is a label, and a decision reaches nothing outside the browser | Server-side scope enforcement plus an immutable decision audit trail: an approved grant actually gates a real API call (allowed in scope, refused out of scope), every decision is written to the trail, and the app shows the server's confirmation including failure states. Done when approve → allow → out-of-scope-refuse is recorded from the server. |

## What "built" means for the ticket's single outcome

The seven scenes are ordered by dependency, not by film position. 05, 19 and 20 need one thing first:
**a live backend/runtime the shipped client can reach** (today every reply comes from a named fixture
engine and all state is one `localStorage` record). 12 and 20 then need the server to own tasks and
scope decisions. 10 is an independent build/serve merge. 08 is an independent model integration.
14 is an independent telephony integration, and it is the one row that must **not** keep the
"Simulated call" label once built — a real call is labelled as a real call.

**Acceptance overflow into the film:** when any row is built, its scene is re-shot as one continuous
take of the real flow and re-cut into the film; the build-requirements row is then struck and the
scene moves to the FILMABLE column. Until then the film's end card says 7 scenes are build
requirements and this file is the list.
