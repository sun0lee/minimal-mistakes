---
title: "IV. 지급여력기준금액 산출"
layout: single-index
thisId : '14'
toc : false
---

<div class="mermaid">
flowchart TB

   T[총 요구자본] --> Tax
    direction TB
    subgraph Tax
        direction RL
        TE[/법인세효과/] -.-> B[기본요구자본]
    end

    subgraph baseScr
        direction TB
        A[기본 요구자본] -->A1(장기생명보험위험액)
        A -->A2(일반손해보험위험액)
        A -->A3(시장위험액)
        A -->A4(신용위험액)
        A -->A5(운영위험액)
    end

  Tax --> baseScr
</div>
