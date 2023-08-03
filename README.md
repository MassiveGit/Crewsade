# Crewsade
DnD Campaign helper - tool to create and maintain character sheets, campaign notes, and record of NPCs etc

## Initial thoughts:

I could try creating a basic front-end before worrying about persistence, that might allow quicker organic growth without being locked into a particular db structure.

It's unlikely I'll use this during the actual gameplay, unless I'm playing remotely (Ant's new campaign will be remote, as Vera (nee' Finn) is in Bolivia, Nat is in the mines, and Ant is in Auckland, so this isn't beyond reason).
Because of this, "quick" note-taking or use in-game is not a major concern. 
This is more for use as a record of game/character state that tracks changes over each session.
Core features:

Character record - contains main stats and description, stats can change - maybe tie them to a session record. So each time I want to update the character, I create a new session, and that allows: 
NPC adds, NPC deaths, Character changes/deaths, New Character creation (on the off chance...), story updates (new journal entry), notes/thoughts (tied to journal entries).

NPC Record

Session notes/Character Journal

For a first time user, what is base flow? Hrm:

1. Login (implement MVP for this - hardcode login credentials. Can look at creating a proper login a la Trakit later).
2. one button: "Start Campaign" (if campaign already exists against account, then two more options: "New Session" and a second panel showing the latest session stats/notes)
3. When clicked, prompts to name campaign, and give description. 
4. User now on basic Campaign page. Has buttons to create basic character sheet (choose class, race, etc.) (if none exists), update character (if exists), update Campaign name/desc.
5. Once complete, Campaign page has "new session" button
6. New session button creates a new session (optionally nameable), and allows adding journal notes, adding NPCs (name + description + optional location met), and updating character (level or stats).

Any change made inside a "new session" is linked to that session. User can view individual sessions and should see character/journal/npc etc state as it was during that session.
This could be done by utilising GIT itself - e.g. when new campagin is created, it creates a new git repo, and new sessions are saved as commits with a specific name format. Then the Session viewer just checks out a given commit/tag.


Git might be overkill. The states that need to be saved are mostly independent (e.g. journal entries and notes), and the ones that aren't could be added as new db rows.
e.g. for character attributes, which may or may not change each session:

1. Inital creation. New db row in char_attrib table with values for each attrib and maybe a link to a campaign_id 0 and a link to a session_id 0. 
2. User updates character outside of a new session. THis creates new char_attrib row with link to campaign and link to session_id 0
3. User creates new session and updates character. New char_attrib row created with session_id 1.
4. User creates new session and does NOT update character. hrm. Maybe session links to the correct character version instead of other way? So session 0 links to char_version 0, Session 1 links to char_version 1, and session 3 links to char_version 1 also?


