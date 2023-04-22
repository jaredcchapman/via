# via

Simple cli tools for expert writers, written in Rust.

Rough draft of modules + pseudocode here: https://github.com/jaredcchapman/via/blob/main/module-spec.md

## Designed for experts

A writer has many tasks: gather, arrange, compose, edit. These tasks require flexible focus and an eye to determine which move the writing forward. And which are mere distraction.

Expert writers understand this. (Amateurs do not.) 

The expert values preparation and order. Arranges his material and tools, like a chef, mise en place. Determines the task to work on and fits tool to task to completion. Consistently. (The amateur, expert at distraction, does not.)

Via assists the expert gather, arrange, compose and edit his material. Concept to manuscript.

Once complete export as `.txt`  and convert to the format necessary for publication. On to the next one. (Amateurs worry most about this step. Most never reach it.)

## Designed to last

Via is designed to be clear and accessible. Not cryptic and insufferable.

Via is not puritanical. The minimalist parent of plethora "distraction-free" apps.

Via is not extensible. The maximalist progenitor of feature-bloat absurdity.

This sidesteps the many myths and malpractices of the copy swamp and keeps its userbase concise and elite. (For everyone else there's ChatGPT.)



## Overview

**User**: Create, read, update delete Databases.

**Database**: Create, read, update delete Docs and Blocks in a graph database.

**Doc**: Collection of Blocks arranged in a Tree Heirarchy. Has unique ID.

**Block**: Base unit of via. String of text. Has unique ID.

**Backlink**: References unique ID of Doc [[Doc Ref]] and Block ((Block Ref)). 

```
via - Main view

+INDEX-----+COMPOSER----- +QUEUE---|
|~ALL      |-Doc          |-Block  |
| ~Doc     | -Block       | -Child |
|*STAR     |  -Child      |+Block..|
| *Doc     |+Block ...    |        |
|#ARCHIVE  |-Block with   +PROMPT--|
| #Doc     | a [[Doc Ref]]|dd-mm-yy|
|!TRASH    |-Block with   |-Block  |
| !Doc     | a ((Blk Ref))|:command|
+-CONDUCTOR---------------+--------+
|@USR/ DB/ Doc / Block... |...    >|
------------------------------------ 
``` 

**Index**: Create, read, update, delete Docs in current Database.

**Composer**: Create, read, update, delete blocks in current Doc tree.

**Queue**: Read, update, delete existing Blocks from multiple locations, ad hoc. Arranged in order queued.

**Prompt**: Create, read, and delete immutable blocks. Arranged in order created.

**Conductor**: Navigate, Search and execute Commands.
