# C-AIB-Boxoffice
박스오피스 매출 예상

# 박스오피스 매출 예상 서비스

---

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3a71ad0f-8f69-479d-8658-be9a56c80d8c/Untitled.png)

1. **상영 중인 영화** 확인. → 어제 박스오피스 순위로 확인. *(매 자정 정보 업데이트)*
2. 상영 중인 영화 중 매출 예상을 해보고 싶은 **영화 고르기**.
3. 예측 모델에 넣어 **예측 결과 송출**.

→ 원하는 영화의 '오늘 매출'을 예측하는 서비스 모델.

## 전체적인 파이프라인

---

![flow.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4b6a5eac-78c3-4257-b57c-04935607a472/flow.png)

1. **사용한 데이터 세트**
    
    영화진흥위원회에서 제공하는 OPEN API 사용.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/316daede-aaa9-4c77-ac1b-b21a3d22ea26/Untitled.png)
    
    - **박스오피스 정보**
        
        [일별 박스오피스 제공 정보](https://www.notion.so/babc1ae9c0cd46f69f625c9fe4268960)
        
    - **영화 정보**
        
        [영화 목록](https://www.notion.so/7a1bc8bff9274c6fa215c474b5428ee3)
        
2. **데이터베이스 Sqlite**

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/887b303d-d5b3-4fc1-9082-992940a91435/Untitled.png)

- movieinfo = 영화 목록에서 가져온 정보
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d9c0769e-9dc7-40b9-9fb5-a1f8ec8c5bdf/Untitled.png)
    
- moviesales = 일별 박스오피스 정보 (개봉일부터 어제 정보까지 모두 저장)
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/01f846cf-2db0-4ed7-b34b-40b2095918a6/Untitled.png)
    
- movieinfo의 movieCd 속성과 moviesales의 movieCd 속성으로 외래키 참조 가능

1. **개발환경 Colab**
2. **flask - HTML CSS** ([https://colorlib.com/wp/template/css-table-16/](https://colorlib.com/wp/template/css-table-16/))

# 간단한 시연

# 데이터 분석 - 대시보드

1. **일일 매출액**

![1.PNG](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d65aa185-c554-46e2-bd61-cf6db91722b4/1.png)

박스오피스 순위 (발표 자료 작성 기준 10월 11일) 일일 매출액.

1. **누적 매출액**

![2.PNG](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5861ee56-5bc6-4c65-9cd4-e14b73d0bddc/2.png)

- 7월 28일 개봉한 모가디슈는 10월 11일까지 스크린 독과점 상태
- 한국 영화의 스크린 독점율이 높지만, 외국 상업 영화(샹치, 007)도 무시할 수 없음
- 이외 애니메이션 영화는 좌석 점유율과 스크린 독점율도 낮은 까닭에 매출액이 적음

1. **전일대비 매출액 증감**

![3.PNG](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/678d69f0-d40b-46a4-aae6-f1faa270ddef/3.png)

- 평일 대비 주말 매출이 높은 까닭에 모두 증가한 상태.

# 마무리

---

1. 실시간 데이터베이스 연동.
    1. 현재 방식은 정보를 데이터베이스에 실행 전, 저장하는 수동 작업으로 진행 중.
2. 모델링 구현 시 ARIMA 모델 사용 중.
    1. 파라미터 값 지정 형식을 익히지 않은 까닭에 예측값이 굉장히 심한 편차.
    2. (모델 학습이 아닌) 특성을 넣지 않고도 예측할 수 있는 적합한 모델 찾기.
3. 순위권에 든 다른 영화와의 영향을 고려한 모델을 제작한다면 예측율이 높아질 거라 예상.
4. 현재 윈도우에서 ARIMA 모델 사용 시 에러를 일으키는 이슈.
    1. Colab으로 진행하였으나 번거로움 있음.
