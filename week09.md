## WEEK 09
## Color Correction

### Grade node

이 노드를 사용하여 한 이미지에서 다른 이미지로 색상을 일치시키고 색조 범위를 정의한다. 
Blackpoints 및 Withpoints를 사용하여 완벽한 검정색과 완벽한 흰색을 설정하면 이미지를 전체 동적 범위로 늘릴 수 있다.

![image](https://user-images.githubusercontent.com/112941366/210245642-0bffd47f-6e2f-4f97-ac47-94b2309ce44f.png)

색상 견본을 사용하여 블랙포인트를 샘플링하고 화이트 포인트 매개변수를 사용하여 이미지에서 가장 어두운 영역과 가장 밝은 영역을 설정한다. 뷰어에서 Cmd+Shift+드래그를 사용하여 영역을 샘플링한다.
|Grade|Function|
|:---:|:---:|
|blackpoint|이 값을 설정하여 black.0을 정의|
|whitepoint|흰색을 정의하려면 이 값을 설정(1)|
|lift|새 블랙포인트를 새 값으로 변경하려면|
|gain|새 화이트포인트를 새 값으로 변경하려면|
|multiply|-|
|offset (Add operation)|-|
|gamma|색상 보정에 사용|

mulyiply 값
- 곱하기 연산이기 때문에, (0값) 을 제외하곤 수치가 높아진다.
- 소수를 넣으면 낮아진다.
- 정수를 넣으면 높아진다.

![image](https://user-images.githubusercontent.com/112941366/210300093-ebfb2892-2b9e-4e3d-8664-427b3c8131e4.png)

블랙을 제외한 다른 부분의 밝기를 제어하기 때문에 기본 컬러 작업에 multiply 조절이 좋은 것 같다.

기본 밝기를 수정하기위해 exposure 노드를 사용하기도 한다.

exposure는 말 그대로 노출을 조절하는 노드인데, 사진 시스템 기반으로 노드를 조절할 수 있기 때문에 영상보다 사진에 익숙한 사람들은 오히려 grade node보다 기본 제어가 쉬울 수 있다. 누크는 동일한 기능도 이름이나 항목이 달라서, 처음 접하는 유저나 개념이해가 부족한 사람들은 grade node 사용이 어렵게 느껴질 수 있다.

whitepoint 연산은 나누기

<img width="609" alt="스크린샷 2023-01-03 오후 1 25 46" src="https://user-images.githubusercontent.com/112941366/210300008-1922025d-0e5f-4acb-8214-a05a46126647.png">

- 화이트 포인트의 연산은 정확히 나누기 연산이다.
- 어떤 수치도 1로 나누면 원본 값을 가진다.
- 어떤 수치도 0으로 나누면 값은 0을 가진다.

예를 들어 white point가 0.5라면, 0.5밝기부터 모두 1이상이 되어, 밝아진다.
white point가 2라면 , 모든 수치가 2배로 나눠지니, 1조차도 0.5로 변화시켜 어두워진다.

### ColorCorrect node (C)

Grade node를 사용하여 색상을 일치시킨 후, 이 노드를 사용하여 이미지에 모양과 느낌을 부여한다. 슬라이더를 사용하여 색상을 변경할 수 있다. 곡선 사용을 선호하는 경우, ColorLookup 노드를 사용할 수 있다.

![image](https://user-images.githubusercontent.com/112941366/210246824-b5dd864d-f60c-41cc-b92d-9d1f6666106c.png)
![image](https://user-images.githubusercontent.com/112941366/210246851-34534ea7-ee4a-4874-84e0-2fcec28b1d8a.png)

- 그림자, 하이라이트 또는 중간톤에 색상을 지정하려면 감마 슬라이더의 색상환 단추를 사용. 색상환에서 색조 슬라이더를 사용할 수 있다.
- 색을 칠하려면 Gain 속성의 컬러 휠을 사용.
- 색상환 창에서 TMI 슬라이더를 활성화하면 슬라이더를 사용할 수 있는데, T(온도) 슬라이더를 사용하여 이미지를 차갑게 또는 따뜻하게 보이게 할 수 있다. 색조를 수정하려면 M(마젠타) 슬라이더를 사용.


### ColorLookup node

곡선을 사용하여 색상을 변경한다.

![image](https://user-images.githubusercontent.com/112941366/210247118-4197d69a-824f-429c-8dcd-3685ad43ac67.png)

뷰어에서 보정을 위해 샘플링할 픽셀 위로 커서를 끌어올린다. ColorLookup 속성 패널에서 곡선을 클릭하는 동안 Ctrl+Alt(Mac의 경우 Cmd+Alt)를 눌러 빨간색, 녹색 및 파란색 선이 색상 곡선과 교차하는 위치에 점을 설정한다.

### HueCorrect node

Nuke의 HueCorrect 노드를 사용하면 다양한 색조의 채도 수준을 정밀하게 조정할 수 있다. HueCorrect는 녹색, 파란색 또는 빨간색 화면 번짐을 줄이는 데 가장 많이 사용된다.

![image](https://user-images.githubusercontent.com/112941366/210247373-1debfe60-bf56-4a04-8caf-8d605d31ad28.png)

- lum : 모든 채널에 영향을 주지만 광도 가중치가 적용(빨간색 채널은 효과의 약 30%, 녹색은 60%, 파란색은 10%).
- g_sup : 억제 기능을 적용하여 녹색 채널의 레벨을 줄인다. 녹색 곡선은 녹색 채널에 곡선 값을 직접 곱하는데 사용되는 반면 g_sup 곡선은 녹색 채널이 억제되는 양을 제어하는데 사용된다.

필요한 경우 뷰어 위로 커서를 끌어 수정하려는 이미지 부분을 나타내는 이미지 픽셀을 샘플링한다. 그런 다음 HueCorrect 속성 패널에서 곡선을 클릭하는 동안 Ctrl+Alt를 눌러 곡선에 특정 픽셀 값을 그린다. 이렇게 하면 편집할 곡선 부분을 볼 수 있다.


---

### 출처

http://defocusedeye.com/2014/01/color-nodes-grade-colorcorrect-colorlookup-hsvtool-huecorrect/

https://learn.foundry.com/nuke/content/reference_guide/color_nodes/grade.html

https://www.youtube.com/watch?v=owr48EDwVkc&list=PL46AC3F3C94F3E187&index=5

https://www.youtube.com/watch?v=EM1EeUCuY4k&list=PL46AC3F3C94F3E187






