Masking
=======

.. c:function:: size_t CRNewMask(int width, int height, uint8_t flags, Vector2 position)

Initializes a new mask of a given width and height, with the given flags set, and put at the provided position. The entire mask is initialized to 255, meaning no masking.

.. c:function:: void CRAddMaskToLayer(size_t mask_index, CRLayer *layer)

Associate a given layer with a mask index. When a layer is being drawn it will check against the associated masks to determine how masked a given tile should be. While you can create as many masks as your computer has memory, any given layer can only have 16 masks associated with it.

.. c:function:: void CRSetWorldMask(Vector2 position, uint8_t mask_value)

Masks a given position on world layer 0. It will create a new mask if one doesn't already exists. If more than one mask exists for world layer 0, it will use the first one.

.. c:function:: void CRSetUIMask(Vector2 position, uint8_t mask_value)

Masks a given position on UI layer 0. It will create a new mask if one doesn't already exists. If more than one mask exists for UI layer 0, it will use the first one.

.. c:function:: uint8_t CRMaskTile(CRLayer *layer, Vector2 position, uint8_t flags)

Checks against all masks used for a layer that overlap a tile at the provided position. This is used for rendering tiles. The flags indicate what is being querried. Bit 0 is 1 if anything that masks an entity will mask the tile, and Bit 1 is 1 if anything that masks a grid tile will mask the tile.

Masking is subtractive. A mask of 205 will reduce a tile's visibility by 50. An additional mask of 205 will reduce the tile's visibility by an additional 50, meaning a total reduction of 100 and a visibility value of 155. A tile's visibility cannot be reduced below 0.
