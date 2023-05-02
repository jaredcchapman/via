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
| !Doc     |  ((Blk Ref)) |:command|
+CONDUCTOR----------------+--------+
|@USR/ DB/ Doc / Block... |...    >|
------------------------------------ 
``` 

```rust
fn main() {
    // initialize modules
    let mut user = User::new();
    let mut editor = Editor::new();
    let mut aperture = Aperture::new();
    let mut conductor = Conductor::new();
    let mut database = Database::new();
    let mut backlink = Backlink::new();
    let mut index = Index::new();
    let mut composer = Composer::new();
    let mut queue = Queue::new();
    let mut prompt = Prompt::new();
    
    // start the main loop
    loop {
        // get user input
        let input = get_user_input();
        
        // execute command based on input
        match conductor.execute_command(&input, &mut user, &mut editor, &mut aperture, &mut database, &mut backlink, &mut index, &mut composer, &mut queue, &mut prompt) {
            Ok(output) => {
                // display output to user
                display_output(output);
            }
            Err(error) => {
                // display error to user
                display_error(error);
            }
        }
    }
}
```

## 1. User: CRUDs User Account and Settings

```rust
// MODULE: USER

// Struct representing a User
struct User {
    id: u32,
    name: String,
    email: String,
    password: String,
}

// Implementation of CRUD operations for the User struct
impl User {
    fn create(user: User) -> Result<(), String> {
        // code to create a new user
        Ok(())
    }
    
    fn read(id: u32) -> Result<User, String> {
        // code to read a user by ID
        Err("User not found".to_string())
    }
    
    fn update(user: User) -> Result<(), String> {
        // code to update an existing user
        Ok(())
    }
    
    fn delete(id: u32) -> Result<(), String> {
        // code to delete a user by ID
        Ok(())
    }
}

```


## 2. Editor

Robust text editor with full keyboard and mouse support and advanced functions: autocompletions, autowraps, multicursor

```rust
// MODULE: EDITOR

// Struct representing the Editor
struct Editor {
    buffer: String,
}

// Implementation of Editor functions
impl Editor {
    fn new() -> Self {
        // code to initialize a new Editor
        Editor {
            buffer: String::new(),
        }
    }
    
    fn insert(&mut self, c: char) {
        // code to insert a character into the buffer
    }
    
    fn delete(&mut self) {
        // code to delete the character before the cursor
    }
    
    fn move_cursor_left(&mut self) {
        // code to move the cursor left
    }
    
    fn move_cursor_right(&mut self) {
        // code to move the cursor right
    }
    
    fn move_cursor_up(&mut self) {
        // code to move the cursor left
    }
    
    fn move_cursor_down(&mut self) {
        // code to move the cursor right
    }
    
    fn autocomplete(&mut self) {
        // code to suggest and insert autocompletion
    }
    
    fn autowrap(&mut self) {
        // code to automatically wrap text
    }
}

```



## 3. Aperture

UI controller that hides and reveals parts of the UI with full keyboard and mouse support

```rust
// MODULE: APERTURE

// Struct representing the Aperture
struct Aperture {
    hidden_sections: Vec<bool>,
}

// Implementation of Aperture functions
impl Aperture {
    fn new() -> Self {
        // code to initialize a new Aperture
        Aperture {
            hidden_sections: vec![false; num_sections],
        }
    }
    
    fn toggle_section(&mut self, section_index: usize) {
        // code to toggle the visibility of a section
        self.hidden_sections[section_index] = !self.hidden_sections[section_index];
    }
    
    fn is_section_hidden(&self, section_index: usize) -> bool {
        // code to check if a section is hidden
        self.hidden_sections[section_index]
    }
}

```



## 4. Conductor 

Navigate, Search, Commands

```rust
// MODULE: CONDUCTOR

// Struct representing the Conductor
struct Conductor {
    current_doc_id: Option<u32>,
    cursor_pos: usize,
}

// Implementation of Conductor functions
impl Conductor {
    fn new() -> Self {
        // code to initialize a new Conductor
        Conductor {
            current_doc_id: None,
            cursor_pos: 0,
        }
    }
    
    fn navigate_to_doc(&mut self, doc_id: u32) -> Result<(), String> {
        // code to navigate to a specified document
        Ok(())
    }
    
    fn search(&self, query: &str) -> Vec<u32> {
        // code to search for documents or blocks matching a query
        vec![]
    }
    
    fn execute_command(&self, command: &str) -> Result<(), String> {
        // code to execute a command
        Ok(())
    }
}

```



## 5. Database

CRUDs Doc and Block nodes Backlined in a graph database

```rust
// MODULE: DATABASE
// Struct representing the Database
struct Database {
    nodes: HashMap<u32, Node>,
}

// Struct representing a Node in the Database
struct Node {
    doc_id: Option<u32>,
    block_id: Option<u32>,
    backlinks: Vec<u32>,
}

// Implementation of Database functions
impl Database {
    fn new() -> Self {
        // code to initialize a new Database
        Database {
            nodes: HashMap::new(),
        }
    }
    
    fn get_node(&self, node_id: u32) -> Option<&Node> {
        // code to get a node by its ID
        self.nodes.get(&node_id)
    }
    
    fn create_doc(&mut self, doc_id: u32) -> Result<(), String> {
        // code to create a new document node
        Ok(())
    }
    
    fn create_block(&mut self, block_id: u32, parent_id: u32) -> Result<(), String> {
        // code to create a new block node and link it to its parent node
        Ok(())
    }
    
    fn update_node(&mut self, node_id: u32, new_node: Node) -> Result<(), String> {
        // code to update a node with new data
        Ok(())
    }
    
    fn delete_node(&mut self, node_id: u32) -> Result<(), String> {
        // code to delete a node and all its backlinks
        Ok(())
    }
    
    fn add_backlink(&mut self, source_id: u32, target_id: u32) -> Result<(), String> {
        // code to add a new backlink between two nodes
        Ok(())
    }
    
    fn remove_backlink(&mut self, source_id: u32, target_id: u32) -> Result<(), String> {
        // code to remove a backlink between two nodes
        Ok(())
    }
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

## 10. Composer

```rust
// Struct representing a Composer
struct Composer {
    current_doc_id: u32,
    current_block_id: u32,
}

// Implementation of Composer functions
impl Composer {
    fn new() -> Self {
        Composer { current_doc_id: 0, current_block_id: 0 }
    }
    
    fn set_current_doc(&mut self, id: u32) {
        self.current_doc_id = id;
    }
    
    fn set_current_block(&mut self, id: u32) {
        self.current_block_id = id;
    }
    
    fn get_current_block(&self) -> Option<&Block> {
        self.get_current_doc().and_then(|doc| doc.blocks.get(&self.current_block_id))
    }
    
    fn get_current_doc(&self) -> Option<&Doc> {
        self.index.docs.get(&self.current_doc_id)
    }
}
```

## 11. Queue

CRUDs "when queued" Positions in Queue Register; Queue to add a Block (with children) to next position in Queue Register; Unqueue to remove block from Queue Register; Blocks are queued ad hoc: from one or multiple Docs; Queuing does not move a Block from its Doc of origin; Queued Blocks retain normal block behavior.

```rust
// Struct representing a Queue
struct Queue {
    blocks: Vec<Block>,
}

// Implementation of Queue functions
impl Queue {
    fn new() -> Self {
        Queue { blocks: Vec::new() }
    }
    
    fn add_block(&mut self, block: Block) {
        self.blocks.push(block);
    }
    
    fn remove_block(&mut self, index: usize) -> Result<(), String> {
        if index >= self.blocks.len() {
            return Err(String::from("Index out of range"));
        }
        self.blocks.remove(index);
        Ok(())
    }
    
    fn clear(&mut self) {
        self.blocks.clear();
    }
}
```

## 12. Prompt

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

## 13. BONUS: viasync.com

Stripped down, wicked fast web-repo to backup and sync local via database.

- **Private**: Fully encrypted. No peeping-tom cloud.
- **Automatic**: No git push-pull. 
- **Read-Only**: Only views `.txt` files (except for Prompt).
- **Prompt**: Live version of Prompt tool. Capture notes quickly, on the go. Work on them when you get home.

### -- END --
