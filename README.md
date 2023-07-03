# via - simple cli tools for serious writers

Serious writing involves many tasks: gathering, arranging and editing material.

These tasks require different kinds of attention: gathering is open and exploratory, arranging is insightful and deliberate, editing is closed and decisive.

At any moment the writer must determine which task will move the writing forward and what is mere distraction — then direct their attention to the right material, with the right tool. 

The serious writer understands this. The amateur does not.

Via provides the serious writer with a unified set of simple tools in an interface that adapts to the task at hand: gather, arrange and edit your material — from raw concept to final composition.

# Features

Block: every line of text is a unique block that can reference any other block or doc.

Doc: all blocks live in a doc, but are not limited to that doc.

Database: all docs and blocks live in a graph database.

Index: organizes docs into groups All, Star, Archive, Trash.

Composer: main text editor arranges blocks in a doc as a nested tree.

Prompt: captures notes quickly, like chat, orders them in blocks chronologically.

Queue: queues blocks ad hoc, like a playlist, doesn't matter which doc they're from.

Conductor: Universal search and navigation. Go anywhere. Find anything.

Aperture: Universal toggle that shows or hides anything. Focus on the task at hand.

Note: via's design owes credit to many text editors but is not intended to duplicate productivity or programming paradigms (e.g., zettlekasten, pkm, gtd, vim, emacs etc).

# Technical Overview

## Database

User: Create, read, update delete Databases.

Database: Create, read, update delete Docs and Blocks in a graph database.

Doc: Collection of Blocks arranged in a Tree Heirarchy. Has unique ID.

Block: Base unit of via contains: string of text and Backlinks. Has unique ID.

Backlink: References unique ID of Doc [[Doc Ref]] and Block ((Block Ref)).

via - Main view

+INDEX-----+COMPOSER----- +QUEUE---|
|~ALL      |-Doc          |-Block  |
| ~Doc     | -Block       | -Child |
|*STAR     |  -Child      |+Block..|
| *Doc     | +Block ...   |        |
|#ARCHIVE  | -Block with  +PROMPT--|
| #Doc     |  [[Doc Ref]] |dd-mm-yy|
|!TRASH    | -Block with  |-Block  |
| !Doc     |  ((Blk Ref)) |:command|
+CONDUCTOR----------------+--------+
|@USR/ DB/ Doc / Block... |...    >|
------------------------------------ 

# Interface

Index: Create, read, update, delete Docs in current Database.

Composer: Create, read, update, delete blocks in current Doc tree.

Queue: Read, update, delete existing Blocks from multiple locations, ad hoc. Arranged in order queued.

Prompt: Create, read, and delete immutable blocks. Arranged in order created.

Conductor: Navigate, Search and execute Commands.

Aperture: Show or hide interface elements.