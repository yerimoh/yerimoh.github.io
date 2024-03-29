---
layout: post
title: "Mat2vec"
date: 2012-05-23
excerpt: "A ton of text to test readability with image feature."
category: [Paper]
layout: post
tag:
- Paper
comments: true
---




**[원 논문]**     
[Unsupervised word embeddings capture latent knowledge from materials science literature](https://www.nature.com/articles/s41586-019-1335-8)https://www.nature.com/articles/s41586-019-1335-8

-----

<details>
<summary>📜 들어가기 전 자주 쓰이는 용어인 power factor 보기</summary>
<div markdown="1">

역률(power factor)의 정의는 **전류가 단위 시간에 하는 일의 비율**이다.
그러면 역률은 언제 **가장 좋나**?
**역률이 '1'** 일 때다. **전류가 모두 일을 했다는 걸 의미**하니까.
이 얘기는 피상전력이 모두 유효전력으로 소비됐다는 뜻이다.
하지만 대부분의 부하에서는 피상전력이 모두 유효전력이 되지 않는다.

전열기나 전구 같은데서는 역률이 거의 1인데
이외에 모터, 형광등 같은 부하에서는 R 이외의 소자들 때문에 역률이 낮기 때문에 피상전력, 유효전력에 차이가 생긴다.
그래서 진상용 콘덴서 같은걸 사용해서 리액턴스를 낮추는 등의 역률을 높이고자 하는 노력을 하기도 한다.


PF(역률)은 에너지 효율의 공식입니다. 이 값은 일반적으로 백분율로 표시되며 백분율 값이 낮을수록 전력 사용량의 효율이 떨어집니다.

역률(PF)은 킬로 와트(kW)로 측정된 유효 전력과 킬로 볼트 암페어(kVA)로 측정된 피상 전력에 대한 비율입니다. 수요 전력이라고 하는 피상 전력은 특정 기간 동안 기계 및 장비를 가동하는 데 사용되는 전력량을 측정하는 것입니다. 이 값은 곱으로 도출됩니다(kVA = V x A). 결과는 kVA 단위로 표시됩니다.


맥주는 유효 전력(kW)입니다. 즉 유용한 전력 또는 액체 맥주는 작업을 수행하는 에너지입니다. 이것이 원하는 부분입니다.

거품은 무효 전력(kVAR)입니다. 즉 거품은 낭비되는 전력 또는 손실되는 전력을 나타냅니다. 이는 열 또는 진동 발생과 같이 작업을 수행하지 않으면서 생산되는 에너지입니다.

맥주잔은 피상 전력(kVA)입니다. 맥주잔은 수요 전력 또는 유틸리티가 공급하는 전력입니다.

![image](https://github.com/yerimoh/img/assets/76824611/1c801798-e142-4465-a5ea-2731c0dac498)

역률 계산 방법
역률을 계산하려면 유효 전력(kW)과 피상 전력(kVA)을 모두 측정하고 kW/kVA 비율을 계산하는 전력 품질 분석기 또는 전력 분석기가 필요합니다.

역률 공식은 다른 방식으로도 나타낼 수 있습니다.

PF = (실제 전력)/(피상 전력)

또는

PF = W/VA

이때 와트는 유효 전력을 측정하고 VA는 공급되는 전력을 측정합니다. 이 둘의 비는 기본적으로 공급되는 전력에 대한 유효 전력을 나타냅니다.


낮은 역률은 전력을 비효율적으로 사용하고 있음을 의미합니다. 이는 다음과 같은 결과를 초래할 수 있기 때문에 회사에 중요합니다.

* 절연재 및 기타 회로 구성 요소에 대한 열 손상   
* 사용 가능한 유효 전력의 감소   
* 도체 및 장비 크기의 증가 요구    
마지막으로, 역률이 낮을수록 부하를 공급하기 위해 더 높은 전류가 필요하기 때문에 배전 계통의 전체 비용이 증가합니다.

[출처](https://www.fluke.com/en-us/learn/blog/power-quality/power-factor-formula)


</div>
</details>  


# ABSTRACT
**[문제]**      
* scientific knowledge은 거의 text로 출판됨     
➡ 전통적인 통계 분석이나 현대적인 기계 학습 방법으로 분석하기 어려움.      
* 기존 materials research와 관련된 machine-interpretable data는 structured property databases [1](https://www.cambridge.org/core/journals/mrs-bulletin/article/materials-science-with-largescale-data-and-informatics-unlocking-new-opportunities/BE294BD45E360E45C9FE0253E702D6B5) [2](https://www.nature.com/articles/s41586-018-0337-2)에서 왔음        
➡ small fraction of the knowledge만 알 수 있음       
* 출판물에는 small fraction 값 외에도 저자가 해석한 **데이터 항목 간의 연결** 및 **관계**에 대한 귀중한 지식이 포함되어 있음.      
* 과거에는 위 문제를 개선하기 위해, large **hand-labelled datasets** for training를 사용하여 과학 문헌에서 정보를 검색하는 데 초점을 맞춤     


**[본 연구]**    
* **방법**     
   * 본 논문은 출판된 문헌에 존재하는 materials science knowledge이 **Human labelling or supervision 없이** information-dense word embeddings(EX, GLOVE)으로 효율적으로 인코딩될 수 있음을 보여줌   
* **장점**    
   * 화학 지식을 명시적으로 삽입하지 않고, 이러한 임베딩은 주기율표의 기본 구조 및 재료의 구조-특성 관계와 같은 **복잡한 재료 과학 개념을 포착** 가능          
   * 또한, 우리는 unsupervised method이 발견되기 몇 년 전 functional 응용 프로그램에 대한 materials를 추천할 수 있음을 보여줌
  ➡ 이것은 **미래의 발견에 관한 잠재적인 지식**이 **과거의 출판물에 상당 부분 내재**되어 있음을 시사함
* 본 논문의 연구 결과는 거대한 과학 문헌에서 **집단적인 방식으로 지식과 관계를 추출할 수 있는 가능성을 강조**하고 **과학 문헌 채굴에 대한 일반화된 접근 방식을 지향**합니다.     





----

# Main
**구문 및 의미 관계를 보존**하기 위해, 텍스트 말뭉치의 단어에 **high-dimensional vectors (embeddings)를 할당**하는 것은 자연어 처리(NLP)의 가장 기본적인 기술 중 하나임(EX, GloVe, Word2vec)      
* 예를 들어, 적절한 텍스트 본문에 대해 훈련할 때, 그러한 방법은 '유기' 벡터보다 '강철' 벡터에 코사인 거리만큼 더 가까운 단어 '철'을 나타내는 벡터를 생성해야 함     

---

**[model train]**         
* **1) text corpus 생성**      
embeddings을 trian하기 위해, 1922년부터 2018년 사이에 발표된 **약 3.3 million개의 scientific abstracts을** materials-related research가 포함될 가능성이 높은 1,000개 이상의 저널에서 수집 및 처리하여 약 **50만 개의 단어가 생성**하였다.       
* **2) skip-gram variation of Word2vec 사용**    
위에서 만든 text corpus를 skip-gram variation of Word2vec에 넣어서 훈련시킴    
이 모델은 target word의 200차원 임베딩을 학습하기 위한 수단임     


----

**[model 작동 예시]**      
![image](https://github.com/yerimoh/yerimoh.github.io/assets/76824611/c0e4c66c-af53-4172-a5bb-2a234bd4e092)
* **1) input word embedding**     
Target words 'LiCoO2'와 'LiMn2O4'는 one-hot encoding으로 바꿈     
즉, 해당 어휘 색인에 있는 단어(예: 그림에서 가각 5와 8번째 만 1임)는 1, 그 외에는 모두 0으로 나타냄.     
* **2) model train with input enbedding**          
이러한 one-hot encoded vectors는 single linear hidden layer (for example, 200 neurons)을 가진 신경망의 입력으로 사용됨      
주어진 Target 단어에서 특정 거리 내에서 언급된 모든 단어**(context words)를 예측하도록 훈련**됨          
ex) LiCoO2와 LiMn2O4와 같은 유사한 배터리 양극 재료의 경우, 텍스트에서 발생하는 컨텍스트 워드(예: 'cathode', 'electrochemical' 등)는 대부분 동일함
* **3) after train**     
이 output을 바탕으로 train이 완료된 후 hidden layer weights 업데이트      
이러한 hidden layer weights는 실제 단어 embedding이다.     

-----


**[main idea of model]**   
* 유사한 의미를 가진 단어가 유사한 맥락에서 나타나는 경우가 많기 때문에, 해당 embeddings도 유사할 것     
* 모델에 대한 자세한 내용은 방법 및 [SUPPLEMENTARY INFORMATION S1](#supplementary-information) 및 [S2](#supplementary-information)에 포함되어 있음     
여기서 GloVe와 같은 대체 알고리즘 옵션에 대해서도 논의합니다.
* 우리는 **algorithm에 화학 정보나 해석이 추가되지 않더라도**, 얻은 word embeddings이 다양한 벡터 연산(projection, addition, subtractio)을 사용하여 결합될 때, **화학적 직관과 일관되게 동작**한다는 것을 발견했음.
   * 예를 들어, 우리 corpus의 많은 단어들은 materials의 chemical compositions을 나타내며, LiCoO2(잘 알려진 리튬 이온 양극 화합물)와 가장 유사한 다섯 가지 물질은 normalized word embeddings의 dot product (projection)을 통해 결정될 수 있음.          
   * 우리의 모델에 따르면 $$LiCoO_2$$와 가장 유사한 compositions은 $$LiMn_2O_4$$, $$LiNi_{0.5}Mn_{1.5}O_4$$, $$LiNi_{0.8}Co_{0.2}O_2$$, $$LiNi_{0.8}Co_{0.15}Al_{0.05}O_2$$, $$LiNiO_2$$이다. 이 다섯가지는 모두 리튬 이온 양극 재료이다.              
* **domain-specific analogies 지원**       
   * 원래 Word2vec paper11에서 관찰한 것과 유사하게, 이러한 임베딩은 **도메인별일 수 있는 유사성**도 지원합니다.   
   * 예를 들어, 'NiFe'는 '강자성'이고, 'IrMn'은 '?'이고, 여기서 가장 적절한 반응은 '반강자성'이다.   
   * 이러한 유사성은 임베딩 간의 subtraction 및 addition 연산 결과에 가장 가까운 단어를 찾아 Word2vec 모델에서 표현되고 해결됨      
<center> ferromagnetic(강자성) − NiFe + IrMn ≈ antiferromagnetic(반강자성)</center>    

-----

**[임베딩 시각화]**      
* **주성분 분석(principal component analysis)을 사용한 시각화**        
  * 이러한 임베디드 관계를 더 잘 시각화하기 위해 주성분 분석(principal component analysis)(그림 1b)을 사용하여 Zr, Cr 및 Ni의 임베딩과 해당 산화물 및 결정 구조를 2차원에 투영했다.         
  * 감소된 차원에서도 '산화물(oxide of)'(Zr - ZrO2 ≈ Cr - Cr2O3 ≈ Ni - NiO)과 '구조(structure of)'(Zr - HCP ≈ Cr - BCC ≈ Ni - FCC) 개념에 대한 벡터 공간에서의 일관된 연산이 있다.       
  * 이는 zirconium이 표준 조건에서 hexagonal close packed (HCP) 결정 구조를 가지고 있고 주요 산화물이 ZrO2라는 사실이 임베딩에 잘 반영됨.       
    ![image](https://github.com/yerimoh/img/assets/76824611/39242ad7-919d-4c9e-ae51-b9c053d30302)
* **Other types of materials analogies captured by the model**     
  * 각 범주의 정확도는 50%에 육박하며, 이는 원래 Word2vec 연구에서 설정한 기준선과 유사함.       
![image](https://github.com/yerimoh/img/assets/76824611/62f885a1-4fab-423b-a57d-9899070b3aae)     
  * 다양한 재료 과학 개념에 해당하는 verifed word analogies의 예.      
      * **첫 번째 열:** tested analogies의 유형      
      * **두 번째 열:** 해당 analogy 유형에 대한 vector operation 예제     
      * **세 번째 열:** 관측된 답      
      * **네 번째 열**: 해당 analogy task의 점수를 매기는 데 사용되는 pairs의 수
      * **다섯 번째 열:** 모델의 결과 점수
      * Application analogies은 정량적으로 테스트되지 않았으며, 이 예는 시연용으로만 사용됩니다. 테스트된 아날로그의 전체 목록은 https://github.com/materialsintelligence/mat2vec 에서 확인가능
  * **단어의 위치를 통한 관계성 표현**        
  * 특히, 우리는 화학 원소의 임베딩이 2차원에 투영될 때, **주기율표**에서 그들의 위치를 대표한다는 것을 발견함     
  * SUPPLEMENTARY INFORMATION 섹션 S4 및 [S5](#supplementary-information)에서 자세히 설명       
  * 활성화 에너지 예측(formation energy prediction—outperforming)과 같은 quantitative machine learning models에서 effective feature vectors 역할을 할 수 있음             
  ➡ 이는 이전에 보고된 몇 가지 선별된 특징 벡터를 능가함(밑의 그림 1c, d, [SUPPLEMENTARY INFORMATION S6](#supplementary-information)).          
    ![image](https://github.com/yerimoh/img/assets/76824611/f8950c86-6e57-4682-8cea-8e9a38fc3980)
* **본 논문의 강조점**       
  * 우리는 Word2vec가 이러한 entities를 단순히 strings로 취급함     
  * 모델에 화학적 해석이 명시적으로 제공되지 않음      
  ➡ 오히려 scientific abstracts에서 **단어의 위치를 통해** materials knowledge이 포착된다             


<details>
<summary>📜 Extended Data Fig. 1 | Chemistry is captured by word embeddings 보기</summary>
<div markdown="1">

  
![image](https://github.com/yerimoh/img/assets/76824611/0dc445ef-82f3-492c-abed-e3fda19ee9be)

* **a,**
해당 원소 기호로 레이블이 지정되고 분류에 따라 그룹화된 100개의 화학 원소 이름(예: 'hydrogen')의 단어 임베딩에 대한 2차원  t-distributed stochastic neighbour embedding (t-SNE) 투영.      
➡ **화학적으로 유사한 원소들이 함께 군집화**되는 것으로 보이며 전체 분포는 **주기율표 자체를 연상**시키는 topology를 나타냄(b와 비교).        
➡ 왼쪽 위에서 오른쪽 아래로 배열된 것은alkali metals, alkaline earth metals, transition metals, and noble gases인 반면, 오른쪽 위에서 왼쪽 아래로 추세는 일반적으로 증가하는 원자 번호를 따른다.      
(자세한 내용은  Supplementary Information section S4  참조).       


<details>
<summary>👀 S4 Word2vec element clustering versus periodic table 보기</summary>
<div markdown="1">

**[주목할 점]**         
과학 텍스트에서 단어의 **상대적인 위치만을 사용**하여 **알고리즘이 평면에 투영**될 때 **주기율표와 매우 유사한 요소에 대한 고차원 표현을 학습**한다는 것은 주목할 만하다.     

그러나 **t-SNE 예상 단어 임베딩의 모든 구조가 주기율표와 잘 일치하는 것은 아니다**.     

이것이 문맥에 기반한 표현이라는 점을 고려할 때, inert noble gases이 나머지 원소들로부터 멀리 떨어져 있는 반면,  
다양한 응용 분야에서 종종 서로 함께 사용되는 물질(post-transition metals, metalloids, and alkali metals) 과 더 가깝게 그룹화되는 것은 당연하다.     

**[주기율표와 다른 사례]**         
* **주기율표 보다 주요 구성 요소끼리 붙어있음**      
   * 수소(hydrogen)가 산소(oxygen), 질소(nitrogen), 탄소(carbon)로 군집되어 있는 것을 관찰할 수 있다.
   ➡ 우리는 이것을 이 원소들이 organic compounds의 주요 구성 요소이기 때문이라고 생각한다.    
   * 마찬가지로, 표에선 모두 방사성 원소인 라돈(Rn, Radon), 라듐(Ra, radium), 폴로늄(Po, polonium)은 주기율표 상의 이웃보다, 우라늄(U, uranium)과 토륨(Th, thorium)에 더 가까운 곳에서 발견된다.
   ➡ <span style="background-color:#fff5b1">주기율표보다 구성요소 관계인 원소끼리 뭉쳐있음</span>           
* **완전히 다름**      
   * 우리의 방식이 non-physical reasons이기 때문에, 일부 원소들은 주기율표와 완전히 맞지 않음.        
   * 우리는 이러한 원소들의 기호가 beryllium의 경우 "be", astatine의 경우 "at", technetium의 경우 "Tc"(temperatures를 뜻하기도 하)와 같이 원소기호가 아니라 **동일한 철자를 가진 일반적인 단어와 겹친다**는 점에 주목한다.       
   ➡ <span style="background-color:#fff5b1">즉, 완전히 다른 일반 언어와 원소기호를 동일시하여 오류가 생겼을 수 있다는 이야기이다.</span>          

그럼에도 불구하고, 임베딩의 높은 차원성은 아래와 같은 관계를 동시에 캡처할 수 있게 하여 **화학적 관계와 구문적 관계를 모두 보존**한다.                

$$“being” - “Be” + “measure” ≈ “measuring”$$      
$$“BeO” - “Be” + “Mg” ≈ “MgO”$$  



</div>
</details>  



* **b,**   
a의 분류를 바탕으로 색을 칠한 주기율표      


* **c.**
원소의 단어 임베딩을 특징으로 하는 간단한 신경망 모델을 사용하여 약 10,000 $$ABC_2D_6$$ elpasolite compounds 의 형성 에너지 예측 대 실제(DFT) 값 (모델의 자세한 내용은 [Supplementary Information section S6](#supplementary-information) 참조).         
그림의 데이터 점은  fivefold cross-validation을 사용함.      



d, f elpasolite formation energies의 10% 테스트 세트에 대한 오차 분포.     
광범위한 optimization이 없으면 단어 임베딩은 원자당 0.056 eV의 평균 절대 오차(MAE)를 달성하는데, 이는 hand-crafted features을 사용한 기존 연구 결과인 원자당 0.1 eV보다 상당히 작다.       


</div>
</details>  






  
-----
----

## thermoelectric관련 실험



**[현 논문의 main advantage and novelty]**       
* 'thermoelectric(열전성)'과 같은 응용 키워드가 '$$Bi_2Te_3$$'와 같은 material formulae과 동일한 표현을 가지고 있다는 것임.   

* material embedding과 'thermoelectric' 임베딩의 cosine similarity이 높을 때,
text corpus는 필수적으로 이 material의 thermoelectric behaviour에 대해 보고하는 abstracts을 포함한다고 예상할 수 있다.    


**[실험 결과 & 가설 설정]**
* 그러나 본 논문의 임베딩 결과, **'thermoelectric'라는 단어와 상대적으로 코사인 유사성이 높은 다수의 물질**(아래 그림 참고)이 발견되었는데,
이 물질이 포함된 **abstract에는 본 물질이 'thermoelectric'라는 것을 명시적으로 나타내지 않는다**.         
➨ 우리는 이러한 사례들을 가짜라고 치부하기보다는, <span style="background-color:#fff5b1">그러한 사례들이 새로운 '**thermoelectric' materials의 예측으로 유용하게 해석**될 수 있는지 조사</span>했다.



<img width="93" alt="image" src="https://github.com/yerimoh/yerimoh.github.io/assets/76824611/e4dcde14-fd0e-41dd-b814-1e0754c5520f">
* thermoelectric materials의 순위는 'thermoelectric'이라는 단어가 포함된 material 임베딩의 cosine similarities을 사용하여 생성될 수 있음.      
* 'thermoelectric' 응용을 위해 아직 연구되지 않은 높은 순위의 물질이 관련선이 있다고 가정할 수 있다.   
 


----

### first test

첫 번째 테스트로, 우리는 예측된 thermoelectric compositions을 available computational data와 비교했다.         


구체적으로 본 논문은 임베딩 결과 중 아래의 과정을 통해 **material을 선정**하고 **선정된 material에 rank** 매긴 것이다.       
* 1️⃣ **예측 기준이 되는 데이터 셋과 비교**      
[density functional theory (DFT)(밀도함수 이론)](https://www.nature.com/articles/sdata201785)을 사용하여 계산된 약 48,000개의 compounds의 **thermoelectric power factors**(전체 thermoelectric 가치 수치(zT)의 중요한 구성 요소)**에 대한 데이터 세트**에 **3번 이상 언급된 물질** 선정        
➨ 그 결과, 두 데이터 세트 사이에 총 **9,483개의 화합물이 중복**됨 확인      
* 2️⃣ **예측 후보 선정**      
중복 물질 중,**7,663개**는 텍스트 말뭉치에서 **thermoelectric 키워드와 함께 언급된 적이 없으며, 예측 후보로 간주**될 수 있다.
* 3️⃣ **예측 후보 rank 설정**         
예측을 얻기 위해, 우리는 이 7,663개의 화합물 각각을 **'thermoelectric'이라는 단어 임베딩으로 정규화**된 **output 임베딩의 dot product**으로 rank를 매겼다.
<img width="271" alt="image" src="https://github.com/yerimoh/img/assets/76824611/6d9949fc-6ffc-40cf-9b67-81cd03884d13">  
(출력 대 단어 임베딩 사용에 [supplementary-information S1](#supplementary-information) 및 [S3](#supplementary-information) 참조).      





**[rank 해석]**            
* 이 rank는 **text corpus에서 명시적으로 발생하지 않았음**에도 불구하고 **해당 물질이 scientific abstract의 'thermoelectric'이라는 단어와 공존**할 가능성으로 해석될 수 있다.       
* density functional theory응 이용해 계산된 power factors        
<img width="155" alt="image" src="https://github.com/yerimoh/img/assets/76824611/71230bdc-7fea-4272-bfc9-edc7bc3cecd0">        
  * fig 구성       
    * **purple:** 1,820개의 알려진 thermoelectrics      
    * **green**: 7,663개의 아직 연구되지 않은 thermoelectric materials 후보 물질    
    * **점선:** 단어 임베딩 접근법에서 가장 높은 순위를 차지한 10개의 후보의 값,      
      상위 10개의 임베딩에 기반한 Power factors (not studied as thermoelectrics in our text corpus)      
      Li2CuSb, CuBiS2, CdIn2Te4, CsGeI3, PdSe2, KAg2SbS4, LuRhO3, MgB2C2, Li3Sb and TlSbSe2     
   * fig 해석
     * **상위 10개 예측(점선)이** 후보 물질의 평균(green), thermoelectric의 평균(purple) 모두에서 **더 좋은 computed power factor**($$μW ^{K-2} cm-^{1}$$)를 갖는다.      
     * 이러한 **상위 10(점선)개 예측**에 대한 40.8$$μW ^{K-2} cm-^{1}$$의 **average maximum power factor의 크기**     
        * 후보 물질(green)의 평균(11.5μW K-2 cm-1)보다 3.6배 크다.
        * 알려진 열전기의 평균(purple)(17.0$$μW ^{K-2} cm-^{1}$$)보다 2.4배 크다.
     * 또한 **상위 10개 예측**에서 가장 높은 세 가지  **power factors**은 **알려진 열전기(purple)의** **99.6번째**, 96.5번째 및 95.3번째 **백분위수**이다.         
     * 우리는 supervised methods와 대조적으로, 우리의 임베딩은 **텍스트 말뭉치만을 기반**으로 한다.       
       즉, **DFT 데이터를 사용하여 어떤 방식으로든 훈련되거나 수정되지 않는다**는 것에 주목한다.     


-----

### second test 

다음으로, 동일한 모델을 실험적으로 측정된 power factors를 [$$zTs$$](https://pubs.acs.org/doi/10.1021/cm400893e)와 직접 비교했다.        


우리의 접근 방식은 이러한 양에 대한 numerical estimations을 제공하지 않기 때문에,     
우리는 텍스트 말뭉치와 실험 세트에 모두 나타나는 83가지 재료에 대해 Spearman rank correlation을 통해 candidates의 상대적 ranking를 비교했다.      

maximum power factor 및 maximum zT에 대한 임베딩 기반 순위와 실험 결과의 59% 및 52%의 rank상관 관계를 얻었다.       

예상치 못하게 우리 모델은 이전 단락에서 사용된 power factor DFT 데이터 세트를 능가했는데, 이는 experimental maximum power factors과 31%의 순위 상관관계만 나타낸다.       



-----


### fianl test     
마지막으로, 모델이 과거 논문을 토대로 trian되었다면,  thermoelectric materials을 제대로 예측하였는지 실험하였다.     


**[실험 1]**     
* 구체적으로, 우리는 2001년과 2018년 사이에 출판된 abstracts으로만 구성된 18개의 다른 'historical' 텍스트 말뭉치를 생성함.        
* 우리는 각 **과거 데이터 세트**에 대해 별도의 단어 임베딩을 훈련했고, 이러한 임베딩을 사용하여 **미래(테스트) 연도에 보고될 가능성이 있는 상위 50개 thermoelectrics를 예측**했다.         


**[결과]**    
* 예측 날짜가 지난 매년, 우리는 thermoelectrics 키워드와 함께 문헌에 보고된 예측 열전 성분의 누적 백분율을 표로 작성했다.     
* 다양한 'historical' 데이터 세트에서 얻은 word embeddings을 사용한 thermoelectric materials 예측 결과.     
<img width="200" alt="image" src="https://github.com/yerimoh/img/assets/76824611/5067e00d-ffbe-473b-a4b0-29e758b21758">      
* **그래프 detail**         
   * 회색 선은'historical' 데이터 세트의 결과(2001년과 2018년 사이에 출판된 abstracts)로 나타냄
   * 예를 들어, '2015'라는 레이블이 붙은 옅은 회색 선은 2015년 1월 1일 이전에 발표된 과학적 추상물에 대해서만 훈련된 모델을 사용하여, 상위 50개 예측 중 1년, 2년, 3년 또는 4년 후(즉 2015-2018년) 열전 키워드와 함께 문헌에 보고된 비율을 나타냅니다           
   * 각 회색 선은 예측을 위해 해당 연도 이전에 publish된 abstracts만 사용한다.       
    (예: 2001년 예측은 2000년 이전의 abstracts을 사용하여 수행됨).            
   * 선은 예측 이후 몇 년 동안 thermoelectrics로 보고된 예측 물질의 누적 백분율을 표시한다.
   초기 예측은 더 긴 테스트 기간에 걸쳐 분석될 수 있으므로 회색 선이 더 길어진다.
   * 결과는 평균(빨간색)이며, 모든 재료(파란색) 또는 [non-zero DFT bandgap materials](https://ceder.berkeley.edu/publications/2013_Jain_Materials_Project.pdf) (녹색)의 기준 백분율과 비교됨       
* **결과 해석**         
   * 전반적으로. 우리의 결과는 **top 50 word embedding-based predictions materials** (빨간색 선)이 그 당시 우리의 말뭉치에서 무작위로 선택된 연구되지 않은 재료(파란색)와 비교하여, **향후 5년 내에 열전기로 연구될 가능성**이 **평균 8배 더 높았**음        
   * 또한 이 **물질(빨간색 선)**이 **non-zero DFT bandgap (녹색)보다 3배 더 높다**는 것을 나타냄      
   * 위 그림에서 시간이 지날수록 더 가파른 기울기로 표시된 것처럼, **더 최근의 데이터를 통합하는 더 큰 말뭉치의 사용은 성공적인 예측의 속도를 향상**시킴           






**[실험 2]**     
* 이러한 결과를 더 자세히 조사하기 위해,      
우리는 **2009년 이전에 발표된 abstracts**만을 사용하여 결정된 상위 5개 예측의 운명에 초점을 맞춤.       

**[결과]**      
* 아래 그림은 다음 해에 abstracts이 더 추가됨에 따라 이 상위 5개 화합물의 예측 순위의 진화를 보여줌          
<img width="204" alt="image" src="https://github.com/yerimoh/img/assets/76824611/e5d3626a-7deb-4051-90c7-4b4c1d793a75">       
* **그래프 detail**     
  * 2009년 데이터 세트의 상위 5개 예측 material     
  * 더 많은 데이터가 수집됨에 따른 이 meterial의  prediction ranks      
  * marker(★): thermoelectric로서 첫 번째 published된 보고서의 year                 
* **결과 해석**      
  *  **$$CuGaTe_2$$**     
    **현재 최고의 thermoelectric 중 하나**이며, 2012년 발표되기 **4년 전에 상위 5개 화합물로 예측**되었다.        
  * **$$ReS_2$$와 $$CdIn_2Te_4$$**     
  우리 알고리즘에서 상위 5개 목록에 처음 등장한 시점으로부터 약 **8-9년 후에 문헌에서 좋은 thermoelectric라고 제안**됨              
  우리는 2015년에 계층화된 **$$ReS_2$$의 순위가 급격히 증가**한 것이, **$$SnSe$$에 대한 기록 $$zT$$의 발견과 일치**한다는 것에 주목한다(이것도 계층화된 물질).    
  * **$$HgZnTe$$와 $$SmInO_3$$**      
  값비싼(Sm, In) 또는 독성(Hg) 요소를 포함하고 있으며 아직 연구되지 않았음     
  $$SmInO_3$$는 더 많은 데이터를 추가함에 따라 순위가 크게 떨어짐      

 
 
2001년과 2018년 사이의 연도별 상위 10개 예측은 Table S3에서 확인 가능


<details>
<summary>📜 Table S3: Top 10 thermoelectric predictions from each year. 보기</summary>
<div markdown="1">

      
materials 목록은 prediction #1에서 prediction #10 순으로 정렬됨       
총 후보는 예측을 위해 고려된 materials의 수이며, 여기에는 3번 이상 언급되었지만 이전에는 열전기로 연구되지 않은 모든 materials가 포함됨.      
총 abstracts은 단어 embeddings을 훈련하는 데 사용되는 (relevant) abstract 수다.



![image](https://github.com/yerimoh/img/assets/76824611/186d5aa3-449d-41ef-b05e-256058dbe2ba)
![image](https://github.com/yerimoh/img/assets/76824611/6cb31ce0-2ef4-4879-a1ae-9c6dbe62c79b)
![image](https://github.com/yerimoh/img/assets/76824611/afe95bb6-dc8b-48dd-b59a-2b004c1f508e)


</div>
</details>  
      

-----
----


## investigated the series of connections

'thermoelectric'라는 단어 옆에 언급되지 않은 물질이 어떻게 높은 기대 확률을 가진 thermoelectric로 식별되는지 설명하기 위해,  
prediction으로 이어질 수 있는 일련의 connections을 조사했다.     

**[thermoelectric로 예측되는 물질과 thermoelectric의 연결 관계 그래프]**           
<img width="233" alt="image" src="https://github.com/yerimoh/img/assets/76824611/211b052a-9731-47ef-9bf6-d8c27fa72aba">    
* **fig detail**      
   * thermoelectric로 예측되는 물질의 context words가 thermoelectric 단어와 어떻게 연결되는지 보여주는 그래프.      
   * **'thermoelectric'과 context words 사이의 edges width(blue):**      
    노드간 단어 임베딩 사이의 cosine similarity에 비례   
   * **material과 context words 사이의 edges width(red, green과 purple):**      
    context words의 단어 임베딩과 material의 출력 임베딩 사이의 코사인 유사성에 비례
   * material는 첫 번째($$$Li_2CuSb$$), 세 번째($$CsAgGa_2Se_4$$) 및 네 번째($$Cu_7Te_5$$) 예측이다.
   * context words는 meterial과 'thermoelectric' 단어 사이의 edge weights의 sum에 따른 top context words다.
   * 경로가 넓을수록 예측에 더 큰 기여를 할 것으로 예상된다.      
   * context words를 검사하면 알고리즘이 아래의 것들을 증명했다.    
      * 결정 구조 연관성 (crystal structure associations)
      * 동일한 응용 프로그램에 대한 다른 재료와의 공동 언급 (co-mentions with other materials for the same application)
      * 서로 다른 응용 프로그램 간의 연관성(associations between different applications)
      * 재료의 알려진 특성을 설명하는 주요 구문
* **결과 해석**     
   * 우리는 상위 5개 예측의 세 가지 재료를 이러한 재료를 '열전성'에 연결하는 몇 가지 핵심 문맥 단어와 함께 제시한다.
     (자세한 사항은 아래 Extended Data Table 2 참고)      
   * 예를 들어, $$CsAgGa_2Se_4$$는 'chalcogenide’, ‘band gap’, ‘optoelectronic’, ‘photovoltaic applications’ 옆에 나타날 가능성이 높다:
      * 'chalcogenides': many good thermoelectrics      
      * ‘band gap’: 이 존재는 대부분의 thermoelectric에 중요
      * 'optoelectronic', 'thermoelectric materials'사이에는 큰 중복이 있다.
        (see [Supplementary Information section S8](#supplementary-information))       
      ➨ 결과적으로, <span style="background-color:#fff5b1"> 이 키워드들과 $$CsAgGa_2Se_4$$사이의 **상관관계**는 **예측**으로 이어짐.</span>    


<details>
<summary>📜 Extended Data Table 2 | Top 50 thermoelectric predictions 보기</summary>
<div markdown="1">
  
![image](https://github.com/yerimoh/img/assets/76824611/1c6c8abe-70d9-4c1a-bc2e-9d0599853796)    
* 작성 시 사용 가능한 full text corpus를 사용한 상위 50개 thermoelectric predictions.        
* 이들 중 일부는 실질적인 한계가 있지만(예를 들어 공기에 민감한 종 또는 독성이 있고 값비싼 요소의 존재), 다른 일부는 실험적으로 테스트 가능한 후보로 보인다.             
* 철저한 매뉴얼 문헌 검색에 따르면 2018년까지 출판된 수집된 abstracts의 전체 말뭉치를 사용한 첫 150개 예측 중 **48개의 재료(32%)가** 이미 훈련에 사용한 **corpus에 표현되지 않은 논문에서 thermoelectric로 연구**되었으며, **이 중 많은 것이 지난 2년 내에 출판**되었다.       
* 여기에 나열된 상위 50개 항목에서 우리는 말뭉치 밖에서 thermoelectric 보고서를 찾을 수 있는 예측을 제외했다. 

</div>
</details>

 
<span style="background-color:#FFE6E6">이러한 **직접적인 해석 가능성**은 meterial 발견부분에서 major advantage다.</span>           



<span style="background-color:#fff5b1">우리는 또한 잘 알려진 thermoelectric material classes가 아님에도 불구하고, **유망한 특성을 나타내는 몇 가지 예측이 발견**되었다는 것에 주목한다.</span>                      
(보조 정보 섹션 S10 참조).       

➨  이것은 <span style="background-color:#FFE6E6"word embeddings이 사소한 구성적 또는 구조적 유사성을 넘어, **인간 과학자가 직접 접근할 수 없는 잠재적 지식을 열 수 있는 잠재력을 가지고 있음**을 보여줍니다.</span>        


--- 

## Generalizability of our approach


**[our approach의 일반화 가능성을 검증]**   
* 마지막 단계로 'photovoltaics', 'topological insulator' 및 'ferroelectric'의 세 가지 추가 키워드에 대한 예측의 역사적 검증을 수행하여,    
접근 방식의 일반화 가능성을 검증함.    
* 우리는 이러한 예측에 사용되는 단어 임베딩이 thermoelectrics 예측과 동일하다는 것을 강조한다.      
* 우리는 단순히 dot product를 다른 target 단어로 수정함.
* 특히 procedure가 거의 변경되지 않은 상태에서 세 가지 functional applications 모두에 대해 아래 그림과 유사한 추세를 발견했으며,       
그 결과는 Extended Data Fig. 2 and Extended Data Table 3.에 요약되어 있다.
![image](https://github.com/yerimoh/img/assets/76824611/0aee9ed7-a667-4c03-b8dd-f2ca262f2261)


<details>
<summary>📜 Extended Data Fig. 2:  Historical validations of functional material predictions </summary>
<div markdown="1">

  
![image](https://github.com/yerimoh/yerimoh.github.io/assets/76824611/119cae2d-beed-4c3f-ba35-6bc0b015ffa2)    
* Ferroelectric **(a)**, photovoltaic **(b)** topological insulator predictions **(c)**         
* 위 3가지 물질은 위의 그림과 유사한 다양한 **과거 데이터 세트에서 얻은 단어 임베딩을 사용**한다.          
* Ferroelectric 및 photovoltaic의 경우 예측 연도 범위는 2001-2018년이다.        
* '‘topological insulator'라는 문구는 2011년(카운트 및 어휘 크기 제한으로 인해)에만 우리 말뭉치에 내장되었기 때문에 더 짧은 기간(2011–2018)에만 결과를 분석할 수 있다.            
* 각 회색 선은 특정 연도 이전에 출판된 요약만을 사용하여 예측한다.      
 이 선은 예측 이후 몇 년 동안 연구된 예측 물질의 누적 백분율을 보여준다.      
 이전 예측은 더 긴 테스트 기간에 걸쳐 분석될 수 있다.       
* 결과는 빨간색으로 평균화되며 모든 materials의 기준 백분율과 비교된다.


![image](https://github.com/yerimoh/img/assets/76824611/6552b6b8-4191-43d9-b86d-d7c8c24fc503)      
* (d) 각 application의 materials 순위를 매기는 데 사용되는 target word 또는 phrase(cosine similarity 기준) 및 잠재적으로 존재하는 연구의 지표로 사용되는 해당 단어

</div>
</details>  


<details>
<summary>📜 Extended Data Table 3: Top five functional material predictions and context words</summary>
<div markdown="1">

![image](https://github.com/yerimoh/img/assets/76824611/f71014d9-aa14-4f7f-b854-8a08c0f01d4b)        
* 전체 텍스트 말뭉치를 사용하여 Ferroelectric, photovoltaic, topological insulator predictions에 대한 예측을 유도하는 상위 5개 예측 및 가장 중요한 상위 10개 context words.     
* Extended Data Fig. 2d에서 언급한 것처럼 대상 영역에서 target 연구를 나타낼 수 있는 context words 목록은 예측을 하는 과정에서 이미 제외됨.      
* 또한 target application에 대한 our corpus 외부의 reports를 찾을 수 있는 예측을 제외함             


  
</div>
</details>  

----


## corpus selection effect

우리의 unsupervised approach의 성공은 부분적으로 **training corpus의 선택**에 영향을 많이 받는다.     

training에 사용한 **abstracts의 주요 목적**은 다음과 같다,      
* training 중 임베딩에서 **노이즈를 증가시킬 수 있는 불필요한 단어를 피하기**     
* 정보를 **간결하고 직접적인 방식**으로 전달           


**[corpus 선택의 중요성]**         
![image](https://github.com/yerimoh/img/assets/76824611/fddab7ec-983b-4399-a812-ec0fcfd41925)         
* **inorganic materials 과학과 관련이 없는 abstracts을 폐기**하는 것이 **성능을 향상**시킴       
* 모든 **Wikipedia articles 세트**에 대해 훈련된 모델(우**리 말뭉치보다 약 10배 많은 텍스트**)이 재료 과학 유추에서 상당히 **더 나쁜 성능을 발휘**한다
* 우리가 모델을 훈련하는 **가장 작은 corpus(Relevant abstract)는 재료 관련 유사성에서 최고의 성능**을 발휘하는 반면,        
가장 큰 말뭉치(Wikipedia)는 문법에서 최고의 성능을 발휘한다.
➡ 우리는 이것이 테스트된 유추 쌍에 적합한 **relevant abstracts의 고도로 전문화된 특성 때문**이라고 생각한다. 우리는 이 연구를 통해 'relevant abstracts' 말뭉치를 사용했다.        
* 기존의 machine learning 모토와 달리 **문제에 더 많은 데이터를 던지는 것이 항상 해결책은 아님**      
➡ 대신, <span style="background-color:#fff5b1">**corpus의 품질**과 **domain-specificity**이 domain-specific tasks에 대한 **임베딩의 유용성을 결정**</span>합니다


<details>
<summary>📝 위 표 설명 자세히 보기</summary>
<div markdown="1">

* **각 수치의 의미**          
top analogy scores는 여러 corpora에 대한  materials science 및 grammatical analogy tasks에 대한 퍼센트이다.            
* **Kim et al.39를 제외한 모든 모델 SETTING**        
trained using CBOW         
동일한 same hyper-parameters
  * 15개의 samples로 negative sampling loss
  * $$10^{-4}$$개의  downsampling
  * window 8
  * size 200
  * initial learning rate 0.01
  * 30 training epochs
  * minimum word count 5
  * no phrases       
* **English Wikipedia dump**      
우리는 2018년 3월 1일부터의 영어 English Wikipedia dump를 사용함
**'Wikipedia elements':** chemical element name(예: 'gold')을 언급하는 글의 하위 집합
**'Wikipedia materials'**: 적어도 하나의 material formula을 언급하는 하위 집합

  
</div>
</details>  


------
-----


# RESULT 

**[장점]**     
* 우리는 여기에 설명된 방법론을 **다른 언어 모델로도 일반화**할 수 있으므로 아래 두가지를 performance로 처리할 수 있다고 함     
  * target application 또는 property를 나타내는 words       
  * entity(예: material 또는 molecule)가 동시에 발생할 확률      
* 이러한 language-based inference methods은 단순히 텍스트에서 entities와 수치를 추출하고 연구 문헌에 존재하는 집단적 연관성을 활용하는 것을 넘어, **자연어 처리와 과학 사이의 교차점에서 완전히 새로운 연구 분야**가 될 수 있음.    


**[개선점]**      
* **context 기반모델 사용**       
  * BERT 또는 ELMo과 같은 context-aware embeddings으로 Word2vec를 대체하면 이러한 모델이 context를 기반으로 단어 embedding을 변경할 수 있기 때문에 functional material predictions을 개선 가능.    
  * context 기반모델은 기존의 모든 NLP 작업에서 Word2vec 또는 GloVe와 같은 컨텍스트 독립 임베딩을 크게 능가함.
  * 또한, 이러한 모델은 동시 발생 외에도 **negation**과 같은 문장에서 **단어 사이의 더 복잡한 관계를 포착**할 수 있음
  **※** 현재의 연구에서는 scientific abstracts 이 종종 긍정적인 관계를 강조하기 때문에 부정의 영향이 다소 완화되는 문제 존재.
* **full texts of articles 사용**
이 작업의 자연스러운 확장은 full texts of articles를 구문 분석하는 것임.
우리는 전체 텍스트가 더 많은 **negation 관계를 포함**하고 일반적으로 **더 가변적이고 복잡한 문장을 포함할 것으로 예상**하므로 더 강력한 방법이 필요할 것임         



**[Comment]**     
* 과학적 진보는 앞으로 가장 유망한 방법을 선택하고 재발명을 최소화하기 위해 **기존 지식의 efficient assimilation에 의존**한다.
➡ 과학 문헌의 양이 증가함에 따라, 이것은 개별 과학자들에게 불가능하지는 않더라도 **점점 더 어려워지고 있**다.
* 우리는 이 연구가  machine-assisted scientific 돌파구의 새로운 패러다임을 가능하게 하는 방식으로,       
과학 문헌에서 발견되는 **방대한 양의 정보를 개인이 접근할 수 있도록 하는 길을 열어주기**를 바란다.


----
----

# METHODS

## Data collection and processing   


아래 방법을 통해 주로 재료 과학, 물리 및 화학에 중점을 둔 approximately **3.3 million abstracts**을 얻음      
* Elsevier’s Scopus and Science Direct application programming interfaces ([APIs](https://dev.elsevier.com/))
* Springer Nature [API](http://dev. springernature.com/)
* web scraping       


**[전처리 방법]**        
* 외국어로 된 abstracts의 일부는 text search 및 regular expression matching을 사용하여 제거함
* 메타데이터 유형이 ‘BookReview’, ‘Erratum’, ‘EditorialNotes’, ‘News’, ‘Events’ and ‘Acknowledgement’에 해당하는 articles 제거          
* 키워드 ‘Foreword’, ‘Prelude’, ‘Commentary’, ‘Workshop’, ‘Conference’, ‘Symposium’, ‘Comment’, ‘Retract’, ‘Correction’, ‘Erratum’ and ‘Memorial’ 등이 포함된 제목의 abstracts 말뭉치에서 선택적으로 제거        
* 일부 abstracts에는 선행 또는 후행 저작권 정보가 포함되어 있으며 regular expression matching 및 heuristic rules을 사용하여 제거.      
* 'Abstract:'와 같은 Leading words와 phrases도 유사한 방법을 사용하여 제거.
* 우리는 binary classifier에 따라 inorganic materials과 관련된 abstracts만 유지함
  (아래의 'Abstract classification' 참조).
* 우리는 일부 관련 없는 Abstract을 유지하는 대신 대다수 관련 relevant abstract를 보장하기 위해 높은 리콜을 위해 classifier를 조정함.
➡ Supplementary Information section S2에서 더 자세히 설명한 것처럼, **관련 없는 abstract를 제거하면 알고리즘의 성능이 크게 향상**됩니다.
* 관련성이 있는 것으로 분류된 **11.5 million개의 Abstract**는 **개별 단어를 생성**하기 위해 **ChemDataExtractor를 사용하여 토큰화**되었다.      
* regular expression 및 rule-based techniques과 결합된 pymatgen을 사용하여, **유효한 화학식으로 확인된 토큰**은 원소 및 공통 multipliers의 **순서가 중요하지 않도록 정규화** (NiFe는 Fe50Ni50과 동일)          
* 원소의 Valence states는 별도의 토큰으로 분할
(예: Fe(III)는 두 개의 별도 토큰, Fe 및 (III)가 됨)
* 우리는 또한 선택적으로 lower-casing와 deaccenting를 제거했
* 토큰이 화학식이나 원소 기호가 아니고 첫 번째 문자만 대문자인 경우에는 단어를 소문자로 표시    
➡ 따라서, 화학식과 약어는 공통적인 형태를 유지한 반면, 문장의 시작 부분에 있는 단어와 고유 명사는 소문자 형태를 유지
* 단위가 있는 숫자는 종종 ChemDataExtractor에 의해 토큰화되지 않았음.
➡ 처리 단계에서 공통 단위를 숫자에서 분할하고 모든 숫자를 특수 토큰 ```<nUm>```으로 변환하여 이 문제를 해결   
➡ 이것은 단어의 크기를 약 20,000개 줄임
* 우리는 **정확한 전처리**, 특히 **individual tokens으로 포함할 phrases 선택**이 **결과를 크게 향상**시킨다는 것을 발견. (즉, 원소와 같은 materials science phrases를 일반단어와 헷갈리지 않도록 individual tokens 부여)             
* 전처리에 사용되는 코드는 https://github.com/materialsintelligence/mat2vec 에서 확인가능      


----

## Abstract classification

이 작업은 inorganic materials science에 초점을 맞춤.       
그러나, 우리의 말뭉치에는 이 범위 밖에 있는 일부 abstracts(예: articles on polymer science)이 포함되어 있었음 

**[binary classifier 제작]**         
1️⃣ 우리는 무작위로 선택된 1,094개의 abstracts에 주석을 달았음. (relevant(588), not relevant(494))               
2️⃣ 위의 주석을 단 abstracts으로 binary classifier training         
3️⃣ abstracts을 'relevant' 또는 'not relevant'으로 레이블을 지정할 수 있는 binary classifier완성          
  - 각 문서가  term frequency–inverse document frequency (tf–idf) vector 벡터로 설명되는 logistic regression에 기반한 linear classifier를 사용함         
  - 분류기는 fivefold cross-validation을 사용하여 89%의 정확도(f1-score)를 달성                     
4️⃣ 이 binary classifier로 inorganic materials science외의 기사를 제거함       




----

## Word2vec training    
* 우리는 [gensim](http:// radimrehurek.com/gensim/)에서 Word2vec 구현을 사용함     
* negative sampling loss (n = 15) 을 갖는 skip-gram이 가장 잘 수행된다는 것을 발견함
(모델 간 비교는 Information section S2).        
* 어휘는 정규화된 화학식은 언급 횟수에 관계없이 추가함.
  그 외는 5회 이상 발생한 모든 단어로 구성
* The phrases were generated using a minimum phrase count of 10, score [threshold of 15](https://arxiv.org/abs/1310.4546)  and phrase depth of 2      
The latter meant that we repeated the process twice, allowing generation of up to four grams     
* 또한 '-', 'of', 'to', 'a', 'the'와 같은 일반적인 용어도 포함했는데, 예외적인 경우에는 더 많은 토큰을 가진 구문으로 이어졌다.      
예를 들어, ' ‘state-of-the-art thermoelectric'은 우리 어휘에 있는 다섯 개의 8개의 토큰 중 하나다.(-포함)   
* 각 구문 생성 주기가 끝날 때마다 구두점과 숫자가 포함된 구문을 제거함        
 어휘의 크기는 구문 생성 후 약 두 배가 되었음
 

<details>
<summary>📜 자세한 hyperparameters 보기</summary>
<div markdown="1">

      
* 200-dimensional embeddings     
* 0.01의 learning rate는 30 epochs에서 0.0001로 감소시킴     
* a context window of 8       
* 가장 일반적인 단어 약 400개를 subsampling with a $$10^{−4}$$ threshold      

 
hyperparameters는 약 15,000개의 문법 및 15,000개의 재료 과학 유사성에 대한 성능에 최적화되었으며,       
점수는 두 세트에서 정확히 '해결된' 유사성의 비율로 정의됨      

hyperparameters 최적화 및 말뭉치 선택에 대해서도 Supplementary Information section S2에서 더 자세히 설명함. 
   
교육에 사용된 코드와 본 연구에 사용된 전체 유추 목록은 https://github.com/ materials intelligence/mat2vec에서 확인가능.


  
</div>
</details>  




----

3️⃣ 예측 후보 순위 설정 방법 자세히 보기    



---
---

# **Supplementary Information**     


<details>
<summary>📜 S1 Word2vec Skip-gram 보기</summary>
<div markdown="1">


**<Figure S1: Word2vec skip-gram>**     
![image](https://github.com/yerimoh/img/assets/76824611/817aae96-5f93-4b29-a468-c63ce601f81c)         
* **a.**       
single linear hidden layer가 있는 neural network은 어휘의 모든 단어에 대한 context words를 예측하는 방법을 배운다.    
배터리 양극 재료 $$LiCoO_2$$와 $$LiMn_2O_4$$의 경우 네트워크는 대부분 동일한 context words를 예측해야 한다.       
그 결과, 두 단어는 유사한 hidden layer weights와 유사한 word embeddings을 갖게 된다.        
softmax 함수는 정규화된 확률을 생성하기 위해 출력에 사용된다.     
* **b.**    
Matrices W와 O는 hidden 레이어와 output 레이어의 가중치에 해당하는 train의 결과임     
**W 행:** word embeddings     
**O 행:** output embedding     
두 가지 유형의 **임베딩의 곱**은 텍스트에서 **해당 단어가 근접하게 사용될 확률**이다.        


 일반적으로 Skipgram이 우리의 애플리케이션에 대해 CBOW보다 더 잘 작동한다는 것을 보여주므로, 우리는 이 작업 내내 **Skip-gram을 사용**함          

* **INPUT**     
전체 어휘 개수(V)를 500,000이라고 가정하여 V = 500,000     
즉, 각 단어를 V차원의 one-hot encoding으로 표현       
이렇게 one-hot encoding으로 표현된 각 단어를 input으로 사용           
* **TASK**        
window size내 단어 예측
신경망의 작업은 행렬 W의 행 w에 행렬 O의 열을 곱하고 소프트맥스 함수를 적용하여 단어 w 옆에 있는 어휘의 모든 단어의 확률을 생성함          
* **GOAL**     
단어에 대한 압축된 표현을 배우는 것       
이 표현은 train이 끝날 때 neural network의 single linear hidden layer의 가중치로 인코딩 됨       
* **weights of the hidden layer**      
**hidden layer의 weights(Materix W):** [V x n] 차원     
**n**: 단어를 "embed"하기 위해 설정한 공간의 크기입니다(이 경우 200)       
**"embed:** 중심 단어의 one-hot encoded vector가 네트워크에 공급되면 매트릭스 W에서 **해당 행을 선택하는 것**이 전부임         
* **OUTPUT LAYER**
그런 다음 출력 계층은 embed를 통해 선택한 행을 softmax classifier의 입력으로 사용하여 **인접 단어 중 하나를 예측**.
예측 후, 예측값과 정답값을 비교하여 가중치 업데이트(행렬 W의 해당 행을 조정)    
이러한 행 벡터를 word vectors 또는 word embeddings이라고 함
마찬가지로 출력 가중치의 [n x V] 행렬 O 열을 output embeddings이라고 함.


</div>
</details> 






<details>
<summary>📜 S2 Word2vec optimization 보기</summary>
<div markdown="1">

**(Table S1: Algorithm choice)**      
![image](https://github.com/yerimoh/img/assets/76824611/de1c19ba-4911-4ada-b534-7a19fb6566c8)    
* materials science 및 grammatical analogy 과제에서 상위 1개의 analogy scores(%)                  
* 각 작업은 약 15,000개의 analogy pairs으로 구성됨.       
* 가장 가까운 첫 번째 단어가 예상되는 유추와 일치하는 경우에만 정답으로 간주됨            
* **Default:** Word2vec 코드의 원래 하이퍼 파라미터를 사용        
  **다른 4개의 Word2vec:** 최적화된 하이퍼 파라미터를 사용          
  **GloVe**: original pape의 권장 매개 변수를 사용, 컨텍스트 창과 매개 변수 알파를 최적화하려고 시도한 후 **최상의 성능을 발휘**
* **phrases:**  individual tokens으로 포함할 phrases 선택 (즉, 원소를 일반단어와 헷갈리지 않도록 individual tokens 부여)      

 

**(Table S2: Hyper-parameter optimization)**     
![image](https://github.com/yerimoh/img/assets/76824611/e9ec6130-d3e4-4819-8234-8602d5842d1c)       
* 다양한 hyper-parameter 선택에 대한 상위 1개의 analogy score(%).
* 표에 언급된 하나의 파라미터만 변경되고 나머지 파라미터는 동일하게 유지              


**(Figure S2: Accuracy of predictions)**         
![image](https://github.com/yerimoh/img/assets/76824611/71c58450-788f-404b-8998-6c4d19cc31a2)        
* **a.**       
다양한 알고리즘 및 parameters에 대한 성능 메트릭        
  * **Word analogies (blue):** materials science 및 grammatical analogy task에 analogy scores      
  * **Thermoelectric ranking score (green)**: 우리 예측의 순위와 약 80개의 재료에 대해 실험적으로 측정된 thermoelectric 값 사이의 Spearman rank correlation coefficient                          
  * **power factor score (red)**: 비교를 위해, 동일한 데이터 세트의 DFT와  experimental power factors의 상관 관계는 0.31다      
     * $$\frac{PF_{pred10}−PF_{mean}}{PF_{best10}−PF_{mean}}$$        
     * $$PF_{mean}$$: 모든 후보 power factor의 평균        
     * $$PF_{pred10}$$: power factor의 처음 10개 예측의 평균       
     * $$PF_{best10}$$: power factor의 가장 높은 10개의 평균         
* **b.**      
a score의 변화      
“Phrases + Skip-gram” model over 30 training epochs             
learning rate는 10^{-2}에서 10^{-4}로 선형적으로 감소         
* **detail**      
  * Fig. S2a는 다른 모델과 매개 변수에 대한 30 training epoch 후 점수를 보여준다.    
  analogy scores와 유사하게, 우리는 Skip-gram이 CBOW보다 더 잘 수행되고, "phrases"을 포함하면 성능이 향상된다는 것을 알 수 있다.         
  * 또한 모든 **Word2vec 모델**은 thermoelectrics 순위에서 **GloVe를 능가**한다.            
  ➡ 우리는 이것을 **Word2vec의 예측 특성**과 **순위 및 예측을 위한 출력 임베딩의 사용** 때문이라고 생각한다. (S3 참조).     
  ➡ GloVe는 카운트 기반이며 추가 출력 임베딩 세트를 제공하지 않음

우리는 Word2vec의 hyper-parameters를 조정하여 결합된 materials science과 grammatical analogies에 대한 성능을 최적화함.      

**[성능]**       
* **"phrases"을 포함**하면 표 S1에 표시된 것처럼 CBOW 및 Skip-gram 아키텍처 모두에서 성능이 약 **4% 향상**됨        
* **Skip-gram은** "phrases"가 있는 경우와 없는 경우 모두에서 **CBOW보다 약 4% 더 나은 성능을 발휘**합니다         
* 더 빠른 trian을 위해 더 빠르기 때문에 negative sampling loss을 사용함     
* GloVe embeddings이 Word2vec보다 성능이 조금 낮음 (Table S1)       


**[analogy-based optimization이 실제 예측에 도움을 주는지]**        
우리는 analogy-based optimization가 materials predictions에 도움을 주는 지의 여부를 특정하기 위해 2가지  additional metrics을 사용했다.      
* **1) quantify the quality of the predictions**          
predictions을 위해 average power factor of the first 10 predicted thermoelectrics을 사용함       
* **2) quality of the ranking**       
rank 계산을 위해, 약 80개의 experimental thermoelectri 수치에 대한 우리 순위의 Spearman rank correlation를 계산함
* **결론**
Figure S2b를 봤을 때 epoch 5 이후로 power factor이 1) quantify the quality of the predictions(word analogies)와 2) quality of the ranking (thermoelectric ranking)의 증가와 유사한 증가를 보이고 있다.
➡ 즉, 유의미하다.        


</div>
</details> 





<details>
<summary>📜 S3 Word versus output embeddings for predictions 보기</summary>
<div markdown="1">
  
  

**[Figure S3: Word vs output embeddings]**          
![image](https://github.com/yerimoh/img/assets/76824611/c7674bfa-7420-4b49-a0e3-44ced1b8afd8)          
* **Word embeddings:** application keyword와 material formula 모두에 대해 Word embeddings을 사용하는 것      
* **output embeddings:** formula의 output embedding과 application keyword의 Word embedding 을 사용하는 것          



**[ranking(결과적으로 predictions)의 선정 방법]**           
* **ranking(그리고 결과적으로 예측):** application keyword(예: “thermoelectric”)의 임베딩과 모든 materials의 임베딩(일부 카운트 임계값, 우리의 경우 3 이상)을 곱하여 수행됩니다.
의 임베딩과 모든 재료의 임베딩(일부 count  threshold, 우리의 경우 3 이상)을 곱하여 수행 도출됨
  * **application keyword**: 항상 normalized word embedding을 사용
  * **materials**: word or the output embedding을 사용 (아래 그림 참조)
   ![image](https://github.com/yerimoh/img/assets/76824611/a1c3f529-bf09-4df6-8d1c-79a446084b0b)
* **1) word embeddings을 사용할 경우**    
**application keyword와 word embeddings의 유사성을 기준**으로 순위가 결정됨        
➡ ⚠ 이것을 텍스트의 상호 교환성으로 생각할 수 있다.
* **2) materials의 normalized output embedding을 사용하는 경우**       
모든 materials이 텍스트에서 동일한 횟수로 언급된 경우, application keyword와 material formula가 서로 옆에 언급될 가능성을 기반으로 예측이 이루짐
➡ **2) materials의 normalized output embedding을 사용하는 경우** 가 일반적으로 그림과 같이 **더 나은 결과**를 산출함(실험 전반에 이 방법을 채택)         



</div>
</details> 

S4 Word2vec element clustering versus periodic table는 본문에 있음    



<details>
<summary>📜 S5 Linear regression for elemental properties 보기</summary>
<div markdown="1">


**(Figure S4: Predictions of Elemental Properties)**        
![image](https://github.com/yerimoh/img/assets/76824611/0b29f714-a768-4bdc-a06e-76da82b7be8a)
*  **a-g**
  * linear regression를 사용한 7개 원소 특성의 5-fold cross-validated prediction          
  * 원소 이름(예: "hydrogen, 수소")의 word embeddings의 처음 15개 주요 구성 요소가 features로 사용됨.
  * 각 plot 마다 5개의 서로 다른 모양은 정확한 cross-validation splitting을 나타냄.(사각형, 삼각형 등)
  각 모양(예: 사각형)은 4개의 다른 모양(예: 삼각형, 다이아몬드, 원, 오각형)으로 표시되는 훈련 요소를 사용하여 예측된 일련의 유효성 검사 요소를 나타냄
* **h.**      
   * 20개의 무작위 80%(training) / 20%(validation) 분할에서 validation R2 scores(백분율)의 평균 및 표준 편차.     


**[목적]**        
우리는 **embedding을 features로 사용하여 각 속성을 예측**하기 위해, linear regression를 fitting하였다.   
이를 통해 **embedding space**에 **원소 properties와 관련된 directions이 있는지** 없는지의 여부를 결정할 수 있다.       

**[test]**    
위 목적을 알아내기 위해, 다음 7 원소 properties에 대해 테스트한다:        
* 7 원소 properties
  * 주기율표의 행과 열        
  * Mendeleev number(멘델레예프 수)     
    ![image](https://github.com/yerimoh/img/assets/76824611/9acb3454-a0bc-4ae3-a2a8-ef1ee4cb15b7)     
  * atomic weight(원자량)      
  * melting temperature     
  * covalent radius(공유 반지름)      
  * electronegativity (전기 음성도)        
* 위의 그래프를 확인해보면 양의 상관관계가 보이므로 **embedding space**에 **원소 properties와 관련된 directions이 있다**는 것을 알 수 있다.         


**[추가 tatic: 차원 축소]**        
200 features이지만 원소는 100개 정도이므로 선형 회귀 분석처럼 단순한 모형도 overfit할 가능성이 있다.       
이를 피하기 위해 정규화된 단어 임베딩에 principal component analysis (PCA)을 적용하여 차원을 15로 줄인다.       
new features은 원래 200개의 inear combinations이며 총 분산의 65%를 설명한다       



</div>
</details> 


<details>
<summary>📜 S6 Formation energies of ABC2D6 elpasolites 보기</summary>
<div markdown="1">
  
**<Figure S5: Formation energies of ABC2D6 elpasolite>**        
![image](https://github.com/yerimoh/img/assets/76824611/6b818cde-fe30-45f6-b0ce-9a026e585dc3)
* **a.** 예측에 사용되는 architecture of the neural network         
* **b.** 서로 다른 hidden layer sizes뿐만 아니라 4개의 다른 feature 선택에 대한 Validation 및 test scores.     
hidden neurons가 800이상이면 word embeddings 성능을 크게 향상시키지 않는다.     



우리는 features로 원소의 단어 임베딩 (Word2vec 및 Glove 모두 테스트됨)만을 사용하여 $$55.7 meV/atom$$의 평균 절대 오차를 가진 elpasolites의  formation energies를 예측할 수 있었다.      

* **dataset:**     
[reference[9]](https://pubmed.ncbi.nlm.nih.gov/27715098/)에서 제공하는 약 10,000개의 $$ABC_2D_6$$ 자료로 구성된 dataset를 사용    
* **architectures:**     
activation function으로 ReLU 를 사용하는 simplest neural network architectures      
촐력은 단일 출력임     

* **dataset split**         
입력의 경우 $$ABC_2D_6$$원소의 각 A, B, C, D 원소 임베딩을 연결하고,     
A와 B가 동일하기 때문에 각 material에 대해 2개의 training examples을 만들어 데이터를 augment한다.          
데이터를 **training, validation and test sets로 분할**한 후 이 데이터 augmentation 수행하여 일반화 가능성을 검증한다.       
➡ 이 확대 방식을 사용하면 최고 성능의 모델 테스트 세트의 평균 절대 오차가 69.2 meV/atom에서 55.7 meV/atom으로 감소함     
* **test alternative feature vectors**        
또한 이전 섹션의 7가지 원소 특성으로 구성된 요소의 one-hot encoding 및 min-max scaled(0과 1 사이 값) vectors와 같은 동일한 신경망 아키텍처로 여러 featuer vector를 실험 했다.     
* **hidden layer**         
hidden layer의 다양한 크기뿐만 아니라 다양한 기능에 대한 성능이 그림에 요약되어 있다.        
* **score**       
단어 임베딩(이 최고의 성능을 발휘합니다. 표시된 유효성 검사 점수는5-fold cross-validation의 mean absolute errors(MAE)다.
train 전에 분리된 10% test 세트에 대해 test 점수가 보고된다.       

</div>
</details>  





<details>
<summary>📜 S7 Zero versus non-zero band gap classification 보기</summary>
<div markdown="1">


**(Figure S6: Prediction of zero vs non-zero band gaps)**           
![image](https://github.com/yerimoh/img/assets/76824611/ae5d9479-89cf-4453-b590-f6badbb4f782)    
* **a.** 20개의 다른 무작위화된 train / validation 분할에 최적화된 hyper-parameters를 사용한 5-fold cross-validation의 confusion matrix           
* **b** a에 표시된 5-fold cross-validation의 decision function value 분포.       
**0보다 작은 값:** zero band gap         
**0보다 큰 값**: non-zero band gap                 

**[corpus]**        
reference [[11](https://pubmed.ncbi.nlm.nih.gov/29946023/)]에서 실험적인 band gaps을 가진 1544개의 materials가 우리의 text corpus 안에 있다    
* band gap이 0인 603개의 materials
* zero band gap인 941개의 materials             

**[SVM trian]**        
unit length로 정규화된 materials의 200-dimensional word embeddings을 features로 사용하여,     
zero vs non-zero band gap materials를 구별하기 위해 radial basis function (RBF) kernel이 있는 support vector machines (SVM) 분류기를 훈련했다.     
SVM에서 parameters C (regularization)와 γ (inverse of the standard deviation of the kernel) 에 대한 하이퍼 파라미터 최적화는 grid search을 사용하여 수행했다.          

**[RESULT]**       
* 20개의 random m train / validation splits 80%/20%에 대한 average f1-score 가 채점에 사용되었음.       
γ = 2.34 및 C = 1.83에 대해 90.8 ± 1.0%의 가장 높은 f1-score가 얻어졌다.      
* 그 결과를 위 그림 a에서 최적의 hyper-parameters를 사용하여 re-shuffled (test) 데이터 세트에 적용되는 5-fold cross-validation에 해당하는 confusion matrix를 표시함     
* 위그림의 b에서 우리는 이러한 예측에 대한 decision functions의 분포를 그림으로 표시하여 좋은 separation을 보여준다


</div>
</details> 







<details>
<summary>📜 S8 Material maps 보기</summary>
<div markdown="1">






화학 원소와 유사하게, 아래의 그림과 같이 material formulas의 word embeddings을 2D로 시각화할 수 있다.          
  

**(Figure S7: Material maps)**
![image](https://github.com/yerimoh/yerimoh.github.io/assets/76824611/96ef22f7-8c34-4431-aee7-24fc7e84fb84)    
* **a.**      
   *  t-SNE는 말뭉치에서 최소 10번 언급된 재료에 해당하는 12,340개의 word embeddings을 투영함.          
   * 각 점은 unique stoichiometry(화학 반응에서 질량관계를 다루는 화학의 한 분야)을 나타냄(즉 질량만 다르고 같은 원소로 이루어진 물질)       
   * materials의 상대적인 거리는  context-based similarity으로 해석될 수 있다.       
   * materials는 high density areas을 함께 그룹화하는 DBSCAN을 사용하여 unsupervised 방식으로 클러스터링된다.     
   * 각 군집의  labeled material는 해당 군집 내에서 “most connected”" material에 해당한다.     
   * 이것은 word embeddings의 cosine similarities에 해당하는 weights와 함께 각 클러스터 내의 [PageRank](https://en.wikipedia.org/wiki/PageRank)을 사용하여 결정된다.         
* **b.**           
   * A region of the map in a, $$PbTe$$ (가장 일반적인 thermoelectric 재료 중 하나)       
* **c.**         
   * a.의 각 클러스터에서 가장 일반적인 8개의 원소를 계수하고, 화학량론적(stoichiometry) 비율에 따라 재료당 1개씩 계산한다.         

**[Figure S7 detail]**       
* **S7a.:**      
DBSCAN라는 unsupervised clustering algorithm을 사용하여 몇 개의 대규모 클러스터를 강조한다.       
또한 검색 엔진이 웹 페이지의 순위를 매기는 데 자주 사용하는 알고리즘인 PageRank을 사용하여 각 클러스터 내에서 가장 "connected" 자료를 표시한다.
DBSCAN 및 PageRank의 구현 세부사항은 다음 섹션에서 설명한다.       
* **S7b.:**
$$PbTe$$(그림 S7b)로 클러스터를 확대하면 모두 thermoelectric chalcogenides이다.     
마찬가지로, $$LiFePO_4$$를 사용하는 클러스터는 대부분 리튬 이온 배터리 재료를 포함하고 있으며,      
$$CdS$$를 사용하는 클러스터는 태양 전지 등에 주로 사용되는 재료로 구성되어 있다.
이렇게 각 클러스터의 공통 요소를 그림으로 요약한다.
* **S7c:**    
이러한 원소가 특정 functional application 내에서 **일반적으로 사용되는 원소와 일치함**을 확인한다.    



**(Figure S8: Dynamic material maps)**      
![image](https://github.com/yerimoh/img/assets/76824611/4ae5fd63-8dbd-46c8-b65c-7a352ab5d3a6)
* Material maps은 다양한 키워드에 따라 강조 표시된다.        
* **더 어두운 색**은 **더 유사**하다.       







**[long range order의 의미]**                       
* **thermoelectrics와 photovoltaics**와 같은 Applications은 일반적으로 높은 도핑이 필요한 중간 대역 반도체를 포함하기 때문에 서로 **병합**된다.(S7에 a를 보면 회색(photovoltaics)과 파란색(thermoelectrics)클러스터가 겹쳐있다.               
그림 S7c는 photovoltaics으로 표시된 클러스터가 대부분 sulfides($$S$$)과 selenides($$Se$$)로 구성되어 있음을 보여준다:       
chalcogenides($$S$$, $$Se$$을 구성요소로 갖음)는 thermoelectrics로도 사용된다           
* 흥미롭게도, photovoltaics에도 사용될 수 있는 $$GaAs$$(보라색)를 포함하는 III-V 반도체가 있는 클러스터는 $$CdS$$(II-VI 반도체)(회색)와 거리가 먼데, 이는 이 application이 지도상의 위치를 결정할 뿐만 아니라 **similarity of chemical compositions도 결정**하기 때문이다.    
이것은 **materials의 이름이 텍스트의 formula 옆에 언급될 때 직접 인코딩**될 수 있다.    
예를 들어, "GaAs" 옆에 "gallium arsenide"이 있다.      
* **지도의 위치에 따른 물질**    
  * 지도의 위쪽에 있는 많은 물질은 oxides(산화물)         
  * 오른쪽 아래는 metallic(금속)   
  * 중앙에서 아래로 뻗어있는 물질은 semiconductors(반도체)     
  * 왼쪽 아래는 organic(유기물)        
* 이와 같이, material이  band-gap with 90.8% accuracy (f1-score)을 가지고 있다면,  **compositions에 대한 명시적인 지식 없이 word embeddings of materials만 features으로 사용하여 예측 가능**하다.       




재료가 구성 기반 표현을 사용하여 보고된 91.4% 점수와 유사한 90.8% 정확도(f1-점수)의 밴드 갭을 가지고 있는지 예측할 수 있습니다(자세한 내용은 보충 정보 참조).

similar to a reported 91.4% score using a composition-based representation11 (see Supplementary Information for the details).

* 우리는 아래와 같은 keyword의 cosine similarity에 따라 2D 맵에서 각 material를 색칠하여 material / keywords 유사성의 동적 시각화를 만들 수 있었다:         
application word(예: "thermoelectric"), 재료 클래스(예: "alloys") 또는 결정 구조(예: "perovskite") 
* 예를 들어, S8a      
  * thermoelectric이라는 단어에 따라 강조 표시된 지도에서 더 높은 유사성를 갖으면 어두운 색상으로 보여줌       
thermoelectric는 많은 유형이 있기 때문에, 모든 열전기가 함께 군집화될 것으로 기대해서는 안됨.        
일부 materials는 다른 contexts에서 다른 용도로 사용되므로 main cluster($$Bi_2Te_3$$ 및 $$PbTe$$와 같은 기존 열전기를 포함하는 cluster)에서 더 멀리 떨어져있음      
  * 2014년에 기록적인 power factor을 가진 최근에 발견된 thermoelectric인 $$SnSe$$도 이 클러스터에 있다.      
  * $$CuGaTe_2$$는 또한 thin film solar cells의 유망한 후보로 고려되는 잘 알려진 반도체다.
  * $$Mg_3Sb_2$$는 [Zintl](https://en.wikipedia.org/wiki/Zintl_phase) 구조을 가진 thermoelectric이다.
  * $$Cu_2Se$$는 thermoelectric와 같은 최근 발견된 ion-liquid       
  * $$Ca_3Co_4O_9$$는 oxide thermoelectric     
  * $$Fe_2VAL$$은 heusler-type nonmagnetic semimetal     
  * $$CuCrSe_2$$는 layered antiferromagnet 및 superionic conductor
  * $$YbAl_3$$는 기록적인 power factor를 가진 금속 간 화합물      
  




</div>
</details>  










<details>
<summary>📜 S9 Projection, clustering and ranking of materials embeddings 보기</summary>
<div markdown="1">

  



**[Projection]**   
* fig S7a, our corpus 에서 10번 이상 언급된 12,340개 재료의 200차원 임베딩은 t-SNE을 사용하여 2차원으로 축소되었음          
* cosine distance를 metric, perplexity 30, learning rate 200, early exaggeration 12.0, 10,000 iterations를 사용한 embedding들 사이의 cosine distance를 사용함:            
PCA를 사용하여 초기화된 좌표로 사용          

**[Clustering]**        
* 더 쉽게 시각화할 수 있도록 2D projection의 고밀도 영역을 그룹화하기 위해 DBSCAN이라는 비지도 클러스터링 기술을 사용      
* neighbour distance cutoff  = 2.75 와  minimum count of 8을 사용하여 잘 분리된 클러스터를 생성했음.
* 재료가 120개 미만인 군집은 무시되었음
* 최종 시각화를 위해 나머지 18개 클러스터 중 8개 클러스터를 선택            


**[Ranking]**          
* 각 cluster 내에서 대표적인 자료를 찾기 위해 igraph소프트웨어 패키지를 통해 사용할 수 있는 PageRank구현을 사용함     
* 방향이 지정되지 않은 그래프의 각 node는 material에 해당함     
* edges의 weights은 materials 간 cosine similarities에 해당     
* (S7a.) default damping value of 0.85를 사용하여 각 클러스터 내의 순위를 계산했으며, 가장 높은 순위의 재료는 그림으로 표시되음       
*  전 세계적으로, 우리의 corpus(화학적 요소 제외)에서 가장 많이 연결된 5가지 물질은 $$TiO_2$$, $$ZnO$$, $$SiO_2$$, $$Al_2O_3$$ 및 $$SiC$$로, 모두 대규모 스펙트럼 applications에 사용됨       



**(S7)**     
![image](https://github.com/yerimoh/yerimoh.github.io/assets/76824611/8260cf21-069b-4995-ab16-fb431a301101)


</div>
</details> 


<details>
<summary>📜 S10 Unconventional thermoelectric predictions 보기</summary>
<div markdown="1">

   

잘 알려진 thermoelectric material classes 외에도, 잘 알려진 thermoelectrics과 strong similarity이 없는 $$KAg_2SbS_4$$(아래 그림 참조)도 관찰함     
이 특정 화합물은 최근 photovoltaic material로 제안되었다.    

또 다른 예는 2010년 역사적 말뭉치(보완 표 S5)에서 최상위 예측이었고 계산된 p형 역률이 25.4 µW/K2·cm(메인 텍스트의 방법 섹션에 설명된 제약 조건을 사용하여 계산됨)인 비정상적인 옥시염소산염인 BiOCl이 우리 데이터 세트 역률의 93%에 해당합니다. 옥시염화물 화학의 잠재적인 문제는 큰 밴드 갭과 도핑 가능성일 수 있습니다. 그러나 이 재료에는 높은 계산 역률을 담당하는 비대칭 지점 X와 R29에 정렬된 두 개의 이중 축퇴 원자가 밴드 피크를 포함하여 바람직한 밴드 구조 기능이 포함되어 있습니다. ZnSiP2는 2005년에 3위였고 33.2의 비슷한 높은 p형 역률을 가지고 있습니다∙W/K2 · cm(95백분위수) 및 n형 역률 29.5µW/K2 · cm (n-type 역률 중 96번째 백분위수). 인산화물은 일반적으로 열전 응용 분야에서 바람직하지 않은 높은 열전도율을 갖는 것으로 생각되지만, 이것은 엄격하게 사실이 아니며 이 화합물이 해당되는지 여부는 분명하지 않습니다. 이 물질은 또한 감마 지점 31에서 삼중 축퇴된 원자가 밴드 피크 및 이중 축퇴된 전도 밴드 포켓뿐만 아니라 Z와 Δ1 사이의 축퇴된 전도 밴드 포켓을 포함하는 밴드 구조 특징 때문에 흥미롭습니다. 또 다른 주목할 만한 예는 Nd0.5Sr0.5MnO3(2004년 5위)입니다. 이 화합물에 대한 계산된 역률은 밀도 함수 이론 방법으로 모델링하기 더 어려운 사이트 장애를 나타내기 때문에 데이터 세트에서 누락되었습니다. 그러나 실험적으로 열전도율이 상대적으로 낮은 것으로 알려져 있습니다(< 3 W/K 300 K에서 m). 32, 높은 도프성, 높은 전기 전도율(> 300 S/cm 300 K)33 - 모두 높은 zT 물질에 대한 유망한 지표입니다. 이러한 각각의 예는 비전통적인 화학으로 인한 도핑 및 열전도성의 잠재적 한계를 극복하기 위해 추가적인 합성 및 최적화 작업이 필요할 수 있지만, 그럼에도 불구하고, 그들은 주류 열전학과 밀접한 관련이 없는 실행 가능한 열전 후보입니다.

In addition to well known thermoelectric material classes, we observe predictions such as KAg2SbS4 (see Table 2 of extended data) that do not have strong similarity to known thermoelectrics. This particular compound has recently been suggested as a candidate photovoltaic material28. Another example is BiOCl, an atypical oxychloride which was the top prediction in the 2010 historical corpus (Supplementary Table S5) and has a computed p-type power factor of 25.4 µW/K2 · cm (calculated using the constraints described in the Methods section of the main text) – ranking in the 93rd percentile of our dataset’s power factors. Potential issues with the oxychloride chemistry might be large band gaps and dopability. However, this material contains desirable band structure features, including two doubly-degenerate valence band peaks aligned at the off-symmetry points X and R29 that are responsible for the high computed power factor. ZnSiP2 was #3 in 2005 and has a similarly high p-type power factor of 33.2µW/K2 · cm (95th percentile) and n-type power factor of 29.5µW/K2 · cm (96th percentile among n-types power factors). Phosphides are typically thought to have high thermal conductivities not desirable for thermoelectric applications, however, this is not strictly true30 and it is unclear if that is the case for this compound. This material is also interesting due to its band structure features, which include a triply degenerate valence band peak and doubly-degenerate conduction band pocket at the gamma point31, as well as a degenerate conduction band pocket between Z and Σ1. Another notable example is Nd0.5Sr0.5MnO3 (#5 in 2004). The computed power factor for this compound is missing from our dataset since it exhibits site disorder that is more difficult to model with density functional theory methods. However, it is known experimentally to have a relatively low thermal conductivity (< 3 W/K · m at 300 K)32, high dopability, and high electrical conductivity (> 300 S/cm at 300 K)33 – all promising indicators for a high zT material. Each of these examples may require additional synthesis and optimization work to overcome potential limitations in doping and thermal conductivity due to their unconventional chemistries, nevertheless, they are viable thermoelectric candidates that are not closely related to any mainstream thermoelectrics.


![image](https://github.com/yerimoh/img/assets/76824611/471e3965-1d11-4e54-8d9d-f2101322aeec)

</div>
</details> 

