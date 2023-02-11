Loading
=======

CRGA supports loading for fonts and tilemaps.

CRGA will use the default Raylib font until at least one font is loaded, and then it will use whatever font is at index 0 in the cr_config struct.

.. C:function:: void CRLoadFont(const char *font_path)

Load a font at the default font size of 96. Calls :c:expr:`CRLoadFontSize()` with 96 passed into the font size.

.. C:function:: void CRLoadFontSize(const char *font_path, int size)

Load a font at the provided font size, placing it into cr_config at the very end of the fonts array. Performs a malloc or realloc, depending on how many elements there are in the config struct.

.. c:function:: void CRLoadTilemap(const char *tilemap_path, int tile_width, int tile_height)

Loads an image and creates a CRTilemap struct which it places into the cr_config struct. The image is loaded as a texture onto GPU memory. The number of tiles wide, tall, and total in the image are calculated from the information provided.

CRGA will not use a tilemap unless specifically configured to do so. This can be done with ``CRSetWorldFlags(0b11)``. For more information see :c:expr:`CRSetWorldFlags(int flags)`.

CRGA expects an image with no spaces between tiles, but may have space at the right or bottom.

Tiles are indexed from left to right, top to bottom, as one would read english text. Index starts at 1 because 0 is reserved for the null tile.
