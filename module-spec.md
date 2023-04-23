# 0. Main Module

Obligatory ascii ui diagram

```
via - Main view

+INDEX-----+COMPOSER----- +QUEUE---|
|~ALL      |-Doc          |-Block  |
| ~Doc     | -Block       | -Child |
|*STAR     |  -Child      |+Block..|
| *Doc     | +Block ...   |        |
|#ARCHIVE  | -Block with  +PROMPT--|
| #Doc     |  [[Doc Ref]] |dd-mm-yy|
|!TRASH    | -Block with  |-Block  |
| !Doc     | ((Blk Ref))  |:command|
+-CONDUCTOR---------------+--------+
|@USR/ DB/ Doc / Block... |...    >|
------------------------------------ 
``` 

```rust
mod main {
    fn main() {
        // initialize the database
        let database = Database::new();

        // initialize the UI controller
        let aperture = Aperture::new();

        // initialize the editor
        let editor = Editor::new();

        // initialize the conductor
        let conductor = Conductor::new();

        // initialize the user account and settings
        let user = User::new();

        // initialize the index
        let index = Index::new(database);

        // initialize the prompt ledger
        let prompt_ledger = PromptLedger::new();

        // initialize the queue
        let queue = Queue::new();

        // run the main event loop
        aperture.get_input_stream()
            .map(|input| conductor.parse_input(input))
            .map(|result| match result {
                Ok(command) => command.execute(),
                Err(error) => Err(error.to_string()),
            })
            .map(|result| aperture.display_output(result.unwrap_or_else(|error| error)))
            .for_each(drop);
    }
}
```

## 1. User: CRUDs User Account and Settings

```rust
// MODULE: USER

// struct to represent a user's account
struct UserAccount {
    id: u32,                // unique identifier for the user account
    name: String,           // name of the user
}

// struct to represent user settings
struct UserSettings {
    font_size: u8,          // preferred font size for the editor
    theme: String,          // preferred theme for the editor
    language: String,       // preferred language for the editor
    // add any additional settings here
}

// function to create a new user account
fn create_user(name: String, email: String, password: String) -> UserAccount {
    // validate input and generate unique id
    // hash password and store new user account in database
}

// function to read user account information
fn read_user(id: u32) -> UserAccount {
    // retrieve user account from database and return it
}

// function to update user account information
fn update_user(id: u32, updates: UserAccount) -> UserAccount {
    // retrieve user account from database
    // update specified fields and save changes
    // return updated user account
}

// function to delete user account
fn delete_user(id: u32) -> bool {
    // retrieve user account from database
    // delete user account from database and return success/failure status
}

// function to read user settings
fn read_settings(id: u32) -> UserSettings {
    // retrieve user account from database
    // return settings object from user account
}

// function to update user settings
fn update_settings(id: u32, updates: UserSettings) -> UserSettings {
    // retrieve user account from database
    // update settings fields and save changes
    // return updated settings object
}
```


## 2. Editor

Robust text editor with full keyboard and mouse support and advanced functions: autocompletions, autowraps, multicursor

```rust
// MODULE: EDITOR

// struct to represent the editor
struct Editor {
    cursor_pos: (usize, usize),   // current cursor position (row, column)
    text: String,                // full text content of the editor
    selected_text: Option<String>, // optional selected text in the editor
    settings: EditorSettings      // settings object for the editor
}

// struct to represent editor settings
struct EditorSettings {
    font_size: u8,              // font size of the editor
    theme: String,              // color scheme of the editor
    language: String,           // programming language of the text (if applicable)
    // add any additional settings here
}

// function to create a new editor instance
fn create_editor() -> Editor {
    // create new editor object with default settings and empty text
}

// function to read editor content
fn read_text(editor: &Editor) -> String {
    // return full text content of the editor
}

// function to update editor content
fn update_text(editor: &mut Editor, new_text: String) {
    // update text content of the editor with new text
}

// function to read selected text
fn read_selected_text(editor: &Editor) -> Option<String> {
    // return optional selected text in the editor (if any)
}

// function to update selected text
fn update_selected_text(editor: &mut Editor, new_selected_text: Option<String>) {
    // update selected text in the editor with new selected text (if any)
}

// function to read cursor position
fn read_cursor_pos(editor: &Editor) -> (usize, usize) {
    // return current cursor position in the editor
}

// function to update cursor position
fn update_cursor_pos(editor: &mut Editor, new_pos: (usize, usize)) {
    // update cursor position in the editor with new position
}

// function to read editor settings
fn read_settings(editor: &Editor) -> EditorSettings {
    // return settings object for the editor
}

// function to update editor settings
fn update_settings(editor: &mut Editor, new_settings: EditorSettings) {
    // update settings object for the editor with new settings
}
```



## 3. Aperture

UI controller that hides and reveals parts of the UI with full keyboard and mouse support

```rust
// MODULE: APERTURE

// struct to represent the UI controller
struct UIController {
    focus: Option<UIElement>,   // currently focused UI element (if any)
    hidden_elements: Vec<UIElement>, // list of hidden UI elements
    revealed_elements: Vec<UIElement> // list of revealed UI elements
}

// enum to represent UI elements
enum UIElement {
    Editor,     // text editor component
    Sidebar,    // sidebar component
    Menu,       // menu component
    // add any additional UI elements here
}

// function to hide a UI element
fn hide_element(controller: &mut UIController, element: UIElement) {
    // hide the specified UI element and add it to the hidden_elements list
}

// function to reveal a UI element
fn reveal_element(controller: &mut UIController, element: UIElement) {
    // reveal the specified UI element and add it to the revealed_elements list
}

// function to set focus on a UI element
fn set_focus(controller: &mut UIController, element: UIElement) {
    // set the specified UI element as the currently focused element
}

// function to remove focus from a UI element
fn remove_focus(controller: &mut UIController) {
    // remove focus from the currently focused UI element
}

// function to toggle the visibility of a UI element
fn toggle_visibility(controller: &mut UIController, element: UIElement) {
    // if the specified UI element is hidden, reveal it, and vice versa
}

// function to get the currently focused UI element
fn get_focused_element(controller: &UIController) -> Option<UIElement> {
    // return the currently focused UI element (if any)
}

// function to get a list of all hidden UI elements
fn get_hidden_elements(controller: &UIController) -> Vec<UIElement> {
    // return a list of all hidden UI elements
}

// function to get a list of all revealed UI elements
fn get_revealed_elements(controller: &UIController) -> Vec<UIElement> {
    // return a list of all revealed UI elements
}
```



## 4. Conductor 

Navigate, Search, Commands

```rust
// MODULE: CONDUCTOR

// function to navigate between UI elements
fn navigate(controller: &mut UIController, direction: NavigationDirection) {
    // navigate to the next or previous UI element in the specified direction
}

// enum to represent the navigation direction
enum NavigationDirection {
    Forward,    // navigate forward
    Backward    // navigate backward
}

// function to search for text in the document
fn search(text: &str) {
    // search for the specified text in the document
}

// function to execute a command
fn execute_command(command: &str) {
    // execute the specified command
}
```



## 5. Database

CRUDs Doc and Block nodes Backlined in a graph database

```rust
// MODULE: DATABASE

// struct to represent the graph database
struct GraphDatabase {
    nodes: Vec<Node>,   // list of nodes in the database
    edges: Vec<Edge>    // list of edges in the database
}

// struct to represent a node in the database
struct Node {
    id: u64,    // unique identifier for the node
    data: Block,    // the block of text associated with the node
}

// struct to represent an edge in the database
struct Edge {
    from_node_id: u64,  // the ID of the node the edge starts from
    to_node_id: u64,    // the ID of the node the edge goes to
}

// struct to represent a block of text
struct Block {
    id: u64,        // unique identifier for the block
    text: String,   // the text content of the block
    children: Vec<Block>,   // list of child blocks (if any)
}

// function to create a new node in the database
fn create_node(database: &mut GraphDatabase, data: Block) -> Node {
    // create a new node with the specified block of text and add it to the database
}

// function to read a node from the database
fn read_node(database: &GraphDatabase, node_id: u64) -> Option<Node> {
    // return the node with the specified ID (if it exists)
}

// function to update a node in the database
fn update_node(database: &mut GraphDatabase, node_id: u64, data: Block) -> Option<Node> {
    // update the node with the specified ID with the new block of text (if it exists)
}

// function to delete a node from the database
fn delete_node(database: &mut GraphDatabase, node_id: u64) -> Option<Node> {
    // delete the node with the specified ID (if it exists) and all edges associated with it
}

// function to create a new edge in the database
fn create_edge(database: &mut GraphDatabase, from_node_id: u64, to_node_id: u64) -> Edge {
    // create a new edge from the node with the from_node_id to the node with the to_node_id and add it to the database
}

// function to read an edge from the database
fn read_edge(database: &GraphDatabase, from_node_id: u64, to_node_id: u64) -> Option<Edge> {
    // return the edge from the node with the from_node_id to the node with the to_node_id (if it exists)
}

// function to delete an edge from the database
fn delete_edge(database: &mut GraphDatabase, from_node_id: u64, to_node_id: u64) -> Option<Edge> {
    // delete the edge from the node with the from_node_id to the node with the to_node_id (if it exists)
}

// function to get all the nodes in the database
fn get_all_nodes(database: &GraphDatabase) -> Vec<Node> {
    // return a list of all nodes in the database
}
```



## 6. Backlink

Relates nodes in the Database (aka an edge)

```rust
mod backlink {
    struct Backlink {
        source_node_id: NodeId,
        target_node_id: NodeId,
        link_type: LinkType,
        metadata: Option<String>,
    }

    enum LinkType {
        Ref,
        Quote,
        Comment,
    }

    impl Backlink {
        fn create(source_node_id: NodeId, target_node_id: NodeId, link_type: LinkType, metadata: Option<String>) -> Result<Self, Error> {
            // create a new backlink
        }

        fn read_by_node_id(node_id: NodeId) -> Result<Vec<Self>, Error> {
            // read all backlinks associated with the given node id
        }

        fn update_metadata(&mut self, metadata: Option<String>) -> Result<(), Error> {
            // update the metadata associated with the backlink
        }

        fn delete(&self) -> Result<(), Error> {
            // delete the backlink
        }
    }
}
```

## 7. Block

Single string of text with unique ID; CRUDs text and Backlinks; Each block is a subtrees that Updates it's children.

```rust
mod block {
    struct Block {
        id: BlockId,
        text: String,
        backlinks: Vec<Backlink>,
        children: Vec<Block>,
    }

    impl Block {
        fn create(text: String, parent_id: BlockId) -> Result<Self, Error> {
            // create a new block and add it as a child to the parent block with the given id
        }

        fn read(id: BlockId) -> Result<Self, Error> {
            // read the block with the given id
        }

        fn update_text(&mut self, new_text: String) -> Result<(), Error> {
            // update the text associated with the block
        }

        fn add_child(&mut self, child: Block) -> Result<(), Error> {
            // add a new child block to the block's children list
        }

        fn remove_child(&mut self, child_id: BlockId) -> Result<(), Error> {
            // remove the child block with the given id from the block's children list
        }

        fn add_backlink(&mut self, backlink: Backlink) -> Result<(), Error> {
            // add a new backlink to the block's backlinks list
        }

        fn remove_backlink(&mut self, backlink_id: BacklinkId) -> Result<(), Error> {
            // remove the backlink with the given id from the block's backlinks list
        }

        fn get_subtree(&self) -> Vec<Block> {
            // return the block's subtree (all of its children and their children, recursively)
        }

        fn get_ancestors(&self) -> Vec<Block> {
            // return the block's ancestors (all of its parent blocks, recursively)
        }
    }
}
```

## 8. Doc

Collection of Blocks with unique ID; CRUDs its blocks in a Tree Heirarchy; Each Block is a subtree

```rust
mod doc {
    struct Doc {
        id: DocId,
        blocks: Vec<Block>,
        parent_id: Option<DocId>,
        children_ids: Vec<DocId>,
    }

    impl Doc {
        fn create(blocks: Vec<Block>, parent_id: Option<DocId>) -> Result<Self, Error> {
            // create a new doc with the given blocks and parent id (if any)
        }

        fn read(id: DocId) -> Result<Self, Error> {
            // read the doc with the given id
        }

        fn update_blocks(&mut self, new_blocks: Vec<Block>) -> Result<(), Error> {
            // update the blocks associated with the doc
        }

        fn add_block(&mut self, block: Block) -> Result<(), Error> {
            // add a new block to the doc's blocks list
        }

        fn remove_block(&mut self, block_id: BlockId) -> Result<(), Error> {
            // remove the block with the given id from the doc's blocks list
        }

        fn add_child(&mut self, child_id: DocId) -> Result<(), Error> {
            // add a new child doc to the doc's children list
        }

        fn remove_child(&mut self, child_id: DocId) -> Result<(), Error> {
            // remove the child doc with the given id from the doc's children list
        }

        fn get_subtree(&self) -> Vec<Block> {
            // return the doc's subtree (all of its blocks and their children, recursively)
        }

        fn get_ancestors(&self) -> Vec<Doc> {
            // return the doc's ancestors (all of its parent docs, recursively)
        }
    }
}
```

## 9. Index

CRUDs all Doc Entries, Titles, and Status in current Database; Orders Docs into tagged subtrees: `~All`, `*Star`, `#Archive`, `!Trash`.

```rust
mod index {
    struct Index {
        docs: Vec<Doc>,
    }

    impl Index {
        fn create(docs: Vec<Doc>) -> Result<Self, Error> {
            // create a new index with the given docs
        }

        fn read() -> Result<Self, Error> {
            // read the current index
        }

        fn update_doc(&mut self, doc: Doc) -> Result<(), Error> {
            // update the given doc in the index
        }

        fn add_doc(&mut self, doc: Doc) -> Result<(), Error> {
            // add a new doc to the index
        }

        fn remove_doc(&mut self, doc_id: DocId) -> Result<(), Error> {
            // remove the doc with the given id from the index
        }

        fn get_doc(&self, doc_id: DocId) -> Option<Doc> {
            // get the doc with the given id from the index (returns None if not found)
        }

        fn get_all_docs(&self) -> Vec<Doc> {
            // return all of the docs in the index
        }

        fn get_tagged_docs(&self, tag: Tag) -> Vec<Doc> {
            // return all of the docs in the index that have the given tag
        }

        fn get_starred_docs(&self) -> Vec<Doc> {
            // return all of the docs in the index that are starred
        }

        fn get_archived_docs(&self) -> Vec<Doc> {
            // return all of the docs in the index that are archived
        }

        fn get_trashed_docs(&self) -> Vec<Doc> {
            // return all of the docs in the index that are in the trash
        }
    }
}
```

## 10. Queue

CRUDs "when queued" Positions in Queue Register; Queue to add a Block (with children) to next position in Queue Register; Unqueue to remove block from Queue Register; Blocks are queued ad hoc: from one or multiple Docs; Queuing does not move a Block from its Doc of origin; Queued Blocks retain normal block behavior.

```rust
mod queue {
    struct Queue {
        register: Vec<BlockId>,
    }

     impl Queue {
        fn create() -> Result<Self, Error> {
            // create a new empty queue
        }

        fn read() -> Result<Self, Error> {
            // read the current queue
        }

        fn add_block(&mut self, block_id: BlockId) -> Result<(), Error> {
            // add a new block to the end of the queue
        }

        fn remove_block(&mut self, block_id: BlockId) -> Result<(), Error> {
            // remove the given block from the queue
        }

        fn move_block(&mut self, block_id: BlockId, position: usize) -> Result<(), Error> {
            // move the given block to the given position in the queue
        }

        fn get_next_block(&mut self) -> Option<BlockId> {
            // return the next block in the queue (and remove it from the queue)
        }

        fn get_all_blocks(&self) -> Vec<BlockId> {
            // return all of the blocks in the queue
        }

        fn clear(&mut self) -> Result<(), Error> {
            // remove all blocks from the queue
        }
    }
}
```

## 11. Prompt

Creates, Reads, Deletes childless, immutable Blocks in Prompt Ledger; Orders Blocks under "Day Created" subtrees; Blocks here are not subtrees, do not have children. Input with `:` command prefix will execute commands from Conductor Module.

```rust
mod prompt {
    struct PromptLedger {
        blocks: Vec<Block>,
    }

    impl PromptLedger {
        fn create_block(&mut self, content: String) -> Result<(), Error> {
            // create a new immutable block with the given content and add it to the ledger
        }

        fn read_block(&self, block_id: BlockId) -> Result<Block, Error> {
            // return the block with the given ID from the ledger
        }

        fn delete_block(&mut self, block_id: BlockId) -> Result<(), Error> {
            // delete the block with the given ID from the ledger
        }

        fn get_all_blocks(&self) -> Vec<Block> {
            // return all blocks in the ledger, ordered by "day created"
        }

        fn execute_command(&self, input: String) -> Result<(), Error> {
            // execute the command indicated by the given input
        }
    }
}
```

## 12. BONUS: viasync.com

Stripped down, wicked fast web-repo to backup and sync local via database.

- **Private**: Fully encrypted. No peeping-tom cloud.
- **Automatic**: No git push-pull. 
- **Read-Only**: Only views `.txt` files (except for Prompt).
- **Prompt**: Live version of Prompt tool. Capture notes quickly, on the go. Work on them when you get home.

### -- END --
