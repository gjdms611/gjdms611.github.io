---
title: "[독서] Clean Architecture - 1부"
date: 2021-12-30 20:18:36 +0900
categories: [취미, 독서]
tags: [독서, Clean Architecture]
---

디자인패턴을 한번 깔짝여보았던 내가 아는 좋은 아키텍쳐란, 유지보수 하기 쉽고, 이해하기 쉽고, 구현하기 쉬운 아키텍쳐라고 생각한다.   
물론 처음 좋은 아키텍쳐를 짜고, 또 좋은 아키텍쳐를 유지하면서 코드를 짜는 것은 어려운 일이지만 결과적으로 구현을 계속 하다보면 좋은 아키텍쳐를 가진 프로젝트가 기능을 추가하기가 훨씬 쉽다고 느꼈다.   
그렇지만 그 방법에 대해서는 아직 명확하게 알지 못한다.   
그래서 클린 아키텍쳐를 꼭 읽어야지.. 하고 생각만 하고 있었는데, 일단 다 읽지는 못하더라도 일부만 읽는 사람이라도 되어보고 싶다.   


## 1장 : 설계와 아키텍쳐란?
설계와 아키텍쳐는 차이가 없다. 아키텍쳐를 흔히 저수준의 세부사항과 분리된 고수준의 무언가를 가리키고는 하지만, 아키텍트는 저수준의 세부사항을 포함한다. 소프트웨어 전체 설계는 저수준의 세부사항과 고수준의 구조로 구성되고, 이를 통해 대상 시스템의 구조를 정의한다. 둘은 떼어낼 수 없는 관계다.   

**소프트웨어 아키텍쳐의 목표는 필요한 시스템을 만들고 유지보수하는데 투입되는 인력을 최소화 하는데 있다.**   

설계 품질은 곧 요구사항을 만족시키는 데에 드는 비용이다. 또 그 낮은 비용을 시스템의 수명이 다할 때 까지 유지할 수록, 새 기능의 추가 시에 비용이 적게 늘어날 수록 좋은 설계다.   

지저분한 코드를 작성하면 단기간에는 빠르게 갈 수 있고, 장기적 관점에서만 생산성이 낮아진다는 것은 착각이다.  

**엉망으로 만든 코드는 깔끔하게 유지할 때 보다 항상 더 느리다.**   

**빨리 가는 유일한 방법은 제대로 가는 것이다.**   

엉망으로 작성된 코드로 인해 처음부터 다시 시작해 전체 시스템을 재설계하는 것은 해답이 될 수 없다.   
**자신을 과신한다면 재설계하더라도 원래의 프로젝트와 똑같이 엉망으로 내몰린다.**   

소프트웨어 아키텍쳐를 심각하게 고려할 수 있으려면 좋은 소프트웨어 아키텍쳐가 무엇인지 이해해야 한다.      


## 2장 : 두 가지 가치에 대한 이야기
모든 소프트웨어 시스템은 이해관계자에게 행위와 구조라는 두 가지 가치를 제공한다.   

### 행위
프로그래머는 요구사항을 만족하도록 코드를 작성한다. 그러나 단순히 요구사항의 구현과 버그 수정만이 프로그래머가 할 일은 아니다.   

### 아키텍처
소프트웨어란 '부드러운(soft)'과 '제품(ware)'의 합성어다. 즉, '부드러움을 지닌'것이 소프트웨어이다. 따라서 소프트웨어는 **변경하기 쉬워야**한다.   
**변경사항을 적용하는데 드는 비용은 변경되는 범위(scope)에 비례해야 하며, 변경사항의 형태(shape)와는 관련이 없어야 한다.**   
개발비용은 변경사항의 크기와 비례한다. 새로운 요청사항이 이전 변경사항보다 어려운 이유는 시스템의 형태와 요구사항의 형태가 서로 맞지 않기 때문이다. 아키텍처가 특정 형태를 선호할 수록 새로운 기능을 이 구조에 맞추는 것이 힘들어진다.   
**아키텍처는 형태에 독립적이어야 하며, 그럴수록 더 실용적이다.**   

변경 비용이 너무 커서 현실적으로 변경이 불가능한 시스템은 결국 행위의 가치를 만족할 수 없게 된다.   

### 아이젠하워 매트릭스
아이젠하워 매트릭스에서 알 수 있는 것은 긴급한 문제가 아주 중요한 문제인 경우는 드물고, 중요한 문제가 아주 긴급한 경우는 거의 없다는 사실이다.   
행위는 긴급하지만 항상 가장 중요한 것은 아니며, 아키텍쳐는 중요하지만 긴급성을 가지는 경우는 거의 없다.   

아이젠하워 매트릭스의 우선순위   
1. 긴급하고 중요한
2. 긴급하지 않지만 중요한
3. 긴급하지만 중요하지 않은
4. 긴급하지도 중요하지도 않은

즉 아키텍쳐는 상위 2순위를 차지하며, 행위는 1, 3순위를 차지한다.   
