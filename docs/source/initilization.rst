Initilization
=============

.. C:function:: void CRInit()

Initilize CRGA. Call this if you just want to use the default configuration and get up and running as soon as possible. The function does the following:

* Creates a config struct using malloc
* Calls :c:expr:`CRInitConfig()` on that struct
* Calls :c:expr:`CRSetConfig()` on that struct
* Calls :c:expr:`CRInitCharIndexAssoc()`
* Calls :c:expr:`CRInitWorld()`
* Calls :c:expr:`CRInitWindow()`

.. C:function:: void CRInitConfig(CRConfig *config)

Takes in a config, and sets the default values. These are as follows

* Window Width: 800
* Window Height: 450
* FPS: 60
* Window Title: "CRGA basic window"
* Tile Size: 20 pixels
* Default Layer Width: Window Width/Tile Size
* Default Layer Height: Window Height/Tile Size
* Default Tile Foreground Color: White
* Default Tile Background Color: Black
* Default Visibility: 0 (not visible)
* Number of World Layers: 0
* Number of UI Layers: 0
* Main Camera Target: (0,0)
* Main Camera Offset: (0,0)
* Main Camera Rotation: 0
* Main Camera Zoom: 1.0
* Background Color: Black (Background for the entire screen, not just a tile)
* Index/Char Associations: 0
* Fonts: 0
* Tilemaps: 0

.. C:function:: void CRSetConfig(CRConfig *config)

Sets the incoming config to equal the global ``cr_config``. ``cr_config`` is used throughout the program and holds all of the relevant data for drawing things on screen.

.. C:function:: void CRInitCharIndexAssoc()

CRGA lets you associate a specific utf-8 character with a specific index on a tilemap. This is designed to make switching between a character version and a tilemap verson easier. This function creates the basic association table with every character in the extended ascii table. Further associations between unicode characters and tilemap indexes are left to the user.

The null character '\0' maps to 0, the "Null" index. Anything with either '\0' or 0 will not be drawn. The control codes are given mappings starting at index 97 after the delete control code. Characters, starting with space, are mapped to index 1 onward. Characters are given lower indexes than control codes to make it easier to create ascii tilemaps without leaving the top part blank.

After the control codes in the regular ASCII table are set, all higher ascii values are given an index that matches their position on an ASCII table.

.. C:function:: void CRInitWindow()

Calls the ``InitWindow()`` and ``SetTargetFPS()`` functions from the Raylib library, using the values set in the configuration file ``cr_config``.
