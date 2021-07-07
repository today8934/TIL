# invliad source release 에러 해결

Spring Boot 프로젝트 생성하여 서버 기동 시 다음과 같은 에러가 발생하였다.

> Error:java: invalid source release: 11

Spring Boot에서 프로젝트를 생성할 때 설정한 자바 버전(11)과 프로젝트의 자바 컴파일러 설정 부분이 충돌한 것 같음.

1. IntelliJ에서 **File → Project Structure → Project Settings → Project** 메뉴의 **Project Language** Level을 수정한다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbVL7lv%2FbtqBW1Ck2qM%2FhHlRFwmVPAAgvQ9mgiCzK1%2Fimg.png">

해결되지않았다...

2. **File → Project Structure → Project Settings → Modules**의 **Source Language Level**을 수정한다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdyfqXP%2FbtqBYegE1K7%2F3zKZPwn2CRGXKcFKzhvKXk%2Fimg.png">

역시 해결되지 않음.

3. **Preference → Build, Execution, Deployment → Compiler → Java Compiler**의 **Target bytescode version**을 수정해준다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbbePSA%2FbtqBWZ5AdhG%2FBnhUCMSXAMmWFx5tyQ9MF0%2Fimg.png">

이걸로 해결됨..

근데 **./gradlew build** 할때 또 똑같은 에러가 났다.

아마 내 맥북에 기존에 설치되어 있던 자바 버전이 10이라 그런듯..

macOS의 자바 환경변수를 변경해주었다.

우선 /Library/Java/JavaVirtualMachines/%jdk버전별 폴더%/Contents/Home 경로를 확인해준다.

그리고 터미널에서

> vi ~/.bash_profile

을 입력해 열어준다.

자바홈과 PATH를 설정해준다

> export JAVA_HOME=/Library/Java/JavaVirtualMachines/%jdk버전별 폴더%/Contents/Home  
> export PATH=${PATH}:$JAVA_HOME/bin

이후 잘 실행됨쓰
