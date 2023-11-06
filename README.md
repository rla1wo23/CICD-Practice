# CI/CD 실습, STEP0:: AWS CodePipeline+GitHub를 통한 빌드 배포 자동화 실습! 개요

---

- 노션으로 보기 원본링크: [https://pitch-amaryllis-776.notion.site/CI-CD-STEP0-AWS-CodePipeline-GitHub-78012a2ad241428da5db1c7e41cf2f6a?pvs=4]

계기:인하대학교 클라우드 컴퓨팅 수업에서 DevOps 파트를 배웠고 실습으로 빌드배포 자동화 과정을!! 올려주셨다. 원래 3시간짜리 수업인데, 수업을 무려 3시간 반 이상 진행했다. 자동화에 관심이 많아서 시간가는 줄 모르고 따라갔다. 강의 내용이 좋아, 복습할 겸 이렇게 글을 올린다.

코드를 Github repository에 push하는 것으로 빌드 배포를 자동화하는 실습입니다. 실습을 따라오시다 보면, 기존에 웹사이트 배포 과정에서 있었던 인프라 세팅, 빌드 과정등이 정말 많이 생략된 것을 볼 수 있을겁니다. 간단한 웹사이트의 서버와 클라이언트를 구현하고, 각각 Github레포지토리에 push할 때 마다 빌드-배포가 자동으로 생성됩니다. 아래 사진은 이 웹사이트의 아키텍처를 설명한 것인데요, 그림을 한 번 읽어보시면 어떤 구조인지 대충 이해가 되실겁니다.
<img src="src/Untitled.png" />

**목표**:

1. 클라이언트 측: Github 레포지토리에 push하는 것이 trigger로 작동하여, 코드파이프라인을 작동시키고 클라이언트는 그것의 빌드를 자동화해줍니다. 배포는 S3에 업로드하는 것으로 충분합니다.
2. 서버 측: Github push가 trigger인것은 같고, Github action이 빌드 과정을 자동화하고, 그것을 AWS CodeDeploy로 넘기면, 그것의 배포는 자동화되며, EC2에서 배포됩니다.

이 실습을 해보니까, 서버에 접속하고 빌드하는 과정이 자동화되어 생산성이 정말 많이 올라간다는 것을 느낄 수 있었습니다. 더구나, Github이랑 통합되는 것이 브랜치를 따로 관리하지않고 버전관리를 쉽게 해준다는 생각도 드네요.

이 게시물은 인하대학교 클라우드 컴퓨팅 강의에서, 코드스테이츠 김은아, 이정훈 강사님으로부터 자료를 받아 실습을 그대로 진행한 것임을 밝힙니다.

### Step0:소스코드 가져오기

---

- **먼저 Client 소스코드부터 가져와 볼겁니다.**

1. GItHub에 로그인하고, 아래 링크에서 레포지토리를 fork합니다.

   [https://github.com/rla1wo23/client-univ](https://github.com/rla1wo23/client-univ)

   <img src="src/Untitled 1.png" />

2. fork가 잘 이뤄졌다면, 이제 이 레포지토리를 clone해봅시다.
   <img src="src/Untitled 2.png" />
   <img src="src/Untitled 3.png" />

   우선, Client폴더랑 Server폴더를 각각 만들어주세요

   <img src="src/Untitled 4.png" />

- **이제 Server 소스코드도 가져와 봅시다.**

1. 아래 레포지토리도 똑같이 fork해줍시다.

   [https://github.com/rla1wo23/server-univ](https://github.com/rla1wo23/server-univ)

2. 얘도 같은 방식으로 Clone해줍시다. 단, 이번에는 Server 폴더에 Clone해야합니다.

   <img src="src/Untitled 5.png" />

여기까지 성공하셨다면 실습을 위한 소스파일이 준비 된 것입니다. 다음 STEP에서 뵙겠습니다.
