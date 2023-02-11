Layers
======

.. c:function:: CRLayer CRNewLayer()

Create a new CRLayer struct with the following attributes.

* Grid: nullptr
* entities.head: nullptr
* entities.tail: nullptr
* tile_index: 0
* width: default layer width
* height: default layer height
* position: (0,0)
* flags: 0
* mask_count: 0

.. c:function:: void CRInitGrid(CRLayer *layer)

Calculate the size of the grid based on the width and height of the layers, then allocate the memory for it and fill the grid with zeros.

.. c:function:: CRLayer CRInitLayer()

Creates a new layer using :c:expr:`CRNewLayer()`, then initializes the grid using :c:expr:`CRInitGrid()`.

.. c:function:: void CRSetWorldLayer(int index, CRLayer layer)

Checks if the index is within the world_layers array bounds, then overwrites whatever is in that index with the provided layer.

.. c:function:: void CRSetUILayer(int index, CRLayer layer)

Checks if the index is within the ui_layers array bounds, then overwrites whatever is in that index with the provided layer.

.. c:function:: void CRNewWorldLayer()

Increases the size of the world_layer array in the cr_config struct by one, adding it to the end of the array.

.. c:function:: void CRNewUILayer()

Increases the size of the ui_layer array in the cr_config struct by one, adding it to the end of the array.

.. c:function:: void CRAddWorldLayer(int index, CRLayer layer)

Creates a new layer using :c:expr:`CRNewWorldLayer()` and adds the provided layer to the index, shifting other layers to make room so nothing is overwritten.

.. c:function:: void CRAddUILayer(int index, CRLayer layer)

Creates a new layer using :c:expr:`CRNewUILayer()` and adds the provided layer to the index, shifting other layers to make room so nothing is overwritten.

.. c:function:: void CRAppendWorldLayer(CRLayer layer)

Creates a new layer using :c:expr:`CRNewWorldLayer()` and adds the provided layer to the end.

.. c:function:: void CRAppendUILayer(CRLayer layer)

Creates a new layer using :c:expr:`CRNewUILayer()` and adds the provided layer to the end.

.. c:function:: void CRInitWorld()

Check if there are already world layers. If not, create a new layer and append it to the world layers.

.. c:function:: void CRInitUI()

Check if there are already UI layers. If not, create a new layer and append it to the UI layers.

.. c:function:: void CRSetLayerFlags(CRLayer *layer, int flags)

Set the flags in the provided layer to the integer ``flags``.

.. c:function:: void CRSetWorldFlags(int flags)

Set the flags in world layer 0 to the integer ``flags``.

.. c:function:: void CRSetUIFlags(int flags)

Set the flags in UI layer 0 to the integer ``flags``.
