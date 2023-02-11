Cleanup
=======

Cleanup functions should only ever be called immediately before the project stops running.

.. c:function:: void CRClose()

Calls the following functions in sequence

* :c:expr:`CRUnloadFonts()`
* :c:expr:`CRUnloadTilemaps()`
* :c:expr:`CRUnloadCharIndexAssoc()`
* :c:expr:`CRUnloadLayers()`
* :c:expr:`CRUnloadMasks()`
* CloseWindow() from the Raylib library

.. c:function:: void CRUnloadFonts()

Iterates through the list of fonts and unloads them.

.. c:function:: void CRUnloadTilemaps()

Frees all the tilemaps memory.

.. c:function:: void CRUnloadCharIndexAssoc()

Frees all the memory providing associations between characters and arrays.

.. c:function:: void CRUnloadLayers()

Frees all the memory associated with layers.

.. c:function:: void CRUnloadMasks()

Frees the memory associated with masks.
