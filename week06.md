# WEEK 06
## Rotoscoping
로코스토핑이란 샷에서 필요한 요소를 추출하기 위해 매트(일명 마스크)를 생성하는 프로세스이다. 또한 가비지 매트를 신속하게 생성하여 원하지 않는 요소를 제거하거나 완벽하지 않은 키잉(Keyer, Primatte, Keylight, IBK 등과 같은 도구에서)에서 간격을 차단하는 데 사용한다.
로토스코핑은 모든 주요 합성 소프트웨어(Nuke, After Effects, Flame, Fusion 등)와 Mocha 및 PFTrack과 같은 추적 소프트웨어에 적용할 수 있다.

![image](https://user-images.githubusercontent.com/112941366/210128569-e07e80c9-5b3a-47ef-a1c3-12bd7274f949.png)
누크에서는 로코스토핑 작업을 통해 alpha 채널을 분리하는 작업을 한다.

1. 로코스토핑 작업을 하기 전, 물체가 가지고 있는 모양이나 특징을 파악하는 것이 중요하다. 
2. 움직임이 비슷한 관절별로 나눠서 로토를 따주는 것이 좋다.
3. 포인트를 움직이기보다는 크기조절을 통해 모양을 맞춘다.
4. Ctrl - 대칭변형, Shift - 자유변형
5. 로토점을 드래그하면 드래그한 부분을 한번에 이동시킬 수 있다.

## Merge operation
로코스토핑 작업을 통해 분리한 alpha 채널을 다른 plate와 합치는 과정이다.
|Operation|Algorithm|Description|Illustration|
|:---:|:---:|---|:---:|
|atop|Ab+B(1-a)|A가 이미지가 겹치는 B를 덮고 있는 이미지 B의 모양을 보여준다.|![image](https://user-images.githubusercontent.com/112941366/210139741-d2a16ba5-905e-4a01-8e9d-5432d2f29c90.png)|
|average|(A+B)/2|두 이미지의 평균. 결과는 원본 이미지보다 어둡다.|![image](https://user-images.githubusercontent.com/112941366/210139774-7b70e6f3-bd91-41f6-91a4-eaee08156553.png)|
|color-burn|darken B towards A|이미지 B는 A의 휘도에 따라 어두워진다.|![image](https://user-images.githubusercontent.com/112941366/210139788-05df56b0-2d62-4571-9e73-7b4963878cb2.png)|
|color-dodge|brighten B towards A|이미지 B는 A의 휘도에 따라 더 밝아진다.|![image](https://user-images.githubusercontent.com/112941366/210139805-487aa22c-3717-4969-aedf-b80638baa8a9.png)|
|conjoint-over|A+B(1-a/b), A if a>b|픽셀이 A와 B 전부에 의해 부분적으로 가려진 경우 컨조인트 오버는 A가 B를 완전히 숨긴다고 가정한다.|![image](https://user-images.githubusercontent.com/112941366/210139870-99be46f1-5e69-403c-9c1d-3e012395c39d.png)|
|copy|A|이미지 A만 표시한다.|![image](https://user-images.githubusercontent.com/112941366/210139876-72037795-66d5-48d8-ac14-2127c72518bb.png)|
|difference|abs(A-B)|픽셀이 얼마나 다른지. Merge > Merges > Absminus 에서도 사용할 수 있다.|![image](https://user-images.githubusercontent.com/112941366/210139917-9ae1fa7c-4bc9-4da7-ac23-98eaf76b84bb.png)|
|disjoint-over|A+B(1-a)/b,A+B if a+b<1|픽셀이 a와 b 모두에 의해 부분적으로 가려지는 경우를 제외하면 오버 연산과 유사하다. 분리 오버는 두 개체가 겹치지 않는다고 가정한다.|![image](https://user-images.githubusercontent.com/112941366/210139924-9a8c75e2-2e69-4a21-b6cd-6e6ddd77e0d8.png)|
|divide|A/B, 0 if A<0 and B<0|값을 나누지만 두 개의 음수 값이 양수가 되는 것을 방지한다.|![image](https://user-images.githubusercontent.com/112941366/210139960-66a68997-bda6-40ea-8c5d-34a2e25145cc.png)|
|exclusion|A+B-2AB|보다 사진적인 형태의 차이.|![image](https://user-images.githubusercontent.com/112941366/210139987-4d4551dd-4e34-475b-89a2-bb7f11f2492f.png)|
|from|B-A|이미지 A는 B에서 뺀다.|![image](https://user-images.githubusercontent.com/112941366/210140010-cea4d282-3f67-48a5-b2aa-7c09e7a00ba2.png)|
|geometric|2AB/(A+B)|두 이미지를 평균화하는 또 다른 방법.|![image](https://user-images.githubusercontent.com/112941366/210140033-fb22f814-5865-4569-923f-395e503fa582.png)|
|hard-light|multiply if A<0.5, screen if A>0.5|이미지 B는 이미지 A 모양의 매우 밝고 선명한 빛으로 비춰진다.|![image](https://user-images.githubusercontent.com/112941366/210140059-82d4a64a-a598-4e3e-a3df-ac3c53818dad.png)|
|hypot|sqrt(A*A+B*B)|더하기 및 화면 조작과 유사. 결과는 플러스만큼 밝지는 않지만 화면보다 밝다.|![image](https://user-images.githubusercontent.com/112941366/210140064-333c9e04-3493-4875-82ef-8bd50b3ce141.png)|
|in|Ab|B의 알파와 겹치는 이미지 A의 영역만 표시한다. Merge > Merges > In 에서도 사용할 수 있다.|![image](https://user-images.githubusercontent.com/112941366/210140102-17b8a258-7335-43b5-aaf3-7460f522044d.png)|
|mask|Ba|A의 알파와 겹치는 이미지 B의 영역만 표시한다.|![image](https://user-images.githubusercontent.com/112941366/210140113-ecfcecf2-a377-4429-97ff-3fc81721d6bc.png)|
|matte|mAa+B(1-a)|이 작업에는 사전 곱셈되지 않은 이미지를 사용해야함. 병합 > 병합 > 매트에서도 사용할 수 있다.|![image](https://user-images.githubusercontent.com/112941366/210140148-76fd7394-2f05-40ec-b512-5bed3443177c.png)|
|max|max(A,B)|두 이미지의 최대값. Merge > Merges > Max 에서도 사용할 수 있다.|![image](https://user-images.githubusercontent.com/112941366/210140181-059f1c0f-e88b-45b8-acdd-3c212711529a.png)|
|min|min(A,B)|두 이미지의 최소값. Merge > Merges > Min 에서도 사용할 수 있다 .|![image](https://user-images.githubusercontent.com/112941366/210140199-f8defb12-3531-4233-bf81-28a982f3f5b1.png)|
|minus|A-B|이미지 B는 A에서 뺀다.|![image](https://user-images.githubusercontent.com/112941366/210140210-703d1e56-2ed7-48e8-bda9-2105e2c69663.png)|
|multiply|AB, A if A<0 and B<0|값을 곱하지만 두 개의 음수 값이 양수가 되는 것을 중지한다. 병합 > 병합 > 곱하기에서도 사용할 수 있다.|![image](https://user-images.githubusercontent.com/112941366/210140230-79300147-9e75-463e-8263-1ea224da711c.png)|
|out|A(1-b)|B의 알파와 겹치지 않는 이미지 A의 영역만 표시한다. Merge > Merges > Out 에서도 사용할 수 있다.|![image](https://user-images.githubusercontent.com/112941366/210140253-a1fe6b20-c08c-4351-b462-02d323b478fb.png)|
|over|A+B(1-a)|이미지 A의 알파에 따라 이미지 A를 B 위에 레이어한다.(가장 일반적)|![image](https://user-images.githubusercontent.com/112941366/210140272-e34d3776-4725-4806-aac8-257e40f6f578.png)|
|overlay|multiply if B<0.5,screen if B>0.5|이미지 A는 이미지 B를 밝게 한다.|![image](https://user-images.githubusercontent.com/112941366/210140283-a34aa14f-e0fc-4648-a667-f580fa87755d.png)|
|plus|A+B|이미지 A와 B의 합계. Merge > Merges > Plus 에서도 사용할 수 있다.|![image](https://user-images.githubusercontent.com/112941366/210140299-1d8eb83e-d1b9-4b3c-ac4d-d8bf5cc76f17.png)| 
|screen|A or B ≤1? A+B-AB: max(A,B)|A 또는 B가 1보다 작거나 같으면 화면은 Plus와 유사한 최대 예제를 사용한다. 병합 > 병합 > 화면 에서도 사용할 수 있다.|![image](https://user-images.githubusercontent.com/112941366/210140316-6d404202-723e-494a-b40c-8eaca4c72d29.png)|
|soft-light|B(2A+(B(1-AB))) if AB<1, 2AB otherwise|이미지 B가 켜진다. hard-light 작업만큼 극단적이지 않다.|![image](https://user-images.githubusercontent.com/112941366/210140329-bcf03aeb-1f59-4c8e-a9ae-d994b81a77ed.png)|
|stencil|B(1-a)|A의 알파와 겹치지 않는 이미지 B의 영역만 표시한다.|![image](https://user-images.githubusercontent.com/112941366/210140338-73e15f61-01b5-4ee9-aef5-0a597b641bea.png)|
|under|A(1-b)+B|이미지 B의 매트에 따라 A 위에 이미지 B를 레이어링한다.|![image](https://user-images.githubusercontent.com/112941366/210140349-cc6f7eae-76a2-4a2c-84bb-980162e8d035.png)|
|xor|A(1-b)+B(1-a)|이미지가 겹치지 않는 이미지 A와 B를 모두 표시한다.|![image](https://user-images.githubusercontent.com/112941366/210140353-9e9a6bc7-a4a7-4511-87c5-1f8d7cefc936.png)| 

---
### 출처
https://learn.foundry.com/nuke/content/comp_environment/merging/merge_operations.html


