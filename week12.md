# WEEK 12
## 3D object compositing
Nuke 의 3D 작업 공간을 사용하면 카메라 이동, 세트 교체 및 '실제' 차원 환경을 시뮬레이션해야 하는 기타 응용 프로그램을 위한 3D 합성물을 설정할 수 있다.

![image](https://user-images.githubusercontent.com/112941366/210299493-cd357561-90cd-4fd1-9687-72537018eb87.png)

3D 작업 영역에는 많은 잠재적 용도가 있지만 적어도 처음에는 팬 및 타일 장면을 만드는 데 사용할 가능성이 가장 높다. 2D 이미지 평면이 곡선 모양으로 정렬된 다음 애니메이션 카메라를 통해 렌더링되어 매끄러운 환경의 환상을 제공하는 장면이다.

![image](https://user-images.githubusercontent.com/112941366/210300722-6f2f8207-356a-46a6-bffc-106ab6cf1ed1.png)

Nuke의 3D 개체는 2D 작업을 수행하는 개체와 구별하기 위해 둥근 모양으로 나타난다. 위와 같이 노드 트리에서 2D 및 3D 개체를 함께 혼합할 수 있다. 예를 들어 2D 클립으로 3D 개체를 질감 처리하거나 3D 장면에서 렌더링된 출력을 가져와 2D 배경으로 사용할 수 있다.

3d object의 합성 전 unpremult(이미지의 외곽을 늘려 랜더링) > (color grade, color correct 등 색 보정) > premult를 해주어야 오브젝트의 배경에 자연스럽게 붙는다.
이미지 외곽에 생기는 검은색 윤곽을 color grading을 통하여 값을 맞춰준 뒤, premult를 해야 깨끗하게 오브젝트가 배경과 붙는다.

## Projection Cameras
카메라 프로젝션이라는 기술은 2D 매트 페인팅을 3D 장면(2.5D 기술)으로 변환하여 카메라 움직임을 통해 깊이 효과를 재현할 수 있다. 카메라 프로젝션을 사용하면 세트에서 전체 장면을 구성하거나 장면을 3D로 다시 만들지 않고도 매트 페인팅을 사용하여 사실적인 결과를 얻을 수 있다. 먼저 그림의 레이어를 분리하고 Nuke 내부에 대략적인 형상을 만들어 양식과 일치시키거나 다른 레이어 섹션을 만든 다음 해당 양식에 텍스처를 투사하여 깊이 효과를 얻기 위해 카메라 시차 이동을 사용하여 깊이를 부여한다.
카메라는 3D 장면을 보고 렌더링하는 것 외에도 2D 스틸 이미지 또는 이미지 시퀀스를 장면의 지오메트리로 투사할 수 있다. 이것은 실제 사진에서 사용되는 전면 투사 시스템과 유사하며 배경 이미지 또는 기타 요소가 무대에 투사되어 다른 요소와 함께 촬영된다.

Nuke에서 프로젝션 카메라는 원본 샷(또는 다른 샷)에서 추적된 카메라 데이터를 수신하여 다른 소스로 일치 이동되는 프로젝션을 설정할 수 있다.

이 설정에는 projection camera, Scene, Project3D, geometry object(투사할 대상) 및 투영하려는 이미지가 있는 2D 노드와 같은 노드가 필요하다.

<img width="1172" alt="스크린샷 2023-01-03 오후 1 44 31" src="https://user-images.githubusercontent.com/112941366/210301311-a312737d-7ea8-42e2-ae29-96a5998647c0.png">
<img width="1124" alt="스크린샷 2023-01-03 오후 1 46 00" src="https://user-images.githubusercontent.com/112941366/210301412-feac4786-657b-4154-a1bd-688ad55a45d1.png">

레이어가 나누어진 파일(psd)을 가져와서 shuffle 노드로 레이어를 다 쪼갠 다음, 이미지의 위치를 조정해준다. 그런 다음에 merge(plus)를 통해서 오브젝트들을 합성한다.


## Copycat Node
인공지능 훈련을 통해 로토스코핑을 수월하게 수행할 수 있다.
- 여러개의 프레임을 주고 Copycat에 넣어 교육하면 알아서 형태를 추출한다.
- 학습횟수가 많을수록 더 발전된 결과가 나온다.


---
### 출처

https://learn.foundry.com/nuke/11.1/content/comp_environment/3d_compositing/3d_compositing.html

https://www.youtube.com/watch?v=waHaU7J-i5o

https://learn.foundry.com/nuke/content/comp_environment/3d_compositing/projection_cameras.html

https://www.3dart.it/en/camera-projection-in-nuke/

