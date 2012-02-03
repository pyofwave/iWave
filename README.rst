iWave ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
=====

Notices
-------

This repository was created to plan the eventual creation of this project and so hackers can can get started before I'm ready. 

PyOfWave wants to encourage decentralization, so while we may create this project as a reference, we won't create any other clients ourselves but encourage others to do it.

Planning allows me & others a feel for where we're headed, but requires leniency for change. 

Getting Started
---------------

Initial work that requires doing is the artwork (I'll ask for a sea theme which fits well with Apple & Wave):

- backdrops (should be unobtrusive, super realistic, & in iPad stylistics)

  Specific desired backdrops:

  - Linen (provided by iOS, default)
  - waves (for theme & welcome stream)

- alerts

  - duplicate iOS alerts
  - "surf" (default)

- ringtones (waves can be set to use this instead)

  - duplicate iOS ringtones
  - "ocean waves" (default)

- app icon
- UIToolbar backdrops

  Specifically:

  - Pages-like "parchment" (for edit)
  - Mediterranean wave pattern "waves" (for welcome)

Overview
--------

iWave is a high quality native Wave client for iPad, and eventually iPhone/iPod Touch with high integration into iOS. The use of the i naming scheme is meant to bring together various charactoristics of Apple products namely iPad (platform), Mail (communicating), and the now obsolete iWeb (authoring). 

While iWave is iOS specific, it will use a custom XML system (to translate XML elements into visual system objects) so it can be used as a starting point in creating other clients. 

I still want iWave to work on iOS4 because I can't make a decent web client for that version (due to lack of content-editable. 

UI
--

iWave plans to appear simalor to Mail, but with the (limited) complexity moved to the structure of waves. It's editing mode will appear like iWork while playback will appear like Movies. The whole design will center around the HID Wave Representation described in the PyOfWave repository.

The goal is to be so consistant with the native applications the user will already know how to use iWave. 

Architecture
------------

I'm currently planning that iWave will hold for an engine:

- XMPP system
- XML to XML to UIView objects translation system with "modes"
- An index of View Controllers

Dependancies
------------

I plan to use in iWave:

- RSully/RSColorPicker
- enormego/EGOTextView
- AlanQuartermain/AQGridView
- Libstrophe --xmppframework (either that or custom)-- (only allows for receiving basic stanzas)
- Webkit/JavaScriptCore compilation by iOS Impact
