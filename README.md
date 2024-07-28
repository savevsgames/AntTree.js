# AntTree.js

AntTree.js is a JavaScript library designed to simplify DOM manipulation and event handling using an analogy of ants and trees. The library allows users to create and manage DOM elements (branches and leaves), handle events (scout ants), and manage data (carrier ants) with an intuitive interface.

**CURRENT STATE => AntTree.js is a conceptual library that is in the planning stages. Eventually it may become a good resource to developers learning JavaScript and web development.**

## Table of Contents

- [AntTree.js](#anttreejs)
  - [Table of Contents](#table-of-contents)
  - [Features](#features)
  - [Note](#note)
  - [Getting Started](#getting-started)
    - [Usage](#usage)
  - [API Documentation](#api-documentation)
    - [Core Concepts](#core-concepts)
    - [Ant Types](#ant-types)
      - [Scout Ants](#scout-ants)
      - [Worker Ants](#worker-ants)
      - [Carrier Ants](#carrier-ants)
      - [Queen Ants](#queen-ants)
      - [Guard Ants](#guard-ants)
    - [Tree Structure](#tree-structure)
      - [Tree](#tree)
      - [Branch](#branch)
      - [Leaf](#leaf)
    - [Example Usage](#example-usage)
      - [Classic DOM Manipulation and Event Handling](#classic-dom-manipulation-and-event-handling)
      - [Simplified with AntTree.js](#simplified-with-anttreejs)
  - [License](#license)

## Features

- **Simplified DOM Manipulation**: Use tree and branch structures to represent and manipulate the DOM.
- **Event Handling**: Utilize specialized scout ants for different event types.
- **Data Management**: Implement carrier ants to handle variables and data.
- **Extensible Classes**: Create custom functionality with queen ants.

## Note

AntTree.js is not yet available on npm. Once it is, installation instructions will be provided here.

## Getting Started

### Usage

Here's an example of how to use AntTree.js:

```javascript
import {
  Tree,
  Branch,
  Leaf,
  ClickScout,
  DataWorker,
  DataCarrier,
} from "anttree";

document.addEventListener("DOMContentLoaded", () => {
  const myTree = new Tree();

  // Create root branch
  const rootBranch = myTree.addBranch("div", { id: "root" });
  document.body.appendChild(rootBranch.element);

  // Add button as a branch
  const buttonBranch = rootBranch.addBranch("button", {
    innerText: "Click me",
  });

  // Add paragraph as a leaf
  const paragraphLeaf = rootBranch.addLeaf("p", "This is a paragraph.");

  // Create a DataCarrier to hold the text data
  const textData = new DataCarrier("textData", "Button was clicked!");

  // Create a ClickScout ant to handle click events
  const clickScout = new ClickScout((event) => {
    console.log("Button clicked!", event);
    paragraphLeaf.content = textData.data;
  });

  // Add the ClickScout to the button branch
  buttonBranch.addAnt(clickScout);

  // Trigger the event to update the paragraph text
  buttonBranch.triggerEvent("click");
});
```

## API Documentation

### Core Concepts

- **Tree**: Represents the entire DOM structure.
- **Branch**: Represents DOM elements.
- **Leaf**: Represents text nodes or content.
- **Bark**: Acts as a firewall, protecting the inner tree mechanisms.
- **Sap**: Represents protected data within the tree.
- **Ant**: Represents various JavaScript functions and event handlers.
- **Trail**: Represents event propagation paths.

### Ant Types

#### Scout Ants

- **ClickScout**: Handles click events.
- **HoverScout**: Handles hover events.
- **InputScout**: Handles input events.

#### Worker Ants

- **DataWorker**: Processes data.
- **DOMWorker**: Manipulates the DOM.

#### Carrier Ants

- **DataCarrier**: Carries data variables.
- **SapCarrier**: Carries protected data (sap).

#### Queen Ants

- **QueenAnt**: Creates instances of classes.

#### Guard Ants

- **GuardAnt**: Implements security checks and validation.

### Tree Structure

#### Tree

```javascript
class Tree {
  constructor() {
    this.branches = [];
    this.ants = [];
    this.guardAnts = [];
  }

  addBranch(tag, attributes) {
    const branch = new Branch(tag, attributes);
    this.branches.push(branch);
    return branch;
  }

  addAnt(ant) {
    if (ant.type === "GuardAnt") {
      this.guardAnts.push(ant);
    } else {
      this.ants.push(ant);
    }
  }

  checkAccess(request) {
    return this.guardAnts.every((ant) => ant.check(request));
  }
}
```

#### Branch

```javascript
class Branch {
  constructor(tag, attributes) {
    this.tag = tag;
    this.attributes = attributes;
    this.leaves = [];
    this.ants = [];
  }

  addLeaf(tag, content) {
    const leaf = new Leaf(tag, content);
    this.leaves.push(leaf);
    return leaf;
  }

  addAnt(ant) {
    this.ants.push(ant);
  }

  triggerEvent(event) {
    this.ants.forEach((ant) => {
      if (ant.type === "ScoutAnt" && ant.event === event) {
        ant.callback();
      }
    });
  }
}
```

#### Leaf

```javascript
class Leaf {
  constructor(tag, content) {
    this.tag = tag;
    this.content = content;
    this.ants = [];
  }

  addAnt(ant) {
    this.ants.push(ant);
  }
}
```

### Example Usage

#### Classic DOM Manipulation and Event Handling

Here is a classic JavaScript example:

```javascript
document.addEventListener("DOMContentLoaded", () => {
  const rootDiv = document.createElement("div");
  rootDiv.id = "root";
  document.body.appendChild(rootDiv);

  const button = document.createElement("button");
  button.innerText = "Click me";
  rootDiv.appendChild(button);

  const paragraph = document.createElement("p");
  paragraph.innerText = "This is a paragraph.";
  rootDiv.appendChild(paragraph);

  button.addEventListener("click", (event) => {
    console.log("Button clicked!", event);
    paragraph.innerText = "Button was clicked!";
  });
});
```

#### Simplified with AntTree.js

The same example using AntTree.js:

```javascript
import {
  Tree,
  Branch,
  Leaf,
  ClickScout,
  DataWorker,
  DataCarrier,
} from "anttree";

document.addEventListener("DOMContentLoaded", () => {
  const myTree = new Tree();

  // Create root branch
  const rootBranch = myTree.addBranch("div", { id: "root" });
  document.body.appendChild(rootBranch.element);

  // Add button as a branch
  const buttonBranch = rootBranch.addBranch("button", {
    innerText: "Click me",
  });

  // Add paragraph as a leaf
  const paragraphLeaf = rootBranch.addLeaf("p", "This is a paragraph.");

  // Create a DataCarrier to hold the text data
  const textData = new DataCarrier("textData", "Button was clicked!");

  // Create a ClickScout ant to handle click events
  const clickScout = new ClickScout((event) => {
    console.log("Button clicked!", event);
    paragraphLeaf.content = textData.data;
  });

  // Add the ClickScout to the button branch
  buttonBranch.addAnt(clickScout);

  // Trigger the event to update the paragraph text
  buttonBranch.triggerEvent("click");
});
```

## License

MIT License
