# 🔍Introduction

![intro](https://user-images.githubusercontent.com/77667889/182480702-633a3948-adb6-4342-bb44-f4c8a9b393cf.png)

<br/>

#### 목적

- KNOW(한국직업정보) 설문 데이터셋을 활용한 직업 추천 알고리즘 개발
- 직업과 연관이 높은 설문지 문항 분석 및 영향변수 발굴

<br/>

#### 주최 / 주관

- 주최 : 한국고용정보원 / 주관 : 데이콘

<br/>

#### 리더보드

- Eval Metric : Macro F1-score
- Public Score : 전체 테스트 데이터 중 33% / Private Score : 전체 테스트 데이터 중 67%

<br/>

#### 최종 순위

🎖 3rd Prize

<br/>

# 🗂Data Set

![dataset](https://user-images.githubusercontent.com/77667889/182480759-a40c91ea-1d4b-47d6-9ba9-5e2ca740dab8.png)

- 전체 데이터셋 row 약 4만개, column 갯수 약 160개

<br/>

### Features

- Likert 5, 7점 척도 기반의 설문<br/>
![5point2](https://user-images.githubusercontent.com/77667889/182480782-71a01e41-ff9c-4030-9ed0-a7af2f98404e.png)

- 주관식 질문<br/>
![text2](https://user-images.githubusercontent.com/77667889/182480816-a612e87a-ee74-4267-aa50-30ef76f7b652.png)

<br/>

### Target

- 약 600개의 직업코드<br/>
![targets](https://user-images.githubusercontent.com/77667889/182480845-ed7f19d5-3efb-4c5a-a857-14a0026004db.png)

<br/>

# 💻Model

### Tabular Data

- 설문조사 데이터는 Categorical Data가 많은 정형데이터이기때문에
정형데이터 처리에 효과적인 Gradient Boosting 기반의 모델 중
Categorical Feauture Combinations과 One-hot Encoding을 지원하는 CatBoost를 사용

### Text Data

- 직업의 특성이 드러나는 주관식 답변들을 한 문장으로 만든 후 KoNLPy의 Mecab 형태소 Tokenizer를 사용
짧은 길이의 Keyword 중심 답변들이 많아 LSTM보다 1D-CNN 모델이 더 높은 성능을 보임

### HyperParameter Tuning

#### CatBoost

- loss_function을 MultiClass(1:1:1..1 예측)에서 MultiClassOneVsAll(1:다 예측)로 바꿔 train에 걸리는 시간을 1/7정도로 줄이고 F1-Score도 높임

### Ensemble

- CatBoost와 1D-CNN이 출력한 모든 클래스 별 확률값에 Min-Max Scaler를 적용시킨 후 Soft-Voting
![result](https://user-images.githubusercontent.com/77667889/182481051-c32b3034-b045-49f9-b4a0-f06d647db8e2.png)

<br/>

# 데이터 활용

### 취하자 - 직업 추천 웹사이트

https://github.com/juhwano/job_manager

### 뉴스 기사 분석

일자리 증가, 감소, 유지
