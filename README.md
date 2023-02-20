# Kubernetes DevSecOps Toolchain Service

 프로젝트명 | 기술문서 | 발표자료 | Git Repository |프로젝트 기간 
:-------------: | :-------------: | :-------------: | :-------------: | :-------------:
 Kubernetes DevSecOps Toolchain Service | [Click](https://docs.google.com/document/d/1o6YaBrFl9ouEKxEBeTSaunQ44BkN39gFtcnx9rqwdEA/edit?usp=sharing) | [Click](https://docs.google.com/presentation/d/1GLuxI_fw9zpWJB_8srKz1OQcm_dco2Up/edit?usp=sharing&ouid=106249240240065525675&rtpof=true&sd=true) | [Click](https://github.com/onesenal/Innogrid_Project.git) | 23.01.01~23.02.27

## Contents:
  - [Intro](#Intro)
  - [Architecture](#Architecture)
  - [Organization](#Organization)
  - [Process](#Process)
  - [Documents](#Documents)
  - [Result](#Result)
  - [Feedback](#Feedback)

#### Intro
```sh
Kubernetes DevSecOps Toolchain Service란?
  사용자는 클릭 한 번만으로 보안 검사가 진행되고 개발환경을 구축해주는 시스템입니다. 
  사용자는 해당 시스템을 사용함으로써, 개발환경을 보다 빠르게 구성할 수 있고 보안상 결함과 취약성을 해소할 수 있습니다. 
  따라서 업무 프로세스의 효율을 높일 수 있습니다. 
```
#### Architecture
![](https://github.com/onesenal/Innogrid_Project/blob/main/Picture/Architecture02.png)

#### Organization
![](https://github.com/onesenal/Innogrid_Project/blob/main/Picture/Organization01.PNG)

#### Process
![](https://github.com/onesenal/Innogrid_Project/blob/main/Picture/Schedule.PNG)
기간 | 작업
:-------------: | :-------------:
1주차  | 주제 선정
2주차  | 1차 프로세스 및 단일 테스트
3주차  | 2차 프로세스 및 단일 테스트
4주차  | 3차 프로세스 및 단일 테스트
5주차  | 중간발표(1/31)
6주차  | 통합 테스트
7주차  | 통합 테스트
8주차  | 통합 테스트
9주차  | 최종발표(2/27)
  

#### Documents
유형 | 파일 | 파일내용
:-------------: | :-------------: | :-------------:
이미지  | [구성도](https://drive.google.com/file/d/1Ze-LKVUij8m3b0f4SDvuXyMrpzjQ6pEk/view?usp=share_link) | 서비스 전체 구성도
Google Docs  | [1차 프로세스](https://docs.google.com/document/d/1l7MFdAAyGkWllzth7KHZe4zCoICNr3sdzxfmMvZzhYo/edit?usp=share_link)  | 1차 프로세스 순서를 나타낸 문서입니다.
Google Docs  |  [2차 프로세스](https://docs.google.com/document/d/1xRl7jvD2D0YRw52dGKawLCe4UdmWvBEzkuReJnj1Ggs/edit?usp=sharing) | 2차 프로세스 순서를 나타낸 문서입니다.
Google Docs  | [3차 프로세스](https://docs.google.com/document/d/1cicCTDoU5wSGKNh2eQ3zqHwVIgsqgEEHqEGrbdELAQU/edit?usp=share_link) | 3차 프로세스 순서를 나타낸 문서입니다.
PowerPoint  | [중간발표자료](https://docs.google.com/presentation/d/1x4Q1G8w-2wpBMtshDAtTIDW0fHK6rAvB/edit?usp=sharing&ouid=106249240240065525675&rtpof=true&sd=true) | 중간발표 문서입니다.
Google Docs  | [시연영상]() | 프로젝트 시연영상 입니다.
Google Docs  | [기술문서](https://docs.google.com/document/d/1o6YaBrFl9ouEKxEBeTSaunQ44BkN39gFtcnx9rqwdEA/edit?usp=sharing) | 프로젝트 기술문서 입니다.
PowerPoint  | [최종발표자료](https://docs.google.com/presentation/d/1GLuxI_fw9zpWJB_8srKz1OQcm_dco2Up/edit?usp=sharing&ouid=106249240240065525675&rtpof=true&sd=true) | 최종발표 문서입니다.

#### Results
아래의 링크에서 결과물을 확인할 수 있습니다.
- [홈페이지](https://django.innogrid.duckdns.org)
- [모니터링](http://monitor.innogrid.duckdns.org)
- [로깅](http://logging.innogrid.duckdns.org)
- [발표영상]() | 2023.02.27 업데이트 예정

#### Feedback
번호 | 유형 | 문제 | 추후 과제
:----: | :------: | :-------------: | :-------------:
1 | 개발 | 배포된 애플리케이션 수정 불가 | Kubernetes API 활용하여 기능 추가
2 | 개발 | 웹 UI/UX 미흡 | 제공하는 페이지에서 세부적인 로그 또는 보안 검사 결과를 보여주는 기능 추가
3 | 보안 | Anchore 로그인 | Helm으로 Anchore 설치시 로그인이 안되는 문제가 발생하여 docker-compose로 설치하였으나 K8s환경에서 docker 연동이 되지 않아 DB를 각각 따로 사용한 부분 추후 해결 과제 
