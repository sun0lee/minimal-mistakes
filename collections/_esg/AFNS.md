---
title: "AFNS 모형의 이해"
toc: true
toc_sticky: true
---

## 무차익 DNS (AFNS) 모형
- AFNS 모형은 연속시간 이론 모형 : 무차익거래 조정항을 제외하면 DNS 모형과 모형의 형태, 추정모수가 실질적으로 같음.
- DNS 모형은 이산 시계열 모형

## DNS, AFNS 모형의 구조

아래 3가지 미관측 잠재요인에 따라 실제 관측되는 만기별 이자율 기간구조를 설명함.

* 수준 ; level
* 기울기 ; slope
* 곡도 ; curvature

### 모수

```
  this.initParas[0]  = this.lambda;
  this.initParas[1]  = this.thetaL;  
  this.initParas[2]  = this.thetaS;  
  this.initParas[3]  = this.thetaC;
  this.initParas[4]  = Math.max(this.kappaL, 1e-4);
  this.initParas[5]  = Math.max(this.kappaS, 1e-4);		
  this.initParas[6]  = Math.max(this.kappaC, 1e-4);		
  this.initParas[7]  = this.initSigma;
  this.initParas[8]  = 0.0;
  this.initParas[9]  = this.initSigma;
  this.initParas[10] = 0.0;            
  this.initParas[11] = 0.0;
  this.initParas[12] = this.initSigma;
  this.initParas[13] = this.epsilon * 1000;
```

### 상태공간(  state - space )모형

미관측 잠재요인(수준,  기울기,  곡도 ) 으로   관측변수(금리)를  설명하는 모형.

|금리모형 | 관측방정식(measurement eq.) | 상태방정식(state eq.) |
| --- | --- | --- |
| DNS (disc)  | $$y_t(\tau)= B(\tau)X_t + \epsilon_i(\tau)$$ | $$X_t - \mu_X = \phi_X(X_{t-1} - \mu_X) + \eta_{Xt}$$ |
| AFNS (Cont) | $$y_t(\tau)= B(\tau)X_t +\dfrac{A(\tau)}{\tau}+ \epsilon_i(\tau)$$ | $$dXt = K^P (\theta^P-X_t)dt + \sum dW_t^P$$|
| AFNS (disc) | $$y_t(\tau)= B(\tau)X_t +\dfrac{A(\tau)}{\tau}+ \epsilon_i(\tau)$$ | $$X_t = (I - e^{-K^P\Delta t})\theta^P + e^{-K^P \Delta t}X_{t-1} + \eta_{Xt}$$ |

<details>
  <summary>DNS (disc) 관측방정식 notation</summary>
  <div markdown="1">
  {% capture notice-1 %}

- $$ \begin{bmatrix} y_t(\tau_1) \\ y_t(\tau_2) \\ \vdots \\ y_t(\tau_N)  \end{bmatrix} =  \begin{bmatrix} 1 & (\frac{1-e^{-\lambda \tau_1}}{\lambda \tau_1}) & (\frac{1-e^{-\lambda \tau_1}}{\lambda \tau_1} - e^{-\lambda \tau_1}) \\  1 & (\frac{1-e^{-\lambda \tau_2}}{\lambda \tau_2}) & (\frac{1-e^{-\lambda \tau_2}}{\lambda \tau_2} - e^{-\lambda \tau_2}) \\  & \vdots &  \\ 1 & (\frac{1-e^{-\lambda \tau_N}}{\lambda \tau_N}) & (\frac{1-e^{-\lambda \tau_N}}{\lambda \tau_N} - e^{-\lambda \tau_N}) \end{bmatrix} \begin{bmatrix}    L_t \\ S_t \\ C_t  \end{bmatrix} + \begin{bmatrix} \epsilon_i(\tau_1) \\ \epsilon_i(\tau_2) \\ \vdots \\ \epsilon_i(\tau_N)  \end{bmatrix} $$

  * $$B(\tau)= \begin{bmatrix}    1 & (\frac{1-e^{-\lambda \tau_1}}{\lambda \tau_1}) & (\frac{1-e^{-\lambda \tau_1}}{\lambda \tau_1} - e^{-\lambda \tau_1}) \\    1 & (\frac{1-e^{-\lambda \tau_2}}{\lambda \tau_2}) & (\frac{1-e^{-\lambda \tau_2}}{\lambda \tau_2} - e^{-\lambda \tau_2}) \\  & \vdots &  \\ 1 & (\frac{1-e^{-\lambda \tau_N}}{\lambda \tau_N}) & (\frac{1-e^{-\lambda \tau_N}}{\lambda \tau_N} - e^{-\lambda \tau_N}) \end{bmatrix}$$: 관측방정식의 계수 행렬, 요인과 수익률을 연결하는 요인 민감도 행렬임.
    - $$L_t$$ 수준요인의 계수 : 1
    - $$S_t$$ 기울기요인의 계수 : $$(\frac{1-e^{-\lambda \tau_1}}{\lambda \tau_1})$$
    - $$C_t$$ 곡도 요인의 계수 : $$(\frac{1-e^{-\lambda \tau_1}}{\lambda \tau_1} - e^{-\lambda \tau_1})$$


  * $$X_t= \begin{bmatrix}    L_t \\ S_t \\ C_t  \end{bmatrix}$$: 추정모수
  * $$\epsilon_i(\tau) \thicksim N(0_{N \times 1},H_{N \times N})$$ : 확률 오차항

  * $$H = \begin{bmatrix} \sigma^2 & 0 & \cdots & 0 \\ 0 & \sigma^2 & \cdots & 0 \\ 0 & 0 & \cdots & 0 \\ 0 & 0 & \cdots & \sigma^2  \end{bmatrix}$$ : 공분산 행렬

  {% endcapture %}
  <div class="notice">
    {{ notice-1 | markdownify }}
  </div>
  </div>
</details>

$$y_t(\tau)= B(\tau)X_t + \epsilon_i(\tau)$$
{: .notice--warning}

<details>
  <summary>DNS (disc) 상태방정식 notation</summary>
  <div markdown="1">
  {% capture notice-1 %}

* $$ \begin{bmatrix} L_t-\mu_L \\ S_t-\mu_S \\ C_t-\mu_C \end{bmatrix} =  \begin{bmatrix} \phi_L & 0 & 0 \\ 0 & \phi_S & 0 \\ 0 & 0 &\phi_C \end{bmatrix} \begin{bmatrix} L_{t-1}-\mu_L \\ S_{t-1}-\mu_S \\ C_{t-1}-\mu_C \end{bmatrix} + \begin{bmatrix} \eta_{L,t} \\ \eta_{S,t} \\ \eta_{C,t}  \end{bmatrix} $$

  * $$\mu_X =  \begin{bmatrix}    \mu_L \\ \mu_S \\ \mu_C \end{bmatrix}$$ : 3요인의 장기평균모수
  * $$\phi_X =  \begin{bmatrix}    \phi_L & 0 &  0 \\   0 & \phi_S & 0 \\ 0&0&\phi_C \end{bmatrix}$$ : 상태방정식 계수행렬 : 3요인의자기회귀모수
  * $$ \eta_{Xt} = \begin{bmatrix} \eta_{L,t} \\ \eta_{S,t} \\ \eta_{C,t}  \end{bmatrix}$$ : 확률 오차항
  * $$ \eta_t \thicksim N(0_{3 \times 1},Q_{ 3 \times 3 }) $$,  $$ Q = \begin{bmatrix} \sigma_L^2 & 0 & 0 \\ 0 & \sigma_S^2 &  0 \\ 0 & 0 & \sigma_C^2  \end{bmatrix}$$ : 공분산 행렬

  {% endcapture %}
  <div class="notice">
    {{ notice-1 | markdownify }}
  </div>
  </div>
</details>

$$X_t - \mu_X = \phi_X(X_{t-1} - \mu_X) + \eta_{Xt}$$
{: .notice--warning}

<details>
  <summary>AFNS (conti.) notation</summary>
  <div markdown="1">
  {% capture notice-1 %}

**관측방정식**

* 무차익거래 조정항 : $$\dfrac{A(\tau)}{\tau}$$ : 채권가격 결정 시 차익거래가 발생하지 않아야 한다는 이론적 제약을 도입하여 모형을 전개하면 도출되는 항. ( $$\tau , \lambda , \Sigma$$ )으로 구할 수 있는 closed form.
<br><br>

**상태방정식**

* Kappa : $$K^P = \begin{bmatrix}    K_{11}^P & 0 &  0 \\   0 & K_{22}^P& 0 \\ 0&0&K_{33}^P \end{bmatrix}$$, 평균회귀속도 모수행렬

* Theta : $$\theta^P=\begin{bmatrix}  \theta_1^P  \\  \theta_2^P \\ \theta_3^P \end{bmatrix}$$ 장기평균모수 벡터

* Sigma : $$\Sigma= \begin{bmatrix}    \sigma_{11} & 0 & 0 \\   \sigma_{21} & \sigma_{22} & 0 \\ \sigma_{31} & \sigma_{32} & \sigma_{33} \end{bmatrix}$$ 공분산 행렬의 촐레스키 하방 삼각 행렬, 변동성 행렬

* $$W_t^P$$ 표준 위너프로세스

  {% endcapture %}
  <div class="notice">
    {{ notice-1 | markdownify }}
  </div>
  </div>
</details>

- **관측방정식**
  - $$y_t(\tau)= B(\tau)X_t +\dfrac{A(\tau)}{\tau}+ \epsilon_i(\tau)$$
- **상태방정식**
  - $$dXt = K^P (\theta^P-X_t)dt + \sum dW_t^P$$
{: .notice--warning}


<details>
  <summary>AFNS (disc.) notation</summary>
  <div markdown="1">
  {% capture notice-1 %}

- 상태공간모형으로  표현된 AFNS 모형은 요인에 대해 linear(선형)이므로 칼만필터를 이용하여 모수를 추정함.

  {% endcapture %}
  <div class="notice">
    {{ notice-1 | markdownify }}
  </div>
  </div>
</details>

- **관측방정식**
  - $$y_t(\tau)= B(\tau)X_t +\dfrac{A(\tau)}{\tau}+ \epsilon_i(\tau)$$
- **상태방정식**
  - $$X_t = (I - e^{-K^P\Delta t})\theta^P + e^{-K^P \Delta t}X_{t-1} + \eta_{Xt}$$
{: .notice--warning}



* AFNS 모형의 관측방정식은 요인에 대한 선형모형으로 표현되므로 칼만필터를 이용하여 모수를 추정함.

### 칼만필터

시간의 흐름에 따라 반복작업.

* 상태방정식을 이용한 예측,
* 관측방정식에 따른 예측오차의 보정을 반복적으로 수행하며, 
* 파라미터 추정치와 미관측요인 $$X_t$$의 추정치를 구함.

1. 초기모수
   * $$X_{1|0} = \theta^P$$
   * $$V_{1|0} =  (I - e^{-K^P   \Delta t})^{-1} \cdot \Sigma_\eta$$
   * $$\psi_0 \equiv (I -  e^{-K^P   \Delta t}) \cdot \theta^P$$
   * $$\psi_1 \equiv e^{-K^P   \Delta t}$$
2. 칼만 필터에 의한 반복 계산 과정
   * 조건부 추정치
     * $$X_{t|t-1} = \psi_0 + \psi_1 \cdot X_{t-1|t-1}$$
     * $$V_{t|t-1} = \psi_1 \cdot V_{t-1|t-1} \cdot \psi_1^T  + \Sigma_\eta$$
   * 조건부 예측오차
