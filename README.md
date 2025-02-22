# 당신도 중고 거래왕이 될 수 있습니다!

## Table of Contents
  1. [Members](#Members)
  2. [Project Overview](#Project-Overview)
  3. [Getting Started](#Getting-Started)
  4. [Hardware](#Hardware)
  5. [Code Structure](#Code-Structure)
  6. [Detail](#Detail)

## Members

|                            김아경                            |                            김현욱                            |                            김황대                            |                            박상류                            |                            정재현                            |                            최윤성                            |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| [![Avatar](https://avatars.githubusercontent.com/u/70522267?v=4)](https://github.com/EP000) | [![Avatar](https://avatars.githubusercontent.com/u/31470457?v=4)](https://github.com/powerwook) | [![Avatar](https://avatars.githubusercontent.com/u/59689327?v=4)](https://github.com/kimhwangdae) | [![Avatar](https://avatars.githubusercontent.com/u/60460317?v=4)](https://github.com/psrpsj) | [![Avatar](https://avatars.githubusercontent.com/u/13325436?v=4)](https://github.com/JHyunJung) | [![Avatar](https://avatars.githubusercontent.com/u/80210706?v=4)](https://github.com/choi-yunsung) |
| [Github](https://github.com/EP000) | [Github](https://github.com/powerwook) | [Github](https://github.com/kimhwangdae) | [Github](https://github.com/psrpsj) | [Github](https://github.com/JHyunJung) | [Github](https://github.com/choi-yunsung) |


## Project Overview
  * 목표
    1. 멀티모달 분류모델을 활용하여 입력된 상품 이미지와 제목으로 카테고리 분류
    2. 생성/추출모델을 통해 상품 노출 빈도를 높일 수 있는 해시태그 생성
  * 모델
    1. EfficientNet-b0 와 BERT Classifier 모델을 이용한 카테고리 분류모델
    2. Elastic Search 와 TF-IDF를 이용한 HashTag 추출모델
    3. [skt/kogpt-base-v2](https://github.com/SKT-AI/KoGPT2)를 기반한 데이터 fine-tuned HashTag 생성모델
  * Data
    * 번개장터 crawling 데이터 (분야 : 전가기기)

  * Contributors
    * 김아경: 추출모델설계, Text 데이터 전처리
    * 김현욱: 이미지 데이터 전처리, 분류모델 검증
    * 김황대: 생성모델 설계, Streamlit 설계
    * 박상류: 생성모델 설계, Text 데이터 전처리
    * 정재현: 데이터 크롤링, Elastic Search 설계 및 구현
    * 최윤성: Project Manager, 분류모델 설계

## Getting Started
  * Install requirements
    ``` bash
      # requirement 설치
      cd code
      pip install -r requirements.txt 
    ```
## Hardware
The following specs were used to create the original solution.
- Ubuntu 18.04.5 LTS
- Intel(R) Xeon(R) Gold 5120 CPU @ 2.20GHz
- NVIDIA Tesla V100-SXM2-32GB

## Code Structure
```text
├── code/                   
│   ├── crawl
│   │   └── bunjang_crawl.py
│   │
│   ├── multimodal-clf
│   │   ├── configs
│   │   │   ├── data/secondhad-goods.yaml
│   │   │   └── model/mobilenetv3_kluebert.yaml
│   │   ├── src
│   │   │   ├── augmentation
│   │   │   │   ├── methods.py
│   │   │   │   ├── policies.py
│   │   │   │   └── transforms.py
│   │   │   ├── utils
│   │   │   │   ├── common.py
│   │   │   │   └── data.py
│   │   │   ├── dataloader.py
│   │   │   ├── model.py
│   │   │   └── traniner.py
│   │   └── train.py
│   │   
│   ├── prototype
│   │   ├── models/mmclf
│   │   │   ├── best.pt
│   │   │   ├── config.yaml
│   │   │   ├── mmclf.py
│   │   │   ├── special_tokens_map.json
│   │   │   ├── tokenizer_config.json
│   │   │   ├── tokenizer.json
│   │   │   └── vocab.txt
│   │   ├── app.py
│   │   └── inference.py
│   │   
│   ├── text_extraction
│   │   ├── es_api.py
│   │   ├── make_vocab.py
│   │   └── text_extraction.py
│   │
│   ├── text_generation
│   │   ├── arguments.py
│   │   ├── data.py
│   │   ├── hashtag_preprocess.py
│   │   ├── inference.py
│   │   ├── preprocess.py
│   │   └── train.py                  
│   │
│   ├── requirements.txt
│   └── README.md
│
└── data/es_data                     
    └── vocab_space_ver2.txt                        
    
```
## Detail
  * 멀티모달 분류모델을 활용하여 입력된 상품 이미지와 제목으로 카테고리 분류
    * 사용자가 제공한 이미지와 상품 제목을 각각 분류 후 Soft Voting을 통한 카테고리 분류
    ![classification](https://user-images.githubusercontent.com/60460317/146878954-899af65a-cf84-4a80-a4d8-66919c3cd4d6.png)
    
  * 생성/추출모델을 통해 상품 노출 빈도를 높일 수 있는 해시태그 생성
    * TF-IDF 빈도수 계산 및 Elastic Search를 이용한 본문 내 해시태그 추출
    * GPT-2를 기반으로 실제 약 10만개의 제목, 본문, 해시태그를 학습한 fine-tuned 모델을 이용한 해시태그 생성
    ![Hashtag](https://user-images.githubusercontent.com/60460317/146884272-25620910-08e0-4d08-bdb4-1b41c64a6cf3.png)
  
  * 시연영상: [YouTube](https://www.youtube.com/watch?v=bVwvSa7A3RA)
