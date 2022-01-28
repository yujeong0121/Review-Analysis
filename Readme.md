# 자연어 처리를 이용한 청소기 리뷰 평가지표 개발 및 감성분석


### 🔗 Link

**Source**

[NLP/code and data at main · yujeong0121/NLP](https://github.com/yujeong0121/NLP/tree/main/code%20and%20data)

**PPT**

[발표자료](https://github.com/yujeong0121/NLP/blob/main/%EC%82%BC%EC%82%BC%EC%98%A4%EC%98%A4_NLP%EB%A5%BC%20%EC%9D%B4%EC%9A%A9%ED%95%9C%20%EC%B2%AD%EC%86%8C%EA%B8%B0%20%EB%A6%AC%EB%B7%B0%20%EB%B6%84%EC%84%9D.pdf)

## ✍️ 요약
![요약](https://user-images.githubusercontent.com/94778140/151472716-8f70cbb2-8560-4097-9369-582900e2ac5c.png)


- Work Team & Member
    - 팀명: 삼삼오오
    - 팀원: 박유정, 김찬희, 정새하, 정한슬
    
- Work Schedule
    - 1월 8일 ~ 10일: 기획 및 데이터 크롤링
    - 1월 11일: 데이터 전처리
    - 1월 12일 : 데이터 전처리, 감성사전 제작 및 감성분석
    - 1월 13일: 점수화 및 시각화
    
- Skills
    - Python
    - Jupyter Lab
    - Github
    - Slack

- Dataset
    - 네이버 쇼핑에서 크롤링한 무선 청소기 리뷰 4000개 (제품 40개 선정, 제품마다 200개의 리뷰 수집)

## 📌 개요

- 문제정의
    
    제품을 구매할 때 여러 요소를 보며 비교하지만 실제 사용자의 리뷰를 읽어보며 정하는 경우가 많음
    이 때 많은 시간이 소모되는데  리뷰가 긍정인지 부정인지 판단하는 것 뿐만 아니라 구매결정에 필요한 다른 요소들도 파악하는데 마땅한 지표나 방법이 없음에 문제를 느낌
    
- 목표
    
    자연어 처리 기술(NLP)로 리뷰를 분석해서 가격 이외의 지표를 명확하게 제시해 소비자의 구매결정에 도움을 주고자 함
    

## 📋 분석 프로세스

1. 데이터 수집: 무선 청소기 리뷰 데이터
2. 데이터 전처리 
    - 문자 단위로 분리(kkma.sentences)
    - 특수문자 제거(re.sub)
    - 띄어쓰기 교정(pykospacing)
    - 맞춤법 교정(okt.normalize)
3. 감성사전 제작: 지표 설정, 점수 산정
4. 감성분석: 키워드 추출, 감성 찾기
5. 점수화: 단어 가중치를 도출해서 반영(CountVectorizer로 벡터화 한 값을 TF-IDF 로 변환해서 중요도를 구함)
6. 분석 결과 시각화:  불용어 제거, 단어 빈도수 워드클라우드, TOP5 제품 시각화

## 🛠 사용 라이브러리

- `selenium 4.1.0`
- `BeautifulSoup4 4.6.0`
- `pandas 1.3.5`
- `KoNLPy 0.5.2`
- `Pycospacing 0.5`
- `Scikits-learn 1.0.1`
- `Numpy 1.19.5`

## 🖥 역할

- 데이터 전처리
- 말뭉치 제작
- 감성사전 제작
- 불용어 제거
- 워드클라우드

## ✨ 결과

![result](https://user-images.githubusercontent.com/94778140/151472825-d6924d5a-3f32-45d6-89a5-247e6e9f9651.png)


![result2](https://user-images.githubusercontent.com/94778140/151472840-d6f22c69-2bd2-4aca-acf8-cf76af15f49c.png)


![result3](https://user-images.githubusercontent.com/94778140/151472854-876d1a14-5066-459c-acd0-2aae405632c6.png)


## 💡 성장한 부분

- 워드클라우드를 그려보는 과정에서 불용어 사전을 사용해도 의미 없는 단어들이 많이 추출되는 현상이 발생했습니다. 먼저 ‘것’, ‘집’ 과 같이 단어 길이가 1인 것은 명사 추출 과정에서 제외 시켰습니다. 추가로 ‘청소기’, ‘청소, ‘제품’, ‘사용’과 같이 청소기 리뷰에서 당연하게 자주 사용되어 중요도가 낮은 것들은 사전에 추가하여 제외되도록 개선했습니다. 그 결과 감성사전에서 지정했던 키워드들이 실제로 리뷰 내에서도 많이 언급되는 것을 확인할 수 있었고 지표를 작성할 때 반영할 수 있었습니다.

- 제가 담당했던 LG와 Tefal의 경우 ‘가성비’라는 키워드가 리뷰 내에서 LG는 추출되지 않았고 Tefal은 비교적 자주 등장했습니다. 고가로 형성되어있는 LG 청소기에서는 나오기 힘든 단어이기 때문이라고 생각됩니다. 전처리 과정이 길어져 팀원과 상의한 후 기존에 수집한 데이터 1만개에서 슬라이싱으로 데이터를 덜어내자고 결정을 하였습니다. ‘데이터가 줄어서 유의미한 인사이트를 얻을 수 있을까’하는 걱정이 있었는데 작은 데이터 속에서도 인사이트를 찾아낼 수 있다는 걸 알게 된 유익한 시간이었습니다.

- 자연어 처리를 하며 분석 과정마다 에러에 대한 고비가 많았습니다. 에러가 발생하면 구글링을 바로 하는 것이 아니라 해당 코드에 가서 값이 어떤 타입으로 들어오고 있는지, 어디까지는 정상적으로 작동하고 어디부터 에러가 나는지 확인하는 것이 우선이라는 것을 깨달았습니다. 에러를 마주쳤을 때 print를 루틴처럼 찍어보게 되는 계기가 되었습니다.
