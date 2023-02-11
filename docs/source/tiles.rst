Tiles
=====

Tiles are the basic building blocks of the CRGA engine. A layer is built up of a sequence of tiles that are in turn drawn on screen.

.. c:struct:: CRTile

   The tile struct that holds all tile data. Every tile drawn to the screen has this data.
   
   .. c:union:: index

   The tile index, used to determine what to draw. This can hold either an integer index for referencing a specific tile on a tilemap, or to hold a utf-8 character.

        .. c:var:: char c[4]

        utf-8 character index. If the character is smaller than 4 bytes, it is null terminated.

        .. c:var:: int i

        integer index.

    .. c:var:: Vector2 shift

    How much to shift the tile foreground, in pixels. Useful when a text character or tile doesn't center perfectly or when you want it to be slightly off center. Should not be used to move tiles more than their size.

    .. c:var:: Color foreground_color

    Text color if drawing a character, tint color if drawing from a tilemap.

    .. c:var:: Color background_color

    Color drawn behind the foreground, filling the entire tile.

    .. c:var:: uint8_t visibility

    How transparent the tile is. 255 is totally visible, 0 is totally transparent.

.. c:function:: CRTile CRDefaultTileConfig(int index)

Generates a default tile configuration, using the provided index as the tile's index.

* Shift: 0
* Foreground: default foreground from cr_config
* Background: default background from cr_config
* Visibility: default visibility from cr_config

.. c:function:: CRTile CRCTile(char *string)

Generates a tile from a utf8 character string. Calls :c:expr:`CRDefaultTileConfig()` passing in 0, and then fills the character index with the provided string.

.. c:function:: CRTile CRITile(int index)

Generates a tile from an integer. Calls :c:expr:`CRDefaultTileConfig` passing in the provided index.

.. c:function:: void CRSetGridTile(CRTile *grid, CRTile tile, Vector2 position, int width, int height)

Checks that the position is possible given the provided width and height of the grid, then sets that element of the grid to the provided tile.

.. c:function:: void CRSetLayerTile(CRLayer *layer, CRTile tile, Vector2 position)

Sets the tile on a specified point on a layer's grid to be the provided tile.

.. c:function:: void CRSetLayerTileChar(CRLayer *layer, char *string, Vector2 position)

Creates a new default tile using the provided string, then sets the specified point on the layer's grid to be that tile.

.. c:function:: void CRSetLayerTileIndex(CRLayer *layer, int index, Vector2 position)

Creates a new default tile using the provided integer, then sets the specified point on the layer's grid to be that tile.

.. c:function:: void CRSetWorldTile(CRTile tile, Vector2 position)

As :c:expr:`CRSetLayerTile()` but for world layer 0. Useful when you're starting out and you only want to work with a single world layer.

.. c:function:: void CRSetUITile(CRTile tile, Vector2 position)

As :c:expr:`CRSetLayerTile()` but for UI layer 0. Useful when you're starting out and you only want to work with a single UI layer.

.. c:function:: void CRSetWorldTileChar(char *character, Vector2 position)

As :c:expr:`CRSetLayerTileChar()` but for world layer 0.

.. c:function:: void CRSetUITileChar(char *character, Vector2 position)

As :c:expr:`CRSetLayerTileChar()` but for UI layer 0.

.. c:function:: void CRSetWorldTileIndex(int index, Vector2 position)

As :c:expr:`CRSetLayerTileIndex()` but for world layer 0.

.. c:function:: void CRSetUITileIndex(int index, Vector2 position)

As :c:expr:`CRSetLayerTileIndex()` but for UI layer 0.

.. c:function:: void CRSetWorldLayerTile(int index, CRTile tile, Vector2 position)

As :c:expr:`CRSetWorldTile()` but on a layer provided by the index.

.. c:function:: void CRSetUILayerTile(int index, CRTile tile, Vector2 position)

As :c:expr:`CRSetUITile()` but on a layer provided by the index.
