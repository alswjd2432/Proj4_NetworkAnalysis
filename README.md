# 네트워크 분석 자금세탁/금융사기 의심거래 탐지 모델 개발
## 목표 1. 네트워크 분석을 통한 시각화 및 패턴 발굴
## 목표 2. 이상금융거래 탐지 모델 개발

### 데이터 : 기업은행 내부 당행 거래 데이터(비공개)
사기계좌 약 14000개와 정상계좌 약 16000개를 시드계좌로 한 depth2 까지의 거래 내역 데이터
- data01 : 시드 계좌의 계좌 정보
<img width="1318" alt="image" src="https://github.com/alswjd2432/Proj4_NetworkAnalysis/assets/95081711/2b36bf0f-72ee-42bf-b244-0534bf73b123">
- data02 : 시드 계좌의 거래 내역 정보
<img width="1349" alt="image" src="https://github.com/alswjd2432/Proj4_NetworkAnalysis/assets/95081711/656d8f34-2ecf-473e-a3d2-9d1a90bbd270">
- data03 : 시드 계좌와 거래한 기업은행 계좌 정보 (data 형식은 data01과 동일)
  <br>
- data04 : data03에 등장하는 계좌의 거래 내역 정보 (data 형식은 data02와 동일)

### 주요 패키지 : NetworkX, DGL, Pytorch

### 패턴 발굴
1. 가설 수립 및 검증
- 사기 계좌가 정상 계좌보다 입금 거래 비율이 높다.
  <br>
: 정상 계좌의 경우, 일반적으로 소비의 성향이 강해서 출금의 비율이 비교적 높았으나, 사기 계좌는 집금 계좌의 존재 등의 이유로 다른 양상을 보였다.
<img width="830" alt="image" src="https://github.com/alswjd2432/Proj4_NetworkAnalysis/assets/95081711/7c4baf04-6b92-4001-aeb8-3592c6789443">

- 사기 계좌는 현금 입금 거래가 비교적 많았다.
<img width="850" alt="image" src="https://github.com/alswjd2432/Proj4_NetworkAnalysis/assets/95081711/bbf9d186-9f4f-425e-96f5-e443251cc5a9">

- 사기 계좌의 거래 지속 기간이 정상 계좌보다 짧다.
  <br>
  : 정상 계좌의 경우, 공과금, 급여 등 한 계좌와 주기적으로 거래하는 비율이 높아 거래 지속 기간이 길었으나, 사기 계좌의 경우 같은 인물이어도 여러 계좌를 이용하는 등 사기 특성상 한 계좌와 오래 거래를 지속하는 경우가 적었다.
<img width="702" alt="image" src="https://github.com/alswjd2432/Proj4_NetworkAnalysis/assets/95081711/628f06ac-3473-4652-93be-29751d2e6d54">

- (영어 적요 거래 내역 수/ 거래 지속 기간)이 큰 값으로 등장한 개인이나 개인사업자의 경우, 사기일 확률이 높았다.
- (영어 적요 거래 내역 수/ (거래 지속 기간 * 총 거래 건수) 가 0.01보다 높은 경우, 사기일 확률이 높았다.
<img width="260" alt="image" src="https://github.com/alswjd2432/Proj4_NetworkAnalysis/assets/95081711/49ab1773-134b-4c64-92bd-aa1588c9a9d9">

### 네트워크 시각화
: networkX를 활용해 거래 내역 데이터에 맞게 시계열 변수, 거래 금액을 모두 효과적으로 시각화
<img width="843" alt="image" src="https://github.com/alswjd2432/Proj4_NetworkAnalysis/assets/95081711/8d11ca8f-8184-4ccc-892a-fb90a9e1da8a">
: 노드 색깔로 계좌의 특성을 표시, 엣지 색깔에 시계열 변수 포함, 엣지 두께에 거래 금액을 시각화
<br>
- 예시 네트워크
<img width="831" alt="image" src="https://github.com/alswjd2432/Proj4_NetworkAnalysis/assets/95081711/fe31dcae-15f5-419d-9068-ee84345c632e">

### 사기 의심 계좌 탐지 모델 개발
: GNN 기반의 EdgeGATConv 그래프 분류 사용
<img width="777" alt="image" src="https://github.com/alswjd2432/Proj4_NetworkAnalysis/assets/95081711/684ba99a-66f5-49ef-89ad-570d9fdd03bd">
- 노드(계좌) 피처로 입금 수, 출금 수, 현금 계좌 여부, 총 거래 기간 사용
- 엣지(거래) 피처로 총 거래 금액, 총 거래 건수, 현금 거래 내역, 거래 지속 기간
- 시드 계좌 그래프에 사기(1), 정상(2)로 라벨링

#### 모델링 결과
- accuracy : 84%
- recall : 86%
- f1 score: 78%

### 결론
- 검증된 가설을 이용해 기존 룰 추가 혹은 보완 가능
- 탐지 모델을 이용해 기존 룰 기반 방식보다 짧은 시간 내에 효과적으로 의심 계좌 탐지 가능

##### 자세한 사항은 '네트워크 분석 기반 자금세탁/금융사기 의심거래 탐지 모델 개발.pdf' 확인
