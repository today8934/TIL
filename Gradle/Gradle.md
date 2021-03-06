# Gradle

## 빌드 관리 도구란

---

- 프로젝트에서 필요한 xml, properties, jar파일들을 자동으로 인식하여 빌드해주는 도구
- 소스코드를 컴파일, 테스트, 정적분석 등을 하여 실행가능한 앱으로 빌드해줌
- 프로젝트 정보 관리, 테스트 빌드, 배포 등의 작업을 진행해줌
- 외부 라이브러리를 참조하여 자동으로 다운로드 및 업데이트 등 관리해줌
- Java의 대표적인 빌드 도구 : Ant, Maven, Gradle

## Gradle이란?

---

- Groovy 스크립트를 활용한 빌드 관리 도구
- 멀티 프로젝트의 빌드에 최적화 하여 설계됨
- Maven에 비해 더 빠른 처리속도
- Maven에 비해 더 간결한 구성 가능

## Gradle과 Maven비교

---

- Maven에 비해 Gradle이 대규모 프로젝트에서 용이
- Maven : pom.xml
- Gradle : build.gradle
- Gradle은 설치 없이 사용할 수 있다.(Gradle Wrapper)

## Gradle의 대표 용어 설명

---

- repositories : 라이브러리가 저장된 위치 등 설정
- mavenCentral : 기본 Maven Repository
- dependencies : 라이브러리 사용을 위한 의존성 설정
- Maven Repository : https://mvnrepository.com/

## build.gradle

---

```groovy
/*
 * This file was generated by the Gradle 'init' task.
 *
 * This generated file contains a sample Java application project to get you started.
 * For more details take a look at the 'Building Java & JVM projects' chapter in the Gradle
 * User Manual available at https://docs.gradle.org/7.1/userguide/building_java_projects.html
 */

plugins {
    // Apply the application plugin to add support for building a CLI application in Java.
    id 'application' //응용 프로그램에 대한 기능을 제공하는 플러그인

    id 'java' //Java 프로그램을 위한 기능 제공 플러그인
}

repositories {
    // Use Maven Central for resolving dependencies.
    mavenCentral() //Apache Maven 중앙 저장소를 이용

		jcenter //Maven과 Gradle 등 각종 빌드 도구에서 사용할 수 있는 공개 저장소
}

dependencies { //repositories에서 설정한 저장소의 라이브러리들을 사용하기 위한 선언
    // Use JUnit test framework.
    testImplementation 'junit:junit:4.13.2' //테스트 컴파일 시 의존 라이브러리

    // This dependency is used by the application.
    implementation 'com.google.guava:guava:30.1-jre' //컴파일 시 의존 라이브러리
}

application {
    // Define the main class for the application.
    mainClass = 'com.studio.tdd.App' //메인클래스 지정
}
```

## Gradle 태스크

---

- 태스크 정의

```groovy
task 태스크명{
    ...... 수행할 처리 ......
}
```

- 태스크 실행

```bash
$ gradle 태스크명
```

- doFirst와 doLast - 태스크의 기본적인 처리 등이 있을 때는 그 전에 실행하는 것과 후에 실행하는 것

    doFirst : 최초에 수행하는 액션

    doLast : 최후에 수행 하는 액션

```groovy
task hello {
    doLast {
        println('이것은 hello 태스크의 doLast이다.')
    }
    doFirst {
        println('이것은 hello 태스크의 doFirst이다.')
    }
}
```

> [https://www.youtube.com/watch?v=3Jp9kGDb01g](https://www.youtube.com/watch?v=3Jp9kGDb01g)

> [https://madplay.github.io/post/what-is-gradle](https://madplay.github.io/post/what-is-gradle)

> [http://www.devkuma.com/books/pages/1064](http://www.devkuma.com/books/pages/1064)
