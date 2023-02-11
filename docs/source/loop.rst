Loop
====

To help developers get up and running as quickly as possible, CRGA provides a ready-made loop called :c:expr:`CRLoop()`, described below. Users may keep this around as long as they want, but it's recommended that one switches to a custom loop once it becomes simpler to do so. To facilitate this and make the transition as smooth as possible, the entirety of :c:expr:`CRLoop()` is provided below.

.. code-block:: c

    void CRLoop() {
        while (!WindowShouldClose()) {
    
            if (CRPreDraw != 0)
                (*CRPreDraw)();
    
            BeginDrawing();
    
                ClearBackground(cr_config->background_color);
    
                BeginMode2D(cr_config->main_camera);
    
                    for (int i = 0; i < cr_config->world_layer_count; i++) {
                        CRDrawLayer(&cr_config->world_layers[i]);
                    }
                    if (CRWorldDraw != 0)
                        (*CRWorldDraw)();
    
                EndMode2D();
    
                for (int i = 0; i < cr_config->ui_layer_count; i++) {
                    CRDrawLayer(&cr_config->ui_layers[i]);
                }
                if (CRUIDraw != 0)
                    (*CRUIDraw)();
    
            EndDrawing();
    
            if (CRPostDraw != 0)
                (*CRPostDraw)();
        }
    }

.. c:function:: void CRLoop()

Enter an infinite loop and draws the world and UI layers. It also calls four functions at specific points during the loop.

* :c:expr:`CRPreDraw()` before it enters the drawing portion of the loop. No drawing may be done in here, but it is ideal for measuring user input and performing simulations.
* :c:expr:`CRWorldDraw()` immediately after drawing all the world layers. Anything may be drawn here using the standard Raylib utilities, and will be relative to the world rather than the camera.
* :c:expr:`CRUIDraw()` immediately after drawing all of the ui layers. Anything may be drawn here, and will be relative to the camera rather than the world.
* :c:expr:`CRPostDraw()` after drawing finishes. No drawing may be done in here, and serves a similar role to CRPreDraw. Which you use is a matter of personal taste.

.. c:var:: void (*CRPreDraw)()

A function pointer used to hold the PreDraw function used in CRLoop.

.. c:var:: void (*CRWorldDraw)()

A function pointer used to hold the WorldDraw function used in CRLoop.

.. c:var:: void (*CRUIDraw)()

A function pointer used to hold the UIDraw function used in CRLoop.

.. c:var:: void (*CRPostDraw)()

A function pointer used to hold the PostDraw function used in CRLoop.

.. c:function:: void CRSetPreDraw(void (*new_func)())

Sets the PreDraw function to the function pointer ``new_func``.

.. c:function:: void CRSetWorldDraw(void (*new_func)())

Sets the WorldDraw function to the function pointer ``new_func``.

.. c:function:: void CRSetUIDraw(void (*new_func)())

Sets the UIDraw function to the function pointer ``new_func``.

.. c:function:: void CRSetPostDraw(void (*new_func)())

Sets the PostDraw function to the function pointer ``new_func``.
