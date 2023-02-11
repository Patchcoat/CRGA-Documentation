Getting Started
===============

.. _installation:

Installation
------------

Download the release for your operating system and unzip it: https://github.com/Patchcoat/CRGA/releases/tag/0.1

* Linking libraries in gcc: https://gcc.gnu.org/onlinedocs/gcc/Link-Options.html
  * specify a location with ``-L/directory/path/`` and link the library with ``-llibcrga.so``
* Linking libraries with cmake: https://cmake.org/cmake/help/latest/command/target_link_libraries.html
  * specify a location with ``target_link_libraries(crga -L/directory/path/)``

.. _building:

Building
--------
It is possible to build the entire API locally

1. clone https://github.com/Patchcoat/CRGA.git onto your machine
2. run ``cmake .`` or the equivalent for your setup
3. build the project

* On linux with gcc, cmake will generate a makefile. You can build the project by typing "make" into the terminal
* On windows with the visual studio compiler, cmake will generate an sln and several vxcproj files. This can be built within visual studio, or by running ``msbuild crga.sln``

Your First Project
------------------
Once you get a file to compile while including the ``crga.h`` library, you can move on to using it. As an introduction, we will start with the following ``main.h``.

.. code-block:: c

    #include "crga.h"
    
    CREntity *movable;
    
    void PreDraw() {
        if (IsKeyPressed(KEY_W)) {
            movable->position.y -= 1;
        } else if (IsKeyPressed(KEY_S)) {
            movable->position.y += 1;
        }
        if (IsKeyPressed(KEY_A)) {
            movable->position.x -= 1;
        } else if (IsKeyPressed(KEY_D)) {
            movable->position.x += 1;
        }
    }
    
    int main() {
        // Startup
        CRInit();
        CRSetPreDraw(&PreDraw);
    
        // Place a tile in the world
        CRSetWorldTileChar("A", (Vector2) {0,0});
    
        // Create player entity
        CREntity player = CRNewEntity(CRCTile("@"), (Vector2) {1, 0});
        player.tile.shift = (Vector2) {0, -3};
        CRAddEntity(&player);
        movable = &player;
    
        CRLoop();
    
        // Cleanup
        CRClose();
        return 0;
    }

We start by importing the ``crga.h`` library and defining a global variable for the player entity. We will skip the PreDraw() function for now, and move to main.

.. code-block:: c

    CRInit();
    CRSetPreDraw(&PreDraw);

The first thing we do is initialize. This initializes world layer zero and the default configuration. It creates a window and opens it. This must be called before loading other parts of the game like the font or tilemap due to the way Raylib works.

``CRSetPreDraw(&PreDraw)`` gets a pointer to the ``PreDraw()`` and tells CRGA to use it during the loop function. The PreDraw function will run before any drawing is done, and in-fact, no drawing can be done in the PreDraw function.

.. code-block:: c

   CRSetWorldTileChar("A", (Vector2) {0,0});

This creates a tile using the character "A" and places it in position (0,0) on world layer zero, which is in the top left corner. It overwrites any other tile that is on that spot on that layer, though at this stage it's just a blank tile. It accepts a character array ("") rather than a single character ('') in order to allow for longer, unicode characters. If the string you provide is shorter than 4 bytes, it must be null terminated (which is done automatically if you use double quotes) and if it's longer than 4 bytes, everything after the fourth byte will be lost.

Setting tiles on a grid in the above manner is preferred for things that stay on the grid and don't move around or get added/removed at a high frequency. Walls, floor tiles, that kind of things. For objects that you expect to be moving around or entering/existing the world a lot like the player, monsters, and items, it's better to use a CREntity, which we cover below.

.. code-block:: c

   CREntity player = CRNewEntity(CRCTile("@"), (Vector2) {1, 0});
   player.tile.shift = (Vector2) {0, -3};
   CRAddEntity(&player);
   movable = &player;

``CRCTile`` Generates a CRTile struct using the provided character, in this case "@". It places it at position (1,0), which is just to the right of the top left corner.

Because we will be using the default Raylib font, the "@" character will not center vertically. We can fix this by using the shift property of the entity's tile. In this case, shifting it three pixels upward will be sufficient. 

Now that we have an entity, we need to add it to the game. ``CRAddEntity(&player);`` adds the entity to world layer zero, where it will be drawn on top of any tiles on that layer but below any layers higher than world layer zero.

At the very end, we set our movable global to be the player so that our ``PreDraw()`` function has something to move. A ``CREntity`` struct has a tile (what to render) and a position (where to render it). We only need to modify the position to move it around. Entities have this advantage over tiles placed directly onto the world layer grid. If you want to move an item on the world layer grid, you have to manually remove it from it's current position and add it to the new position.

.. code-block:: c

   CRLoop();

This enters an infinite loop which draws the world and UI and runs the PreDraw function we set earlier. Layers are drawn from lowest to highest, world layers under UI layers. There are other function pointers you can set as well. These are covered on the documentation page about Loops.

The loop continues for as long as the Raylib function ``WindowShouldClose()`` returns false. This is automatically set to true when pressing the esc key.

.. code-block:: c

   void PreDraw() {
       if (IsKeyPressed(KEY_W)) {
           movable->position.y -= 1;
       } else if (IsKeyPressed(KEY_S)) {
           movable->position.y += 1;
       }
       if (IsKeyPressed(KEY_A)) {
           movable->position.x -= 1;
       } else if (IsKeyPressed(KEY_D)) {
           movable->position.x += 1;
       }
   }

The PreDraw function, as mentioned, is called prior to any drawing being done. This function can be named anything, so long as its pointer is passed to the ``CRSetPreDraw()`` function. The key press detection seen here is handled with Raylib functions. CRGA itself does not provide any input handling. 

This function illustrates an important point, that up is negative Y. X is aligned as one would expect, with the positive direction being to the right, but Y is inverted from what most people expect. If you aren't prepared for this it this can catch you, so be careful.

.. code-block:: c

   CRClose();
   return 0;

``CRClose()`` frees all memory allocated throughout the process when creating layers, masks, and the config struct; and loading fonts and tilemaps. After it has finished freeing all the memory, it closes the window.

Afterward, we return out of main with a 0.

