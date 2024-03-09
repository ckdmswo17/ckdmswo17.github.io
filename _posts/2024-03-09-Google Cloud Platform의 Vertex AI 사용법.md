해당 글은 Google Cloud Platform의 Vertex AI의 classification 기능에 대한 간략한 사용법에 대해서 설명합니다. 동일한 내용을 Vertex AI 콘솔 안의 튜토리얼에서도 더 자세하게 확인 가능합니다.

Python을 이용해 데이터셋을 생성하는 방법은 설명하지 않습니다.

![vertexAI](https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/a1d412e4-7e6c-4267-a93f-d1ae7d7dd4e6)

[Vertex AI 사이트](https://console.cloud.google.com/vertex-ai?hl=ko&project=coastal-mesh-414403)

## 1. 무료로 체험 시작

Google Cloud Platform은 클라우드 사용량, gpu 사용량에 따라 요금을 부과하는 형식입니다.

하지만 Google Cloud에서는 체험을 위해 일정 크레딧을 무료로 제공합니다.

콘솔 상단에 파란 "무료로 체험하기" 버튼을 누르고 정보를 등록해야합니다.

<img width="633" alt="정보등록1" src="https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/016cc398-5d87-400f-98e0-13d830ed97bd">

![정보등록2](https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/f3fda072-f04d-4a98-90b5-c109c9e8992f)

해당 내용들은 모두 작성해주시고 계속하기 버튼을 누릅니다.

## 2. 데이터셋 등록

홈 화면에서 좌측 바의 "데이터 세트" 탭을 클릭하고 상단의 "만들기" 버튼을 클릭합니다.

![데이터셋만들기](https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/2ac2b7ae-86fb-4e7b-8016-d7e4952110dd)

다음으로는 데이터 유형을 선택합니다. 저는 채널코딩 데이터프레임 데이터셋을 분류하기위해 분류/회귀를 선택했습니다.

![데이터셋결정](https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/cdb17354-d512-4417-aa97-a47b681b2cc6)

다음으로 데이터셋 파일을 직접 업로드합니다. 사진 오른쪽의 요구사항을 고려해서 CSV 파일을 업로드하면 됩니다.

![데이터파일추가](https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/b4e828be-151f-4755-863d-1ac1d86a332a)

업로드하고 나면 데이터셋 등록이 완료되고, 우측의 "새 모델 학습 - 기타" 버튼을 클릭하면 바로 학습까지 진행할 수 있습니다.

## 3. 모델 학습

다른 다양한 옵션도 있지만 제가 설정한 방식으로 작성하겠습니다.

1. 학습 방법 : 커스텀 학습(고급) 선택
2. 모델 세부정보 : Target column 설정, 밑의 고급 옵션 열어서 데이터 분할을 수동으로 선택(자동 방식은 클래스 별 비율을 못 맞춰줘서 수동으로 선정. 수동으로 하려면 CSV 파일에 데이터 분할 열을 선정해야합니다. 열 생성 가이드는 아래 이미지를 참고하시면 됩니다.)
3. 피처스토어 조인(선택사항) : 건들지 X
4. 학습 옵션 : 직접 학습에 쓰일 열 선정, 가중치 열 선정 X, 최적화 목표는 로그 손실
5. 컴퓨팅 및 가격 책정 : 예산 1시간, 조기 중단 사용 설정 체크

<img width="471" alt="수동분할가이드" src="https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/a8d4099d-ad50-4970-a4c1-0aed7fbdc9f0">

<img width="612" alt="훈련설정" src="https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/147eb9ad-17bd-4c8e-acfe-87262279b6f9">

모든 설정을 끝내면 학습 파이프라인이 생성이 되고, 2시간 정도 기다리시면 학습이 완료가 됩니다.

<img width="283" alt="학습파이프라인" src="https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/0acdbbb3-6fda-4570-b11b-a1e55906e6fb">

학습이 완료되고 파이프라인을 클릭하면 라벨별 정확도, 혼동행렬, 특성 중요도 등 다양한 정보를 확인가능합니다.

![학습완료](https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/8a57e278-6b3c-4823-a862-f736cdf49698)

## 4. 일괄 예측

테스트 CSV 파일 x 데이터셋이 존재한다면 일괄 예측 기능을 이용해서 y를 예측 할 수 있습니다.

예측 결과 파일은 사용자 당 할당된 구글 클라우드 안에 CSV 파일로 저장됩니다.

<img width="526" alt="일괄예측" src="https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/f2648c1e-f2b5-4971-8a36-ea7f9aca2acf">

## 5. 온라인 예측 & 모델 다운로드

홈페이지에서 바로 예측과 모델을 로컬에 다운로드 받으려면 엔드포인트 배포를 먼저 진행해야합니다.
배포 및 테스트 탭에서 "엔드포인트 배포" 버튼을 클릭한 후 학습 설정때 했던 것 처럼 엔드포인트 이름과 학습 데이터와 타겟 열만 설정해주면 됩니다.

![배포및테스트](https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/c70b1069-5856-4bfc-a27b-e9c4b3c37dfd)

바로 특성 값 넣어서 타겟을 예측 가능

<img width="526" alt="일괄예측" src="https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/f2648c1e-f2b5-4971-8a36-ea7f9aca2acf">

모델 파일을 해당 명령어를 사용해서 로컬로 다운로드까지 가능.

하지만, 암호화되어있는 pb 파일이라 그런지, neutron이나 파이썬 saved_model_cli 커맨드를 사용해도 자세한 구조는 확인이 불가능했음. 방법 아시는 분들은 댓글이나 메일 좀 보내주세요..ㅎ

![모델내보내기](https://github.com/ckdmswo17/ckdmswo17.github.io/assets/71180737/84fc54e2-6dd5-48b6-99cf-515c54f6056c)
