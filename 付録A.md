## 付録A：統合フローチャート

### A-1. 概要

本付録では、テンポリウムの全層を統合したフローチャートを提示する。

---

### A-2. 第0層〜第3層：移動条件群フロー

```mermaid
flowchart TD
    START[テンポリウム検証開始] --> Q0{移動方向は?}
    
    Q0 -->|現在より前| PAST[過去移動]
    Q0 -->|現在より後| FUTURE[未来移動]
    
    PAST --> Q1T{時間座標精度は?}
    FUTURE --> Q1T
    
    Q1T -->|年月日時分秒を指定可能| T_FULL[完全指定]
    Q1T -->|大まかな時代のみ| T_RANGE[範囲指定]
    Q1T -->|制御不能| T_RANDOM[ランダム]
    
    T_FULL --> Q1S{空間座標は?}
    T_RANGE --> Q1S
    T_RANDOM --> Q1S
    
    Q1S -->|正確に到達| S_POINT[空間座標指定点]
    Q1S -->|ズレた位置| S_DEV[空間座標ズレ]
    Q1S -->|空間が上書き| S_OVER[空間座標上書き]
    
    S_POINT --> Q2TL{時間線構造は?}
    S_DEV --> Q2TL
    S_OVER --> Q2TL
    
    Q2TL -->|一本の線| TL_SINGLE[単一線型]
    Q2TL -->|改変で分岐| TL_BRANCH[分岐型]
    Q2TL -->|最初から複数| TL_PARALLEL[平行型]
    Q2TL -->|ループ| TL_CIRCULAR[環状型]
    Q2TL -->|複雑に交差| TL_NETWORK[網目型]
    
    TL_SINGLE --> Q2TF{時間流状態は?}
    TL_BRANCH --> Q2TF
    TL_PARALLEL --> Q2TF
    TL_CIRCULAR --> Q2TF
    TL_NETWORK --> Q2TF
    
    Q2TF -->|過去から未来へ| TF_FWD[順行]
    Q2TF -->|未来から過去へ| TF_BWD[逆行]
    Q2TF -->|止まっている| TF_STOP[停止]
    Q2TF -->|状況で変わる| TF_VAR[可変]
    
    TF_FWD --> Q3C{接触可能性は?}
    TF_BWD --> Q3C
    TF_STOP --> Q3C
    TF_VAR --> Q3C
    
    Q3C -->|物理的干渉が可能| C_YES[接触可能]
    Q3C -->|観測のみ| C_NO[接触不可]
    
    C_NO --> SAFE[パラドックス発生なし: 検証終了]
    
    C_YES --> Q3R{帰還可能性は?}
    
    Q3R -->|確実に戻れる| R_GUAR[帰還保証]
    Q3R -->|戻れない| R_IMP[帰還不可]
    Q3R -->|不明または確率的| R_UNC[帰還不確定]
    
    R_GUAR --> Q3D{滞在時間制限は?}
    R_IMP --> Q3D
    R_UNC --> Q3D
    
    Q3D -->|制限なし| D_UNL[滞在無制限]
    Q3D -->|一定時間で終了| D_LIM[滞在有限制限]
    Q3D -->|条件で変動| D_VAR[滞在可変制限]
    Q3D -->|一瞬のみ| D_INST[滞在瞬間のみ]
    
    D_UNL --> TO_L4[第4層へ進む]
    D_LIM --> TO_L4
    D_VAR --> TO_L4
    D_INST --> TO_L4
```

---

### A-3. 第4層〜第6層：状態判定群フロー

```mermaid
flowchart TD
    START[第3層から継続] --> Q4CA{原因側の状態は?}
    
    Q4CA -->|論理的に説明可能| CA_ALI[原因整合]
    Q4CA -->|論理的に説明不可能| CA_CON[原因矛盾]
    
    CA_ALI --> Q4EA{結果側の状態は?}
    CA_CON --> Q4EA
    
    Q4EA -->|原因から論理的に導かれる| EA_ALI[結果整合]
    Q4EA -->|原因と矛盾している| EA_CON[結果矛盾]
    
    EA_ALI --> PATTERN{パターン判定}
    EA_CON --> PATTERN
    
    PATTERN -->|原因整合 + 結果整合| PA[パターンA: 完全整合]
    PATTERN -->|原因整合 + 結果矛盾| PB[パターンB: 結果破綻]
    PATTERN -->|原因矛盾 + 結果整合| PC[パターンC: 原因破綻]
    PATTERN -->|原因矛盾 + 結果矛盾| PD[パターンD: 完全矛盾]
    
    PA --> Q5O{観測者は誰か?}
    PB --> Q5O
    PC --> Q5O
    PD --> Q5O
    
    Q5O -->|時間旅行者本人| O_TRAV[旅行者観測]
    Q5O -->|旅行者でも被観測者でもない| O_THIRD[第三者観測]
    Q5O -->|パラドックスの主体| O_SUBJ[被観測者観測]
    Q5O -->|誰もいない| O_NONE[観測者不在]
    
    O_NONE --> UNVERIFY[検証不能: 判定終了]
    
    O_TRAV --> Q5M{記憶の状態は?}
    O_THIRD --> Q5M
    O_SUBJ --> Q5M
    
    Q5M -->|元の記憶を保持| M_CHAIN[記憶連鎖]
    Q5M -->|特定時点で途切れ| M_SEV[記憶断絶]
    Q5M -->|完全に失われた| M_LOSS[記憶消失]
    Q5M -->|書き換えられている| M_FALSE[記憶改竄]
    
    M_CHAIN --> Q6E{同時存在の状態は?}
    M_SEV --> Q6E
    M_LOSS --> Q6E
    M_FALSE --> Q6E
    
    Q6E -->|2人存在| E_DUAL[二重存在]
    Q6E -->|3人以上存在| E_MULTI[複数存在]
    Q6E -->|同時存在不可で消滅| E_ANNIHIL[存在消滅]
    Q6E -->|重複なし| E_NONE[同時存在なし]
    
    E_ANNIHIL --> PARADOX_EXIST[存在パラドックス: 完全矛盾]
    
    E_DUAL --> Q6I{情報の状態は?}
    E_MULTI --> Q6I
    E_NONE --> Q6I
    
    Q6I -->|完全に保持| I_FULL[情報完全保持]
    Q6I -->|一部が欠損または変質| I_PART[情報部分劣化]
    Q6I -->|完全に失われた| I_LOST[情報完全劣化]
    Q6I -->|誤った内容が混入| I_NOISE[情報ノイズ混入]
    
    I_LOST --> UNVERIFY2[検証不能: 判定終了]
    
    I_FULL --> FINAL{最終判定}
    I_PART --> FINAL
    I_NOISE --> FINAL
    PARADOX_EXIST --> FINAL_FC[完全矛盾]
    
    FINAL --> RESULT{全層の結果を統合}
    
    RESULT -->|全層で矛盾なし| FINAL_FA[完全整合]
    RESULT -->|一部の層で矛盾| FINAL_PC[部分矛盾]
    RESULT -->|複数層で矛盾| FINAL_FC2[完全矛盾]
```

---

### A-4. 最終判定サマリ

|判定|条件|結論|
|---|---|---|
|完全整合|全層で矛盾なし|パラドックスは発生しない|
|部分矛盾|一部の層で矛盾|条件付きでパラドックスが発生|
|完全矛盾|複数層で矛盾、パターンD、存在消滅|パラドックスが完全に成立|
|検証不能|観測者不在、情報完全劣化|判定自体が不可能|
|発生なし|接触不可|干渉不能のためパラドックスなし|

---
