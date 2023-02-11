Entities
========

.. c:function:: CREntity CRNewEntity(CRTile tile, Vector2 position)

Creates a new CREntity struct with the following attributes.

* tile: provided tile
* position: provided position
* next: nullptr
* prev: nullptr

.. c:function:: void CRAddEntity(CREntity *entity)

Checks if world layer 0 exists. If it does, add the provided entity to it.

.. c:function:: void CRAddEntityToLayer(CRLayer *layer, CREntity *entity)

Removes the provided entity from it's current position (if any) then adds it to the provided layer. If the layer is null, check if world layer 0 exists and add it to it.
