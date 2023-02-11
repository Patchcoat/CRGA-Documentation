Configuration
=============

.. c:struct:: CRConfig
   
A struct which holds all of the configuration information used to draw things on the screen. All of the primary drawing, layer, window, and camera information is stored in here.

   .. c:var:: int window_width

    Width of the window.

   .. c:var:: int window_height

    Height of the window.

   .. c:var:: int fps

    Target FPS

   .. c:var:: char *title

    Window Title

   .. c:var:: float tile_size

    Tile size (width and height) in pixels

   .. c:var:: int default_layer_width

    Default layer width, in number of tiles

   .. c:var:: int default_layer_height

    Default layer height, in number of tiles

   .. c:var:: Color default_foreground

    Default foreground tile color. Used for drawing text and tinting tilemap tiles.

   .. c:var:: Color default_background

    Default background tile color.

   .. c:var:: uint8_t default_visibility

    Default tile visibility

   .. c:var:: CRLayer *world_layers

    Pointer to an array of world layers

   .. c:var:: size_t world_layer_count

    Size of the world layer array

   .. c:var:: CRLayer *ui_layers

    Pointer to an array of UI layers

   .. c:var:: size_t ui_layer_count

    Size of the UI layer array

   .. c:var:: CRMask *masks

    Pointer to an array of layer masks

   .. c:var:: size_t mask_count

    Size of the mask array

   .. c:var:: Camera2D main_camera

    Main camera struct

   .. c:var:: Color background_color

    Background color of the screen

   .. c:var:: CRCharIndexAssoc char_index_assoc[255]

    Character-to-index association array

   .. c:var:: CRCharIndexAssoc *assocs

    Pointer to an array of additional character-to-index associations beyond the first 255

   .. c:var:: size_t assoc_count

    Size of the assocs array

   .. c:var:: Font *fonts

    Pointer to an array of font structs

   .. c:var:: size_t font_count

    Size of the font array

   .. c:var:: CRTilemap *tilemaps

    Pointer to an array of tilemaps

   .. c:var:: size_t tilemap_count

    Size of the tilemap array

.. c:function:: void CRSetCharacterAssoc(char *character, int index)

Associates a character with an index on a tilemap. Takes in an up-to 4 byte-long character. Any character smaller than 4 bytes must be null terminated. This lets the user represent tiles as characters, but associate them with a specific position on a tilemap.

For example, if you want to use "@" for your player character, but the tile is index 10 on your tilemap, you would call:

``CRSetCharacterAssoc("@", 10);``
