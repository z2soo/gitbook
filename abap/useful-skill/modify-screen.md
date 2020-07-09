---
description: Screen
---

# Modify screen



## 1. 특정 경우에만 screen field 활성화 방법

```sql
*&---------------------------------------------------------------------*
*& Module MODIFY_SCREEN OUTPUT
*&---------------------------------------------------------------------*

MODULE MODIFY_SCREEN OUTPUT.
    LOOP AT SCREEN.
      IF SY-UCOMM = 'MODIFY' AND SCREEN-NAME = 'INPUT_1'.
        SCREEN-INPUT = 1.
      ENDIF.  
      MODIFY SCREEN.
    ENDLOOP.
ENDMODULE.
```

