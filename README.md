<div align="center">
  
# CSGTree
### A basic module that allows unions with GeometryService to be tracked and so ensure parity with their Studio counterpart.

</div>

## Introduction

[GeometryService](https://create.roblox.com/docs/reference/engine/classes/GeometryService) is a wonderfully useful Roblox service, that allows CSG operations to be done.

However, it comes with a heavy drawback, which is its lack of features and parity compared to the Studio tools' system. This includes - and isn't limited to:

- Separation: Actions cannot be reverted with GeometryService, which may be extremely disturbing when developing a system like [mine](https://github.com/VikkoMakesStuff/Fork3X)
- Position: GeometryService unions take most of their properties from the first argument's part, making them weirdly offset
- Unilateral: You can make GeometryService unions off Studio ones, but not the opposite
- Serialisation: GeometryService offers nothing to serialise unions

If this list includes something you need, **CSGTree can make it possible.**

## Features

- **Both camelCase and PascalCase supported**: Whether your preference is, both most common cases are supported by this module.
  
- **Some extra and unique features**: The parity patch is a completely new patch to center and resize your unions correctly.
  
- **Strict typing**: The module has been built with strict typing, which prevents mistakes caused by putting the wrong classes.

- **An encoding-ready architecture:** Only numbers, tables, dictionaries and strings are stored in CSG trees, so they can be saved on datastores and encoded into any format, including JSON.

## Documentation

### Principle

The module's principle is more or less the same one as [here](https://en.wikipedia.org/wiki/Constructive_solid_geometry).

- **Trees hold unions.** For example, the result of 3 parts and a negative part is a tree.
- **Leaves are the objects used inside a tree.** They're the set of parts themselves, but it can also be another tree we can to assemble.
  
  → For instance, if you add a negative part to an union, the negative part will be a leaf, the union another, and the result a tree

Visual examples will be added soon.

### Operations

Operations don't use names such as "Union", "Intersect" or "Negate". Instead, you must use **numbers.** This is a solution to allow trees to be included inside leaves.

Here's a list of each operation with its number:

- Union → 1
- Negate → 2
- Intersect → 3

Fragment and other operations will be added later.

### Settings

You can - and must - configure some things inside the module:

- **CSGTree.UseParityPatch**: The parity patch is an unique feature that outputs a correctly centered and sized union. However, it adds extra operations, which may make operations longer.

- **CSGTree.Serialize**: You can put here a function to serialise the parts that are important to create the union.
  
- **CSGTree.Desialize**: You can put here a function to desialise the parts (aka recreate them) that are important to create the union.

### Methods

Here's a list of every function in CSGTree, with their parameters highlighted in code blocks. Every function has a camelCase alternative for people who might not like PascalCase:

**Data management:**

- **CSGTree.CreateTree**: Returns an empty tree. The tree is made of two indexes, respectively Version and Data.
  
- **CSGTree.CreateTreeFromItems**: Creates a CSG Tree from the given `Items` - whose positions are accoridng to `Origin` - and `Operation`. You can add extra operations with the functions here.
  
- **CSGTree.CreateParenthesisWithTree**: Returns a CSGLeaf with the given `Tree` inside. It can be then added to another tree with the functions found here.
  
- **CSGTree.CreateLeafFromItems**: Creates a CSGLeaf from the given `Items` - whose positions are accoridng to `Origin` - and `Operation`. This leaf can be added to a tree with the functions here.

**Reading:**

- **CSGTree.IsAParenthesis**: Returns whether a leaf is a parenthesis, this means if the leaf includes a tree.

**Modification:**

- **CSGTree.SplitFromUnion**: Changes the given tree to take in account that a part of the union must be split from the given `Tree`, `TreeCFrame`, and `SplitUnion` parameters.

- **CSGTree.OffsetLeafFromUnion**: Offsets the given `Leaf` from the given `MainUnion` according to its `LeafUnion`.

- **CSGTree.TrackUnionProperties**: Tracks relevant properties from the given `Leaf` and its respective `Union`.

- **CSGTree.FixUnionCFrame**: Returns a new version of the `Union` that's correctly centered. This function is always run automatically with the parity patch enabled.

**Operations:**

- **CSGTree.Union**: Adds a union operation from the given `Leaf` to the `Tree`.
  
- **CSGTree.Intersect**: Adds a negate operation from the given `Leaf` to the `Tree`.
  
- **CSGTree.Negate**: Adds an intersect operation from the given `Leaf` to the `Tree`.

**Generation:**

- **CSGTree.CreateUnionFromTree**: Returns an array of unions from the given `Tree` at the given `DesiredCFrame`, with optional `Parameters`.
  
- **CSGTree.CreatePartsFromTree**: Returns an array of parts from the given `Tree` at the given `DesiredCFrame`. The parts can be sorted between positives and negatives according to the SplitNegatives parameter
  
- **CSGTree.RobloxToCSGTree**: Returns a CSG tree for each given Studio `Unions`. The index of the table is always the union, and the data its value
  
- **CSGTree.UseGeometryServiceWithOperation**: Returns the result of the GeometryService function corresponding to the action. `UseParityPatchAt` also readjusts the union's postion to the given CFrame.

## Demonstration

The best demonstration I can suggest are my own tools [Fork3X](https://github.com/VikkoMakesStuff/Fork3X). Most features are used there, and this gives a great overview on what this module allows.

Credits to @GigsD4X and the @F3XTeam for [SupportLibrary](https://github.com/F3XTeam/RBX-Support-Library)!
