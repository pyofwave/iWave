API Design
++++++++++

Desired Design
==============

xWave downloads waves as constantly updating XML. iWave needs to translate this to a UIView structure with an editing mode. 

I plan to use XML since I'd need to use it anyways, and for both a change and ease, I'll provide tag based translation with a selection of UIView tags to translate to.

Modes can be extended to include the play and normal modes as well as edit (which needs to focus on a post). They would also include modes within the structure like contrib and search modes. 

The paradigm can be extended further to the master controller (stored XML -> inboxes -> search results) with a slight adjustment to include cells, which would also help with popovers. 

So, all the UI covered by the UI document would be programmed in live XML tag based translation overlayed with modes which are processed between ordinary XML and the UIView translation. 

XML Design
==========

To create the XML engine, we need to know what we need from it. This section explores what components are neccessary. 

View Components
---------------

Wave rendering:

- UIView (provide structure, mostly outputed by "frames") - needs full CALayer properties
- ENTextView (rendering & editing text)
- UIImageView (for rendering icons & participants)
- UIDocumentView (for rendering attachments)

Wave modes:

- Slider (playback)
- Button (all modes)
- title (all modes)

Master & Popovers:

- UITableViewCell (all, structure)
- UIStepper (inspector)

Events
------

These are properties on any view. 

- Popover (VCIndex_name arguments...) - Dominant usage
- Show (xPath) - For tags & replies expand/collapse icons
- target (XML with %s) - Add Participant action
- mode (filename) - For playback & move icons, search, edit action, contributors option
- data (XML request) - for playback slider
- block (names) - for live toggle option

Text View:

- type (XML request with %s) - for edit mode, tags, etc. 
- sel (XML request with %s) - for edit mode
- menu (title : [XML with %x/%y/%i|VCIndex_name arguments...]; ...) - for edit menu

Cells:

- to (VCIndex_name arguments...)

Processing
----------

These tags are neccessary for translating input to the output. 

- tag (name) - Defines a translation for a tag
- out - outputs xPath
- attr (name) - outputs xPath to an attribute of parent
- if (val) - Runs content only if val is true
- import - Loads in contained file name

VCIndex
-------

Native & custom view controllers for the HID display

Options follow name. Options between [ and ] are optional. Ellipses (...) signal a continuation within any type of brackets. | signals an alternative argument. 

- XML fileName [XMLRequest [data...]]
- XMLgrid fileName [XMLRequest [data...]]
- contacts/contact address [selectLabel {value : label; ...} value]
- contacts/select Title [search]
- photos
- prompt VCIndex | { label : VCIndex; ...}
- edit { label : xPath; ...} element
- colorPicker color
- web [search]

These are used as follows (unmentioned cases use XML). ? = dependant on situation.

- Media : prompt { Photos : photos; History : XML complete <fetch:records type="files">%s</fetch:records>; Web : web; Inputs : XMLgrid inputs;}
- Participant : contacts/contact ? Permissions { None : none; View : view; edit : edit; Invite : invite; Manage : manage;} ?
- Add participant : prompt contacts/select "Select User to Join wave"
- (colorPicker used in Inspector)
- (edit used in edit mode, add button of inboxes and edit mode, and welcome screen)
- (postOptions uses XMLgrid -> XMLgrid -> contacts/contact)

Non UI Tasks
============

Apart from rendering UI and table views, iWave will include other tasks which needs to be documented and engined. 

These tasks include:

- Syncing with the Address Book (with 4 options: sync to account, favor iPad, favor account, sync to iPad)
- Sounding alerts when updates are received (and if tagged, display alert)
- Setting up the canvas for the XML view, including:

	- Saving/loading state
	- Preparing UISplitView
	- Defaulting to welcome screen & preparing accounts XML file.

With the exception of the UI setup, we need to ensure that the engine is capable of intercepting responses and in the case of the address book, altering them. 
