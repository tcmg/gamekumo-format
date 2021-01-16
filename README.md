# The GameKumo Format

A general purpose game project description format. Purely JSON-based. Created by @kumobius.

## Overview

The GameKumo format is a flexible object data structure that aims to represent a complete game project which can then be easily read and if necessary, further transformed, by other middleware tools and game engines.

A game project is represented as a tree wherein the top node is a game object and all other parts of the project are other game objects which are descendants of the root game project. Depending on an object’s type, it may or may not have children of its own but will almost certainly have default attributes.

Therefore every object:
* Has a unique ID.
* Has a parent with regards to its position in the data structure.
* Has a set of attributes which describes that object.
* May have subsequent children of its own. The children of an object may be of different types and therefore different arrays of children.

Finally, another key element of the GameKumo format is that objects may optionally have an heir – which is to say, an object from which they inherit attributes from.

## Project Structure

Below is an example that shows the overall structure of a project in a GameKumo project. The black lines denote parent-child relationships. While the blue dash-dotted lines denote inheritance relationships.

![GameKumo object relationship diagram](https://github.com/tcmg/gamekumo-format/blob/master/images/overview.png?raw=true)

Here is an example of the structure of an object:

```
{
    "id": "00002344793322804578",
    "type": "game",
    "config": {
        "name": {
            "value": "Example Game",
            "type": "directstring",
            "comments": "",
            "meta": ""
        },
        "height": {
            "value": "568",
            "type": "integer",
            "comments": "",
            "meta": ""
        },
        "icon": {
            "value": "00001712611806977053",
            "type": "textureId",
            "comments": "",
            "meta": ""
        },
        "iconSolid": {
            "value": "00004854120959970687",
            "type": "textureId",
            "comments": "",
            "meta": ""
        },
        "startLevel": {
            "value": "00007641181819011078",
            "type": "layout-reference",
            "comments": "",
            "meta": ""
        },
        "version": {
            "value": "1.0",
            "type": "directstring",
            "comments": "",
            "meta": ""
        },
        "width": {
            "value": "320",
            "type": "integer",
            "comments": "",
            "meta": ""
        },
        "zoom": {
            "value": "1",
            "type": "integer",
            "comments": "",
            "meta": ""
        }
    },
    "classes": [...],
    "layouts": [...],
    "behaviours": [...],
    "textures": [...]
}
```

All objects in GameKumo have at least these 3 JSON properties:
* id: 
* type: 
* config: 

Children objects are collected as arrays with individual labels denoting their relationship to the parent, for example:
* classes: 
* layouts: 
* behaviours: 
* textures: 

## Predefined Object Types & Default Config Values

For a definition of all predefined object types, consult the templates.json file in the project root. The following are the most core object types.

Game
* Config:
  * name
  * width
  * height
  * startLayout
  * version
  * zoom
* Children:
  * classes
  * layouts
  * behaviours
  * textures

Class
* Config:
  * name
  * width 
  * height
* Children:
  * behaviours

Instance
* Inherit: this object type can inherit from another object (specifically a class)
* Config:
  * width
  * height
* Children:
  * behaviours

Layout:
* Config:
  * name
  * width
  * height
* Children:
  * layers
  * behaviours

Layer:
* Config:
  * name
  * z
* Children:
  * instances
  * behaviours

Behaviour:
* Inherit: this object type can inherit from another object (specifically other behaviours)
* Config:
  * width
  * height

Texture:
* Config:
  * src

Other object types:
* Font
* Sound
* Music

## Attribute Types

* string
* integer
* float
* enum
* boolean
* class-reference
* instance-reference
* layout-reference
* layer-reference
* behaviour-reference
* texture-reference
