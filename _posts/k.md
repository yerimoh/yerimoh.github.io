ㅏ---
title: "Quantifying the advantage of domain-specific pre-training on named entity recognition tasks in materials science
 정리" 
date:   2023-08-17
excerpt: "Quantifying the advantage of domain-specific pre-training on named entity recognition tasks in materials science"
category: [Paper]
layout: post
tag:
- Paper
order: 0

comments: true
---

   **[원 논문]**     
[Quantifying the advantage of domain-specific pre-training on named entity recognition tasks in materials science](https://www.sciencedirect.com/science/article/pii/S2666389922000733)


-----


# THE BIGGER PICTURE 
새로운 materials 발견을 기존 문헌에 효율적으로 연결하는 데 병목 현상이 발생했음.     
그래서 이를 해결하기위해 materials science articles에서 **중요한 정보를 자동으로 수집**하도록 네 가지 언어 모델을 교육한다.      
그리고 materials 과학 지식을 갖춘 간단한 모델(BiLSTM)을 3가지 science model과 비교한다.       
**1)** 일반 지식을 갖춘 모델 (BERT)    
**2)** 일반 과학 지식을 갖춘 모델 (SciBERT)    
**3)** materials 과학 지식을 갖춘 모델(MatBERT)    

그 결과,    
* **MatBERT가 전반적으로 가장 성능이 좋음**을 발견함.          
이것은 materials 과학 지식을 담은 언어 모델이 materials 과학 관련 작업에서 더 잘 수행할 것임을 암시한다.     
* 더 간단한 모델은 심지어 지속적으로 BERT를 능가한다.           
* 모델이 **배울 정보 추출의 예가 더 적을 때 성능 격차가 증가**     


MatBERT의 더 높은 품질의 결과는 materials 과학 문헌에서 정보 수집을 가속화해야할 것이다.     


----

# SUMMARY
많은 established literature로 인해 **새로운 재료 발견을 기존 문헌에 효율적으로 연결하는 데 병목 현상이 발생**함      
이 문제는 **NER(Named Entity Recognition)** 를 사용하여 <span style="background-color:#fff5b1">**비정형 재료 과학 텍스트**에서 **구조화된 요약 수준 데이터**를 **추출**함으로써 해결</span> 가능.    

**[실험]**
우리는 3개의  materials science datasets에서 4개의 NER 모델의 성능을 비교함.      
* **4개의 모델:**
a bidirectional long shortterm memory (BiLSTM)      
domain-specific materials science pre-training 정도가 증가하는 3개의 transformer models(BERT, SciBERT 및 MatBERT)이 포함됨

**[결과]**       
* **MatBERT**는 다른 2개의 BERTBASE 기반 모델보다 1%~12% 향상되 **domain-specific pre-training이 측정 가능한 이점을 제공**한다는 것을 의미함       
* **BiLSTM** 모델은  **domain-specific pre-trained word embeddings** 때문에 BERT를 지속적으로 능가
* 게다가, **MatBERT와 SciBERT** 모델은 **작은 데이터 한계에도 original BERT 모델보다 더 우수**      

 
 MatBERT의 materials science literature에서 **구조화된 데이터 추출을 가속화**해야한다.        

----


# **INTRODUCTION**
**[PROBLEM]**        
* 최근 재료 과학 분야의 출판물 수가 기하급수적으로 증가하고 있다.       
그 결과, 연구자들은 상대적으로 <span style="background-color:#fff5b1">제한된 하위 영역 내에서도 **연구 성과를 따라가기가 점점 어려워지고 있다**</span>       
* <span style="background-color:#fff5b1">재료과학 문헌이 매우 많아 졌다는 것은 이전에 **특정 응용을 위해 연구된 재료 후보들이 어떤 것**인지와 같은 **비교적 간단한 질문**들조차도 포괄적으로 **대답하기가 어렵거나 불가능**할 수 있다</span>는 것을 의미한다.       
* <span style="background-color:#FFE6E6">이것은 **관련 문헌과 관련된 정보를 추출**하기 위한 **새롭고 효율적인 방법에 대한 필요성**을 창출함</span>           


**[Motivation]**      
* **Natural language processing (NLP)로 접근**해 위 문제 해결 시도.        
NLP는 많은 재료 과학 응용 분야에 성공적으로 적용되었고 재료 정보학 분야에서 최근 몇 가지 연구의 주제이기 때문        
* BERT와 같은 **transformer ML 아키텍처**의 등장은 NLP를 벤치마크화했다          
Transformer models 은 downstream tasks을 위해 pre train과 fine tuning의 개념을 도입합.    
이 방식은 task별 모델이 비교적 적은 hand-annotated examples를 사용하여 교육될 수 있도록 한다.      
* single pre-trained model이 여러 NLP 작업(예: QA, NER, 다음 문장 예측)을 처리할 수 있지만,
domain-specific pre-training 모델(예: BioBERT, CaseHOLD)의 성공이 아래의 질문을 제기한다.
<span style="background-color:#FFE6E6"> **can transformer models be further improved with even more domain-specific pre-training?**</span>
즉, domain-specific pre-training을 transformer에 model에 적용해해도 성능이 좋을까라는 의문이다.


**[Main Idea]**       
* domain-specific pre-training로 보여졌던 측정 가능한 이점(예: SciBERT)이 **재료 과학과 같은 더 좁은 과학 분야에 특화된 모델**로 **다시 확장될 수 있다고 가정**        
✨ 여기서, domain-specific 모델 성능이 향상되었다는 것은 (NLP 모델의 관점에서) 가장 복잡하고 성가신 과학 영역에서도 **자동화된 지식 추출 능력이 향상**되었다는 것을 의미함


**[NER]**    
* transformer models을 **named entity recognition(NER)** 작업에 적용하여 비정형 텍스트에서 **재료 화학과 관련**된 **중요한 과학 개체를 추출하고 레이블을 지정**한다.
* 본 연구에서, 우리는 **3개의 다른 재료 과학 데이터 세트**에 **4개의 다른 NER 모델**을 적용하고 성능을 분석한다.


------

# Datasets
Here we consider three different NER datasets, chosen to represent a diversity of text sources and problems relevant to materials science; a . Each of these is described in detail below. The solid-state dataset is , though  and annotated entities are available for the other two.

여기서 우리는 다양한 텍스트 소스와 재료 과학과 관련된 문제를 나타내기 위해 선택된 **세 가지 다른 NER 데이터 세트**를 사용.         
**1)** set of solid-state materials science abstracts with entities of broad interest (publicly available)      
**2)** set of abstracts with inorganic doping information (only the DOIs)     
**3)** set of methods/results sections relevant to gold nanoparticle synthesis (only the DOIs)     







## Solid-state dataset
The solid-state dataset은 solid-state materials publications의 800 annotated된 abstracts으로 구성되어있다.       
이 논문의 출처는 아래와 같다.       
- Elsevier’s Scopus/ScienceDirect         
- Springer-Nature APIs     
- web scraping for journals published by the Royal Society of Chemistry and the Electrochemical Society


**[수집 방법]**                
Abstracts은 적어도 하나의 inorganic 재료 & inorganic 재료에 synthesis or characterization을 적어도 한 번 언급하는 경우 관련이 있는 것으로 간주된다.         

**[entity types]**    
- inorganic materials (MAT)      
- symmetry/phase labels (SPL)      
- sample descriptors (DSC)       
- material properties (PRO)      
- material applications (APL)     
- synthesis methods (SMT)        
- characterization methods (CMT)       

[자세한 예 확인](https://doi.org/10.1021/acs.chemmater.0c02553)    
[해당 논문 확인](https://pubs.acs.org/doi/abs/10.1021/acs.jcim.9b00470)      

**[Figure 1. Solid-state annotation example]**        
<img width="248" alt="image" src="https://github.com/yerimoh/yerimoh.github.io/assets/76824611/204a63d0-c16c-427d-bf6a-ccb1bfb6ed4f">
- 이 데이터 세트는 Solid 물질의 특정 측면에 집중하지 않고 관련 정보를 "전체"로 제공하기 위한 것이다.       
- entities의 광범위한 정의로 인해 Solid 데이터 세트는 일반적으로 다른 데이터 세트보다 문단당 더 많은 entity를 포함함       
- inter-annotator agreement of 87.4%










------




## Doping dataset

반도체가 필요한 응용 프로그램에 사용되는 doped material의 특성은 아래와 같은  중요한 정보에 의해 결정된다.    
- base material (BASEMAT)    
- the doping agent (DOPANT)    
- doping density      
- charge carrier density (DOPMODQ)     

              

이 데이터 세트의 의도는 물질의 도핑 및 기타 관련 정량적 측정과 관련된 정보를 캡처하는 것임.          


**[수집 방법]**    
* doping에 대한 정보를 구체적으로 포함하는 abstracts를 재료 과학 추상화의 [Matscholar 데이터베이스](https://matscholar.com/)에서 쿼리했음.         
  - i.e., those containing regular expressions matching ‘‘dop*’’  (such as ‘‘dopant,’’ ‘‘doped,’’ and ‘‘codoping’’)      
  - ‘‘n-type’’          
  - ‘‘p-type’’      
* 500개의 abstracts set은 쿼리된 set에서 무작위로 샘플링되었으며, 이 집합에서 455개의 abstracts가 inorganic materials과 관련된 것으로 인간 주석자에 의해 식별됨(3명의 주석자)        



**[Figure 2. Doping annotation example]**       
<img width="252" alt="image" src="https://github.com/yerimoh/yerimoh.github.io/assets/76824611/82d2d5f3-1dc4-4295-821e-fbfdc1267d32">     
* solid-state 및 gold nanoparticle dataset와 달리 토큰에는 한 번에 한 문장씩 주석이 달렸다  (샘플 하나 = 한 문장).      
* 문장에는 solid-state materials의 doping에 대한 구체적이고 직접적인 정보가 포함되어 있을 때만 주석이 달렸음.
(예: 'X가 Y로 도핑되었다', 'X:Y', 'Y 도핑' 등)     


-----

## Gold nanoparticle dataset


금 나노 입자(Gold nanoparticles_AuNP)는 아래와 같은 분야에 널리 쓰인다.             
- Gold nanoparticles (AuNPs)       
- 생체 의학 biomedicine (e.g., 체외 진단 vitro diagnostics)     
- 반도체 기술 semiconductor technology     
- 화장품 cosmetics    
- 크기와 모양에 대한 AuNP 특성의 강한 의존에도 불구하고, synthesis methods는 최근에서야 AuNP morphology, 특히 anisotropic nanorods를 제어할 수 있었다.     

**[데이터 세트의 목표]**      
- 이 데이터 세트는 AuNP 합성 문헌의 전문의 관련 섹션에서 AuNP 형태론과 설명을 캡처하는 것을 목표로 한다.       


**[수집 방법]**     
- single annotator는 AuNP 합성에 대한 73개의 articles에서 85개의 characterization paragraphs에 주석을 달았다.     
<img width="295" alt="image" src="https://github.com/yerimoh/yerimoh.github.io/assets/76824611/3ee26bb0-6519-4004-a252-88166216a9b7">

**[Figure 3. Gold nanoparticle annotation example]**       
요약된 예는 그림 3에 나와 있습니다. 이 모델의 개체에는 명사 기반 형태적 개체(MOR) 및 형용사 기반 서술적 개체(DES)를 포함하여 합성된 AuNP에 대한 일반적인 형태 기반 형태학적 정보가 포함됩니다. "particle" 또는 "AuNP"와 같은 개체는 MOR 개체로 주석이 달렸으므로 많은 나노 입자 기사에서 입자를 덜 설명적인 "나노입자" 또는 "NP"로만 언급하기 때문에 적어도 일부 대상은 미래에 크기 정보를 속성으로 지정할 수 있습니다. 원본 데이터에서 이러한 레이블에 대한 지원 수준이 매우 낮기 때문에 입자의 치수와 같은 다른 측면이 포함되지 않았습니다. 이는 나노 물질 합성 문헌에서 정보 추출에 대한 과거 연구와 유사합니다. 또한 레이블의 수를 제한하면 특히 더 작은 데이터 세트에 대해 더 나은 성능을 제공하는 경향이 있습니다


A condensed example is shown in Figure 3. 79 The entities for this model include general shape-based morphological informa tion for the synthesized AuNPs, including noun-based morphological entities (MOR) and adjective-based, descriptive entities (DESs). Entities like ‘‘particle’’ or ‘‘AuNP’’ were annotated as MOR entities, so at least some target could be identified with which to attribute size information in the future since many nanoparticle articles only refer to the particles as the less descriptive ‘‘nanoparticle’’ or ‘‘NP.’’ Note that other aspects such as the dimensions of particles were not included due to very low levels of support for such labels in the original data. This is similar to past work on information extraction from nanomaterial synthesis literature.57 Furthermore, limiting the number of labels will tend to provide better performance, particularly for smaller datasets



[해당 논문 확인](https://www.sciencedirect.com/science/article/pii/S002554081400693X)

-----

