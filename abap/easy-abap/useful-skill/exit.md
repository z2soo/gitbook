---
description: Program 종료 및 뒤로 가기 설정
---

# 작성중\_Exit

### EXIT-COMMAND



ICON\_BACK의 Function type을 'E'로 주고, PAI 부분에 EXIT MODULE을 생성

```sql
# SCREEN
PROCESS AFTER INPUT.
MODULE EXIT AT EXIT-COMMAND.

# MODULE EXIT
MODULE EXIT INPUT.
  CASE OK_CODE.                        # OK_CODE값은 INCLUDE_TOP에 정의되어야 함 
    WHEN 'BACK'.
      LEAVE SCREEN 0.                  # LEAVE PROGRAM, LEAVE SCRREN <NUMBER>
  ENDCASE.
ENDMODULE.
```



