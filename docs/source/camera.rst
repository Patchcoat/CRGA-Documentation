Camera
======

These are all manipulations of a Raylib Camera object.

.. c:function:: Camera2D *CRGetMainCamera()

Return a reference to the main camera struct stored within the cr_config struct.

.. c:function:: void CRSetCameraTarget(Camera2D *camera, Vector2 target)

Set the target value of the provided camera.

.. c:function:: void CRSetCameraOffset(Camera2D *camera, Vector2 offset)

Set the offset value of the provided camera.

.. c:function:: void CRShiftCameraTarget(Camera2D *camera, Vector2 target)

Change the camera target position by the given target value.

.. c:function:: void CRShiftCameraOffset(Camera2D *camera, Vector2 offset)

Change the camera offset position by the given offset value.

