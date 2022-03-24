---
layout: post
title: '디즈니팝을 만든 기술 1'
author: jungmin.park
date: 2019-07-21 10:00 +0900
categories: [TECH]
tags: [TECH]
image: /files/covers/disneypop-worldmap.jpg
---

> 디즈니팝은 선데이토즈에서 가장 최근에 출시한 게임입니다. 그런만큼 새로운 기술들이 많이 사용되었습니다.
>
> 플레이어와 상호작용하며 살아 숨쉬는 거대한 월드맵을 구현하기 위해 특히 최적화에 방점을 둔 여러 테크닉들이 사용되었는데요.
>
> 어떻게 월드맵을 최적화 시켰는지 알아보도록 하겠습니다.

# Sprite Shape

Sprite Shape는 유니티에서 제공하는 프리뷰 패키지로 Package Manager를 통해 설치하여 사용해볼 수 있습니다. 

유니티 블로그에서는 Sprite Shape에 대해 다음과 같이 소개하고 있습니다.

> Sprite Shape는 2D 환경을 유니티 에디터에서 직접 생성하고 꾸밀 수 있는 다양한 기능을 시각적, 직관적으로 제공합니다. 
> Sprite Shape를 통해 이미지를 곡선을 따라 동적으로 타일링하여 배치할 수 있습니다. 동적으로 배치된 이미지에 중돌체를 설정하거나 스크립트로 기능을 추가할 수도 있습니다.

Sprite Shape를 사용하면 작은 이미지를 타일링하여 큰 오브젝트를 생성할 수 있습니다. 조그만 이미지만으로 넓은 도로를 깔 수 있다는 것이죠.

![01](/files/images/2019-07-21-DisneyPop-Worldmap/01.png)

뿐만 아니라 타일링 방향을 곡선으로 바꾸거나 개발자가 지정한 모양대로 이미지를 타일링할 수도 있고, 내부를 채울 수도 있으며, 생성한 모양대로 충돌체를 설정할 수도 있습니다.

![02](/files/images/2019-07-21-DisneyPop-Worldmap/02.png)

이렇게 Sprite Shape를 사용하면 작은 이미지만으로 큰 오브젝트를 생성할 수 있기 때문에 텍스쳐를 절약할 수 있다는 장점이 있습니다. 

다만 Sprite Shape를 사용한 오브젝트에 대해 배칭이 적용되지 않고 너무 작은 이미지를 사용하여 오브젝트를 생성할 경우, 버텍스 수가 늘어나 도리어 성능을 저하시킬 수도 있습니다.

### 참고자료

- [Sprite Shape 문서](https://docs.unity3d.com/Packages/com.unity.2d.spriteshape@1.0/manual/index.html)
- [Sprite Shape 소개 블로그](https://blogs.unity3d.com/kr/2018/09/20/intro-to-2d-world-building-with-sprite-shape/)

# Sprite Sharp - Mesh Optimizer

Sprite Sharp는 에셋 스토어에서 유료로 판매되고 있는 플러그인입니다. 사용해보려면 13달러를 사용해 구매해야 하죠.

Sprite Sharp는 스프라이트의 메쉬를 최적화하여 2D씬에서의 폴리곤 수와 드로우 콜 수를 줄여 스프라이트 출력 비용을 줄여줍니다.

![03](/files/images/2019-07-21-DisneyPop-Worldmap/03.png)

특히 Sprite Sharp를 유니티의 Sprite Atlas와 함께 사용하여 좀 더 치밀하게 스프라이트를 Packing할 수 있습니다.

![04](/files/images/2019-07-21-DisneyPop-Worldmap/04.png)

다만 메쉬 제작 알고리즘이 외부툴이자 역시나 유료 툴인 Texture Packer 와 비교했을 때 비효율적이며, Json 파일이 자주 변경되어 버전 컨트롤 시스템에서 충돌 또는 롤백이 자주 발생하는 단점이 있습니다.

### 참고자료

- [Sprite Sharp](https://assetstore.unity.com/packages/tools/sprite-management/spritesharp-mesh-optimizer-37599)

# SpritePMA

디즈니팝 월드맵 상의 오브젝트들은 플레이어와 상호작용하며 다채롭게 움직입니다. 이런 애니메이션은 게임에 생명력을 불어넣지만 로딩 시간을 늘이는 주범이기도 하죠. 

그래서 디즈니팝에선 월드맵을 로딩할 때 텍스쳐만 우선 로딩해서 출력하는 기법을 사용하고 있습니다.

한 장짜리 이미지로 구성된 텍스쳐 오브젝트와 연출이 구현된 애니메이션 오브젝트를 별도로 관리함으로써 평소에는 이미지로만 월드맵을 그리다가 연출이 필요할 때 애니메이션 프리팹으로 교체하여 재생하는 것 입니다.

![05](/files/images/2019-07-21-DisneyPop-Worldmap/05.png)

텍스쳐 오브젝트는 애니메이션 오브젝트에서 RenderTexture로 스크린샷을 찍어서 생성하고 있습니다. 그런데 스크린샷을 찍는 과정에서 백그라운드 컬러가 외곽선으로 잔류하는 현상이 발생하였습니다.

이 외곽선을 제거하기 위해 PMA 쉐이더를 사용했습니다.

![06](/files/images/2019-07-21-DisneyPop-Worldmap/06.png)

추가로 SpritePMA를 사용하면 색상을 블렌드할 때 가산 혼합 방식을 사용할 수 있다는 장점이 있습니다.

유니티에서 스프라이트에 색상을 적용하는 방법은 기본적으로 Multiply 방식입니다. 따라서 색상을 블렌드하면 할 수록 점점 스프라이트의 색상이 어두워집니다.

SpritePMA에서는 0.5 이상의 컬러값이 적용될 경우 Additive 방식으로 색상이 적용됩니다.

![07](/files/images/2019-07-21-DisneyPop-Worldmap/07.png)

그래서 디자이너들이 원하는 색상을 더 다채롭게 적용할 수 있게 되었습니다.

# World Space Tiling

바닥 타일을 출력할 때 `Unlit/Transpaernt`에 기본 매터리얼 `Tiling`을 사용할 경우 대각선으로 타일을 배치할 수 없는 문제점이 있었습니다.

또한 여러 Quad를 매치할 경우 서로 간의 타일 모양을 맞추는 것이 쉽지 않았습니다. 

그래서 이미지를 World Space로 그려주는 쉐이더를 추가하여 해당 이슈를 해결했습니다.

![08](/files/images/2019-07-21-DisneyPop-Worldmap/08.png)

이렇게 작은 이미지를 대각선으로 그릴 수 있게 되면서 버텍스 수도 줄이고, 텍스쳐 크기도 줄일 수 있었습니다.

---

여기까지 디즈니팝 월드맵을 구현할 때 사용된 기술들에 대해 알아봤습니다. 
이미지를 최적화하는데 유용한 팁인 만큼 각자의 프로젝트에 한번씩 활용해보는 건 어떨까요?



