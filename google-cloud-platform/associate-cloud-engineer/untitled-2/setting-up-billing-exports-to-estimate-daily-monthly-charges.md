# Setting up Billing Exports to Estimate Daily/Monthly Charges

![](../../../.gitbook/assets/image%20%28102%29.png)

* BigQuery export: give more detail about the expense/use big query to analysis data: billing 데이터를 가지고 또 다른 데이터로 사용할 수 있음
* file export: 많은 info x, csv나 json, 저렴

만들려면 storge 만들어야 함

storage &gt; bucket 만들

![](../../../.gitbook/assets/image%20%28128%29.png)

create bucket

![](../../../.gitbook/assets/image%20%28116%29.png)

다시 billing으로 돌아오기

![](../../../.gitbook/assets/image%20%2897%29.png)

prefix: prepared ID to the file  name for each report

prefix 이름 + 날짜로 저장이 됨



![](../../../.gitbook/assets/image%20%28107%29.png)

file export 상태가 enable



