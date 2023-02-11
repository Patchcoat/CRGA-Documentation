Drawing
=======

.. c:function:: int CRCharToIndex(char *character)

Convert a character to an integer index using the mapping in the char_index_assoc map in the cr_config struct.   

.. c:function:: void CRDrawTile(CRTile *tile, uint8_t tilemap_flags, size_t index, float tile_size, Vector2 position, uint8_t mask)

Draws a tile char or tile image depending on bit zero of the tilemap flags. 0 means draw the tile as a character, 1 means draw the tile as an image. Bit one of the tilemap flags is used if drawing as an image to determine if the direct index of the tile should be used, or if the char-to-index association should be used.

.. c:function:: void CRDrawTileChar(CRTile *tile, Font *font, float tile_size, Vector2 position, uint8_t mask)

Draws the given tile as a character with the given font at the given size, the given position, and with the given transparency from the mask.

.. c:function:: void CRDrawTileImage(CRTile *tile, CRTilemap *tilemap, int char_index, float tile_size, Vector2 position, uint8_t mask)

Draws the given tile as an image with the given font at the given size, the given position, and with the given transparency from the mask.

.. c:function:: void CRDrawLayer(CRLayer *layer)

Iterate through every tile in a layer's grid and draw it to the screen, masking as necessary. Afterward, draw the entity tiles if any, also masking as needed.
