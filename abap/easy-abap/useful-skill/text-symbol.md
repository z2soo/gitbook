# Text Symbol

다음 구문을 활용하여 Text Symbol을 생성할 수 있다. 

{% hint style="info" %}
Text-번호
{% endhint %}

```sql
SELECTION-SCREEN BEGIN OF BLOCK CON WITH FRAME TITLE TEXT-100.
SELECT-OPTIONS: COMPANY FOR EKPO-BUKRS NO INTERVALS NO-EXTENSION OBLIGATORY,
                PLANT FOR GS_EKPO-WERKS NO-EXTENSION,
                MATERIAL FOR GS_EKPO-MATNR NO-EXTENSION,
                VENDOR FOR GS_EKKO-LIFNR NO-EXTENSION,
                PUR_ORD FOR GS_EKPO-EBELN NO-EXTENSION,
                PUR_ORG FOR GS_EKKO-EKORG NO-EXTENSION,
                PUR_GRO FOR GS_EKKO-EKGRP NO-EXTENSION.
SELECTION-SCREEN END OF BLOCK CON.

# NO-INTERVALS: PARAMETER 처럼 입력받음 
# OBLIGATORY: 필수 입력
# NO-EXTENSION: 화살표 제
```

![](../../../.gitbook/assets/image%20%28154%29.png)

![](../../../.gitbook/assets/image%20%28153%29.png)

