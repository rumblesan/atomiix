# Architecture

This document should hopefully serve to give a good overview of how the various bits of Atomiix fit together and talk to each other.

Essentially there are three main parts :-

* The language processor
* The Atom editor
* The SuperCollider audio engine

The structure can be roughly broken down as follows :-

* Atom takes lines of code, selected by the user, and passes them to the language processor
* The language processor parses and interprets those lines and returns some number of actions
* Those actions will either be Audio actions or Editor actions
* Audio actions will be converted to OSC messages and sent to SuperCollider by Atom
  - This could be a new agent score to play, or freeing an existing agent.
* Editor actions will be handled by Atom
  - This could be modifying the score text of an agent in the editor.
* In some cases SuperCollider will send OSC messages to Atom
  - An agent finishing its repeats, or a callback firing.
* These will be converted into Inbound actions and handled by the language processor

## Actions

### Editor Actions

#### MarkText

Create a group of one or more marked sections of text in Atom. This is primarily so that further editor actions can update them. The editor is responsible for making sure that these Marks track the same section of text, even if it moves.

Groups are currently just the most recently active agent line and the marks specify the agent name and the pattern part of the score string.

#### UnmarkText

Remove a mark group, primarily used when freeing an agent.

#### ReplaceText

Replace the text in one or more sections of a marked group.

#### ReplaceLine

Replace an entire line with the given new string. Used with the `grid` command for example.

#### DisplayInfo

Will be used to get the editor to display help and info text.

#### DisplayAgentState

Style the line containing an agent

#### FlashMarkedText

Temporarily highlight a line. Primarily for `future` commands triggering.


### Audio Actions

If these are being sent to SuperCollider then they will be turned into OSC messages by Atom.

#### AgentMethod

Run the specified method against an agent. e.g. `shake jimi`

#### FreeAgent

Free an existing agent.

#### NapAgent

Mute/sleep an agent but don't free it.

#### AddAgentFX

Add effects to an agent. Can handle multiple effects.

#### RemoveAgentFX

Remove the listed effects from an agent. Will remove all effects if the list is empty

#### SetAgentAmplitude

Set the amplitude of an agent.

#### SetTempo

Set the global tempo.

#### FutureCallback

Register a callback with SuperCollider. After the specified amount of time it will respond, returning the given callbackId and the number of remaining times the callback will be triggered.

#### PlayPercussiveScore

Play a percussive score for the specified agent.

#### PlayMelodicScore

Play a melodic score for the specified agent.

#### PlayConcreteScore

Play a concrete score for the specified agent.

### Inbound Actions

These are actions that will be sent from the audio engine to the language interpreter. If it's SuperCollider sending them, then it will be necessary for Atom to convert these from OSC messages.

#### AgentFinished

If an agent has a finite number of repeats, then this will be sent when it finishes.

#### CallbackTriggered

Sent when a callback timer is up.

#### AgentStateChange

Sent if an agents state changes. Sleeping to waking for example.
