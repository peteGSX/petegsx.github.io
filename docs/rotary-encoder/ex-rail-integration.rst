*************************************
Device Driver and EX-RAIL Integration
*************************************

EX-RAIL automation
==================

Two EX-RAIL commands have been added to enable usage:

ONCHANGE() Event Handler
------------------------

An event handler has been added ``ONCHANGE(vpin)`` similar to the turnout and accessory event handlers.

This enables any position change of the rotary encoder to be used to define an activity.

IFRE() Test Statement
--------------------- 

A test statement ``IFRE(vpin, position)`` has been added to check for the specific position selected by the encoder.

Valid positions are from -127 to 127.

myAutomation.h Example
----------------------

This is a brief example of how to use the encoder to select some turntable positions, based on the myEX-Turntable.example.h file included with the CommandStation code:

.. code-block:: 

  // EX-Turntable macro and route definitions
  #define EX_TURNTABLE(route_id, reserve_id, vpin, steps, activity, desc) \
    ROUTE(route_id, desc) \
      RESERVE(reserve_id) \
      MOVETT(vpin, steps, activity) \
      WAITFOR(vpin) \
      FREE(reserve_id) \
      DONE

  EX_TURNTABLE(TTRoute1, Turntable, 600, 114, Turn, "Position 1")
  EX_TURNTABLE(TTRoute2, Turntable, 600, 227, Turn, "Position 2")
  EX_TURNTABLE(TTRoute3, Turntable, 600, 341, Turn, "Position 3")
  EX_TURNTABLE(TTRoute4, Turntable, 600, 2159, Turn, "Position 4")
  EX_TURNTABLE(TTRoute5, Turntable, 600, 2273, Turn, "Position 5")
  EX_TURNTABLE(TTRoute6, Turntable, 600, 2386, Turn, "Position 6")
  EX_TURNTABLE(TTRoute7, Turntable, 600, 0, Home, "Home turntable")

  // Rotary encoder event handler to select positions:
  ONCHANGE(700)
    IFRE(700, 1)
      START(TTRoute1)
    ENDIF
    IFRE(700, 2)
      START(TTRoute2)
    ENDIF
    IFRE(700, 3)
      START(TTRoute3)
    ENDIF
    IFRE(700, -1)
      START(TTRoute4)
    ENDIF
    IFRE(700, -2)
      START(TTRoute5)
    ENDIF
    IFRE(700, -3)
      START(TTRoute6)
    ENDIF
    IFRE(700, 0)
      START(TTRoute7)
    ENDIF
  DONE

  // Pre-defined aliases to ensure unique IDs are used.
  // Turntable reserve ID, valid is 0 - 255
  ALIAS(Turntable, 255)

  // Turntable ROUTE ID reservations, using <? TTRouteX> for uniqueness:
  ALIAS(TTRoute1)
  ALIAS(TTRoute2)
  ALIAS(TTRoute3)
  ALIAS(TTRoute4)
  ALIAS(TTRoute5)
  ALIAS(TTRoute6)
  ALIAS(TTRoute7)
