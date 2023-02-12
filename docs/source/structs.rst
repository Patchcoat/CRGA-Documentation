Structs
=======

.. c:union:: CRTileIndex
   
The index for a tile, indicating which character or tilemap tile is drawn. An index of 0 means nothing is drawn.

   .. c:member:: char c[4]

    Character representation of the index. 4 wide in order to store utf-8 characters.

   .. c:member:: int32_t i

    Integer representation of the index. Useful for specifying a position on a tilemap.

.. c:struct:: CRTile

The struct indicating how to draw a specific tile.

   .. c:member:: CRTileIndex index

    The tile index, describing what to draw.

   .. c:member:: Vector2 shift

    How much to shift the foreground (character or tile image) before drawing it.

   .. c:member:: Color foreground
    
    What color to draw the character, or what color to tint the tile image.

   .. c:member:: Color background

    What color to fill the background of the tile

   .. c:member:: uint8_t visibility

    How visible the tile should be. 0 is totally invisible, 255 is totally visible.

.. c:struct:: CREntity

Free entities that can move around a layer easily. Entities are stored as a doubly linked list.

   .. c:member:: CRTile tile

    The visual component associated with the entity. What to draw.

   .. c:member:: Vector2 position

    The position of the entity. Where it should be drawn.

   .. c:member:: struct CREntity *next

    The next entity within the linked list.

   .. c:member:: struct CREntity *prev

    The previous entity within the linked list.

.. c:struct:: CREntityList

A data structure for holding the doubly linked list in order to make accessing the first or last element in it easier.

   .. c:member:: CREntity *head

    The first element in the list.

   .. c:member:: CREntity *tail

    The last element in the list.

.. c:struct:: CRMask

A layer mask. Used to conceal or fade specific tiles.

   .. c:member:: uint8_t *grid

    All of the visibility values within the mask.

   .. c:member:: Vector2 position

    How much the mask is shifted, in tiles.

   .. c:member:: int width

    The width of the grid.

   .. c:member:: int height

    The height of the grid.

   .. c:member:: uint8_t flags

    Bit flags controlling the behavior of the mask.

    * **Bit 0**

      * **0** don't mask the grid
      * **1** mask the grid

    * **Bit 1**

      * **0** don't mask the entities
      * **1** mask the entities

.. c:struct:: CRLayer

The layer struct holds all the data indicating what is drawn where. A game is likely to have multiple layers store in the cr_config file for everything from world information to UI.

   .. c:member:: CRTile *grid

    A 2d grid of tiles, iterated through when drawing a layer.

   .. c:member:: CREntityList entities

    A linked list of all entities on this layer.

   .. c:member:: Vector2 position

    The position of this layer.

   .. c:member:: size_t mask_indexes[MAXLAYERMASKS]

    A list of mask indexes, used to identify which masks affect this layer. Masks are stored in an array, hence the usage of indexes. This can store up to MAXLAYERMASKS mask indexes, currently 16.

   .. c:member:: size_t mask_count

    The number of masks currently within mask_indexes.

   .. c:member:: size_t tile_index

    Indicates which font or tilemap to use, by their index. Indexes start at 0, so if the game has 5 fonts, and you want this layer to use the second font, you would provide an index of ``1``.

   .. c:member:: int width

    Width of the grid.

   .. c:member:: int height

    Height of the grid.

   .. c:member:: uint8_t flags

    Indicates whether to use an image, and what kind of tilemap mapping to use.

    * **Bit 0**

      * **0** Draw a character
      * **1** Draw a tilemap image

    * **Bit 1** assume we're drawing a tilemap image, this does nothing if drawing a character.

      * **0** Draw using the integer index of the tile
      * **1** Draw using the character mapped index of the tile

.. c:struct:: CRTilemap

The grid of tiles used to draw pictures on screen. A tilemap assumes an input image without gaps between tiles, or a border along the top or left.

   .. c:member:: Texture2D texture

    The texture data, stored in a Raylib data structure. Being a Texture2D, the data is kept on the GPU. It is sliced into individual tiles during rendering.

   .. c:member:: int width

    The width of a single tile in pixels.

   .. c:member:: int height

    The height of a single tile in pixels.

   .. c:member:: size_t tile_count

    The number of tiles stored on a tilemap. Calculated automatically if using a builtin function.

.. c:struct:: CRCharIndexAssoc

An association between a utf-8 character and an integer index. These are stored in a 255 long array for all of the ASCII and extended ASCII characters. Each element of this array is in turn a linked list for the larger unicode values.

   .. c:member:: char character[4]

    The character to associate with an index. 4 wide in order to store utf-8 characters. Anything shorter than 4 bytes must be null terminated.

   .. c:member:: int index

    The integer index associated with the character.

   .. c:member:: struct CRCharIndexAssoc *next

    The next chararacter index association

