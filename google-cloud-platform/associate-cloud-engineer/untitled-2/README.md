---
description: billing related topic
---

# Managing Billing Configuration

1-billing account

billing account consists of a payment method and some billing permissions, and can attach to one or more projects

두 종류의 account

1\) self serve

default / charged at threshold or every 30 days 

2\) invoiced

billed monthly / contact google cloud sales team 

//

inorder to control who has access to billing info, 

can use primitive roles or predifined role related with billing

ex. billing admin : allows you to manage payment details/

billing user: allows you to link and unlinked projects from the billing accounts/

viewer:look at the spending data, usually for finalcial team

//

2. budgets and alerts

how mush you willing to use for month and you can match with previous month expends

alert allow you trigger when your spent hit specific 기 the budget: 50/90/100

//

3. billing exports

analysis billing

1\) big-query exports ; data analysis tool 을 가지고 바로 다시 분석 가능, 패턴 등  
2\) file exports: just export data in json or csv/ appended to storage bucket



