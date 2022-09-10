# Piece Tables
The "Unsung hero" data-structure that is responsible for much of the functionality and performance characteristics that power modern day text editors. `Visual Studio Code` for example is an implementer of the piece table.

I was first made aware of the "Piece Table" data structure when re-searching text editors both new and old. Multiple times I came across the mention that Piece tables were used in a variety of text editors, however I found no real major documentation on the structure itself. Luckily the internet is vast and carries a multitude of one off blogs and github examples which together supplement the personal enrichment of such a data structure.

The history of the piece table itself came along when the O.G text editor data structure `"Array of Strings"` just wasn't cutting it performance wise anymore.

The problem with `Array of Strings` is that whenever you want to insert some text into the middle of the said **"Document"** in the case of a text editor. You would have to push every item following the insertion point, to the right. When it comes to smaller documents this itself will work just fine, it's once you start increasing in size that you start bumping into the aggregating effects of time-complexity. 

The Piece table, was brought into scope to ease this performance eater by walking down an append only approach. Meaning when we add data to the main array we don't have to shift other items to make space.


## How it Works
The Piece Table itself has three components
1. `add buffer`: A single string that Stores anything that has been added to the document since the start of the session
2. `original buffer`: A single string that Stores anything that was pre-existing, whether it was read from a file or received from an API. nothing in this buffer is to be changed.
3. `piece descriptors`: A custom object that at least contains three fields of information   
   1. **source**: tells which buffer to read from.
   2. **start**: tells which index in that buffer to start reading from.
   3. **length**: tells how many characters to read from that buffer.
        ```typescript
        type Piece = {
            source: string,
            start: number,
            length: number
        }
        ``` 
   
4. `descriptor array`: An array of **piece descriptors** that defines the final outcome of the document by adding the descriptors together.

With these components you can create a simple piece table object.
```typescript
type Piece = {
    source: string,
    start: number,
    length: number
}

type PieceTable = {
    original: string,
    add: string,
    pieces: Piece[]
}

const myTable = new PieceTable({
    original: 'This is pulled from the original file',
    add: 'and I have added this',
    pieces: [
        new Piece({source: "original", start: 0, length: 35}), 
        new Piece({source: "add", start: 0, length: 21})
    ]
})
```

Once constructed the document will stitch the pieces together and the final output will read like so...
- **This is pulled from the original file and I have added this**

### Deleting Text
When deleting text from a piece table we split an existing piece into two pieces:
1. On piece points to the left of the deleted text.
2. The second piece points to the right of the deleted text.

Don't worry the data for the deleted text is gone, but not gone? :smile:. 
It's still available in either the original or add buffer so we can get it back, however it won't be shown in the final output of the document.

### Undo and Redo
A benefit of keeping text even though it has been deleted, is that we can add functionality to `undo` and `redo` in our text editor. This is almost a given in modern text editors, so it's good that with the piece table that's already under our belt.

### Final Considerations
Piece tables themselves aren't the only answer to a good text editor, and like a phenominal dish, it's usually combined with other data structures in order to provide the best experience for your text editor.

