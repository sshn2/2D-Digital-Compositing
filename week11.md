# WEEK 11
## 3D Camera Tracking
3D 추적 도구는 수십 개의 가능한 동작 추적 지점을 자동으로 생성한 다음 사용자가 추적할 지점을 선택할 수 있도록 한다. 이렇게 하면 추적 지점을 설정하는 데 많은 수작업이 필요하지만 사용하려면 상당한 시간과 처리 능력이 필요하다.

### Camera Tracking
3D 모션 트랙 및 매치 무브의 소스 시퀀스를 분석하고 원본 카메라의 렌즈 및 모션 매개변수를 추출하여 샷을 촬영하는 데 사용된 카메라를 참조하여 2D 또는 3D 요소를 올바르게 합성하게 도와주는 트래커이다.

![image](https://user-images.githubusercontent.com/112941366/210297001-f02518b1-eb63-4f89-824e-a46e51a58e47.png)

2차원에 이미지에 3차원 오브제를 넣으려고 한다면 nuke x을 활용하면 된다. Add the Camera Tracker node. NukeX required

![image](https://user-images.githubusercontent.com/112941366/210297073-09fdbad5-d93d-4b2f-b77e-09ef6cd711b3.png)

트래커 설정
- Range : Global은 프로젝트 설정의 범위이다. 전체 범위를 추적하지 않으려면 사용자 정의를 선택하면 된다. 프레임이 많을수록 시간이 더 오래 걸리지만 더 많은 정보를 얻을 수 있기 때문에 종종 더 나은 결과를 제공한다.
- Lens Distortion: Unknown Lens를 선택하고 Undistort Input를 선택한다.
- Film Back Preset: 정확하게 설정하는 것이 중요하다. 자신이 실제로 사용한 카메라를 설정하면 더 정확한 결과를 볼 수 있다.

![image](https://user-images.githubusercontent.com/112941366/210297519-1887b9a8-eea7-4cf9-b52c-9071a9b717e1.png)

Detection Threshold: 너무 많은 기능이 사용되거나 다른 영역이 거의 이해되지 않는 경우, 값을 높이고 모니터링한다.

![image](https://user-images.githubusercontent.com/112941366/210297622-28d14845-4c5a-4542-b479-bc19edb6bb7f.png)
![image](https://user-images.githubusercontent.com/112941366/210297641-5fc39fef-5ae9-4a3e-8645-b0fdcbdfa904.png)
![image](https://user-images.githubusercontent.com/112941366/210297656-5f3cd560-7972-4e25-b73b-a55f1a4635ee.png)
![image](https://user-images.githubusercontent.com/112941366/210297680-0f361c1e-ff26-41e7-b730-f70ffef9d399.png)

녹색(좋음)
주황색(아마도)
빨간색(거부됨)

마우스를 올려 개별 트랙의 세부 정보를 확인할 수 있다.

![image](https://user-images.githubusercontent.com/112941366/210297734-7a73516b-8fb4-42cd-a12f-796062aaa710.png)

1 미만의 오류는 훌륭한 값이다. 1과 2 사이에서 계속해서 면밀히 테스트한다. 2 이상은 좋지 않다. 반드시 아래에 있는 해결 방법 개선 섹션을 방문해야 한다.

### 3D Scene

![image](https://user-images.githubusercontent.com/112941366/210297885-8d33fe42-6318-47f1-be47-b825c29a6a97.png)

모든 Nuke 3D 장면에 필요한 3개의 노드(Scene, ScanlineRender, Camera)로 기본 설정을 얻는다. PointCloud 및 LensDistortion 도 있다. Camera 및 LensDistortion는 CameraTracker 노드에 연결한다.

![image](https://user-images.githubusercontent.com/112941366/210298135-0d5450aa-684a-42b5-85ee-124d71dcf74a.png)

Scene 노드를 뷰어에 연결하고 자동으로 3D 보기로 전환해야 한다. 그렇지 않으면 TAB 키를 사용하여 View Selection을 전환하거나 길을 잃으면 카메라를 선택하고 뷰어에서 단축키 F를 누르면 된다.

- MMB(또는 Alt+LMB): 뷰어 관점 변환
- Wheel(또는 Alt+MMB): 뷰어 관점 확대
- Ctrl+LMB(또는 Alt+RMB): 뷰어 관점 회전

모든 Nuke 단축키 목록 > 3D 뷰어


---

### 출처

https://www.foundry.com/products/nuke/plug-ins/cameratracker

https://lesterbanks.com/2020/07/getting-started-with-3d-camera-tracking-in-nuke/

http://admvfx.com/vfx-course/match-move/camera-tracker-in-nuke/

https://mattepaint.com/academy/series/camera-tracking-advanced-projections-nuke/
