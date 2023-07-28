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

1. 패턴 발굴
(1) 가설 수립 및 검증
- 사기 계좌가 정상 계좌보다 입금 거래 비율이 높다.
: 정상 계좌의 경우, 일반적으로 소비의 성향이 강해서 출금의 비율이 비교적 높았으나, 사기 계좌는 다른 양상을 보였다.









