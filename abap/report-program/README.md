---
description: SAP에서 제공하는 교육 내용과 Easy ABAP 교재 참조
---

# 12. Report Program

## Report program

Type-1에 해당하는 Report program은 실행 시, 다음과 같은 각각의 이벤트를 통해 통제되며, 이벤트 블록은 사용자의 액션에 의해 발생하는 이벤트에 의해 호출된다. 

![&#xCD9C;&#xCC98; EASY ABAP : Report program flow](../../.gitbook/assets/image%20%2860%29.png)



## Program Type 종류 

### Type-1

* Report program, Executable program, Interactive program
* 자동으로 생성되는 Initial screen\(1000\) 사용
* Event block 단위 &gt; Initialization - Selection screen - At selection screen - Start of selection - End of selection &gt; ALV 이전의 표현방식인 Selections screen & Output list 구성

### Type-2

* Include program
* Include로 호출되는 내장형 프로그램

### Type-3, Type-M

* Module pool program, Online program
* T-code 또는 Menu function\(사용자 메뉴 Tree\)에 의해서만 실행
* Program 생성시 Top Include 클릭하면, 자동으로 Type-M 생성
* Screen 단위 &gt; Design time에 화면 구성 &gt; PBO - Screen - PAI &gt; Screen module process 구성

### Type-4

* Functions Groups

### Type-5

* Subroutine Program
* External perform 구문에서 호출 가능한 form 구성

### Type-6

* Interface Pools
* Interface 구성

### Type-7

* Class Pools
* Class 구성 
* F~K는 Program attribute에서 변경 불가하며 각각의 builder에서 관리



