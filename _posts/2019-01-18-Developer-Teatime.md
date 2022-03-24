---
layout: post
title: '2019년 1월 18일 개발자 티타임'
author: hyegeun.cho
date: 2019-01-18 16:00 +0900
categories: [CULTURE]
tags: [TEATIME, LOCALDB]
image: /files/covers/dev-teatime-20190118.jpg
---

> "선데이토즈 개발자 티타임" 세 번째 시간입니다.
>
> 세 번째 티타임에는 안영훈님이 2018 시니어 개발자 과제였던 `로컬 DB R&D`에 대한 내용을 나누어 주셨습니다.

## [로컬 DB 리서치]

### 필요성

네트워크 비용이 비싸고 속도가 느린 글로벌 게임 서비스를 위해서 오프라인 모드를 위한 백그라운드 싱크, 암호화, 데이터 및 파일 접근 비용을 최소화한 기능이 필요함.

### 사례 분석

- [BGDatabase](http://www.bansheegz.com/BGDatabase/) Asset
    - 자세한 내용은 [이 문서](https://github.com/SundaytozDevelop/stz-tech-research/tree/master/LocalDB/BG-Database) 참조
    - 자체 제공하는 Editor 기능으로 데이터의 상태를 이해하기 쉬우나, 관련 코드가 DLL로 배포되어 있어서 수정 불가능
    - 자체 암호화 기능이 없고, 스키마 정의 등 DB 설정 파일의 제약
- [Realm](https://realm.io/docs/dotnet/latest/)
    - 자세한 내용은 [이 문서](https://github.com/SundaytozDevelop/stz-tech-research/tree/master/LocalDB/Realm) 참조
    - .NET Core 지원
    - Unity를 지원하지 않아 별도 개발 비용 발생
- [Firebase RealtimeDatabase](https://firebase.google.com/docs/database/unity/start?hl=ko)
    - 자세한 내용은 [이 문서](https://github.com/sundaytoz/stz-plugins-firebase-database) 참조
    - 오프라인 상태에서 수행되는 모든 트랜잭션이 대기열에 저장되었다가 온라인 상태가 될 때 데이터베이스에 적용
    - 앱을 재시작할 경우 트랜잭션이 유지되지 않아 별도로 트랜잭션을 저장했다가 앱 재시작 시 직접 실행해 줘야 함.
    - Cloud Firestore라는 베타 기능이 있음

### 결론

- 현존하는 로컬 DB 서비스들을 검토해봤으나 사용 편의성이 떨어짐
- 사내 프로젝트로 별도 구현할 예정

## [뒷 이야기]

- 게임 진입 속도가 중요하다. 네트워크 속도가 느린 글로벌의 경우 유저 진입 후 로딩을 견디지 못하고 이탈하는 경우가 빈번하게 발생한다. 리소스를 잘 나눠서 필요할 때만 백그라운드에서 Lazy loading 하도록 구현할 필요가 있다. 
- iOS의 경우 로딩이 진행되는 동안 유저에게 의미있는 인터랙션을 제공해야 한다. 따라서 위베베의 경우 로딩 시간동안 유저에게 인게임 경험을 제공하는 기능을 개발하고 있다.
- 글로벌 서비스 게임들의 경우 메인 어플리케이션 용량을 최대한도로 잡고 인게임 로딩을 줄여서 출시하는 경우도 있다. 글로벌에서는 큰 용량의 앱은 와이파이를 통해 다운로드 받는다는 생각이 일반적이라 그런 것 같다.


