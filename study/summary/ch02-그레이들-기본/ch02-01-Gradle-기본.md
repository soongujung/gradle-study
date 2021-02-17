# Chapter02. Gradle 기본

# 참고자료

## 책

[엔터프라이즈 빌드 자동화를 위한 Gradle - 윤석진 저](http://www.yes24.com/Product/Goods/20052289)

  

## 공식문서

- [gradle.org - getting started](https://gradle.org/guides/#getting-started)

- [github.com/gradle](https://github.com/gradle/gradle)

- Gradle 의 Project
  - [Gradle Manual - Project](https://docs.gradle.org/current/dsl/org.gradle.api.Project.html)
  - [Gradle API Docs - Project](https://docs.gradle.org/current/javadoc/org/gradle/api/Project.html)
- 가이드문서
    - https://docs.gradle.org/current/javadoc/org/gradle/api/Project.html
  - 설명페이지
    - https://docs.gradle.org/current/dsl/org.gradle.api.Project.html
  
- Gradle 의 Task

  - [Gradle Manual -Task](https://docs.gradle.org/current/dsl/org.gradle.api.Task.html)

  

# 인터페이스 "Project"

> 참고자료 : [docs/gradle.org/.../gradle/api/Project.html](https://docs.gradle.org/current/javadoc/org/gradle/api/Project.html)

책에서는 UML로 설명하고 있었다. Project 인터페이스에 대해서 설명해주고 있었는데, 이 인터페이스라는 말이 흔히 사람들이 사용하는 "인터페이스"라는 의미인것인지, JAVA 에서의 "인터페이스"인지 혼동이 되었었다.  

이런 이유로 [참고자료](https://docs.gradle.org/current/javadoc/org/gradle/api/Project.html)를 읽어보게 되었는데, JAVA의 "인터페이스"인데, "인터페이스 명"이 "Project" 로 이름지어져 있는 것을 의미하는 것이었다. Groovy 역시 JVM위에서 동작하는 것이라서 Java의 문법을 따르는 것으로 보인다.  

Java 언어에 가끔 불만이 생기는 것은 키워드를 너무 실생활에서 사용하는 용어로 만들었다는 점이다. 새로운 것을 익힐때 이게 현실세계의 그 단어인지 혼동되게 한다는 점은 가끔 스트레스이기도 한 것 같다. (* 잘못된 기억일지는 잘 모르겠지만... C++에서는 virtual 이라는 키워드가 interface와 비슷한 역할을 했던것으로 기억하고 있다.)



**인터페이스 "Project" 내의 멤버필드/멤버함수**  

![이미지](INTERFACE_Project.png)

위의 그림은 인터페이스 'Project'를 간단하게 그림으로 요약해본 그림이다. 책에서 보여주는 **그림 2-1**과 [공식문서](https://docs.gradle.org/current/javadoc/org/gradle/api/Project.html)를 참고해 이해한 대로 그려봤다. 혼자 공부하는 용도인지라 UML 문법은 간단하게 무시했다. **'나중에 다 까먹은 후에 다시 봤을때 내가 이해할수 있을까?'**를 기준으로 다시 그려봤다.  



## 멤버필드 요약

- DEFAULT_BUILD_DIR_NAME
  - 빌드한 결과물이 저장되는 디렉터리
  - 그레이들에서는 기본 설정으로 빌드 결과물이 저장되는 디렉터리는 build 디렉터리이다.
  - ex) 메이븐의 target 디렉터리
- DEFAULT_BUILD_FILE
  - 프로젝트 설정에 대한 정보를 담고 있는 파일
  - 그레이들의 기본설정은 build.gradle 이다.
  - build.gradle 파일 내에 빌드에 관련된 설정들을 정의한다.
- GRADLE_PROPERTIES
  - 프로퍼티들을 key/value 형태의 프로퍼티(Properties)파일에 대한 속성
  - build.gradle 파일과 함께 생성되며, 속성을 정의해서 사용가능하다.
- SYSTEM_PROP_PREFIX
  - 프로퍼티 파일을 사용할 때 접두어가 SYSTEM_PROP 인 이유는 SystemPropertiesHandler 에서 프로퍼티 파일을 읽을 때 다른 속성값들과 구분하기 위해 'SystemProp\\\\.(.\*)' 과 같은 형태를 사용하기 때문이라고 한다.



# 인터페이스 "Task"

> 참고자료
>
> - [Gadle API Docs - Task](https://docs.gradle.org/current/javadoc/org/gradle/api/Task.html)
> - [Gradle API 매뉴얼](https://docs.gradle.org/current/dsl/org.gradle.api.Task.html)

Gradle 공식문서의 Project API에 대한 [설명서](https://docs.gradle.org/current/javadoc/org/gradle/api/Project.html) 에서는 Task를 아래와 같이 설명하고 있다.

> A project is essentially a collection of [`Task`](https://docs.gradle.org/current/javadoc/org/gradle/api/Task.html) objects.  
>
> "프로젝트는 본질적으로 Task 개체의 모음입니다."

그리고 Task API에서는 Task API를 아래와 같이 설명하고 있다.

> Each task belongs to a [`Project`](https://docs.gradle.org/current/javadoc/org/gradle/api/Project.html). You can use the various methods on [`TaskContainer`](https://docs.gradle.org/current/javadoc/org/gradle/api/tasks/TaskContainer.html) to create and lookup task instances. For example, [`TaskContainer.create(String)`](https://docs.gradle.org/current/javadoc/org/gradle/api/tasks/TaskContainer.html#create-java.lang.String-) creates an empty task with the given name. You can also use the `task` keyword in your build file:  
>
> task 는 Project에 속한다. Task 인스턴스 들을 생성하고 찾기 위해(lookup) TaskContainer 내의 다양한 메서드를 사용할 수 있습니다. 예를 들면 TaskContainer.create(String) 은 원하는 이름으로 지어진 비어있는 태스크를 생성하는 메서입니다.  
>
> task 키워드를 빌드 파일 내에서 사용하는 것 역시 가능합니다.



**인터페이스 "Task" 내의 멤버필드/멤버함수**  

![이미지](INTERFACE_Task.png)

  

프로젝트는 위와 같이 생긴 인터페이스를 가지고 있다. Task 는 프로젝트를 기준으로 실행된다. Task를 실행할 때 Task 인터페이스에서는 기본적으로 Task의 이름과 Task의 유형, Task의 의존성 여부, Task 액션 등을 속성으로 가지고 있다. 즉 Task 인터페이스는 Action 을 가지고 있다.



# Gradle 빌드 라이프사이클

Gradle 의 빌드 라이프사이클은 아래와 같이 크게 세 단계로 나뉘어진다.

- 초기화
- 설정
- 실행



## 초기화

그레이들이 초기화 되는 단계이다. 이때 settings.gradle 의 값들을 build.gradle에서 참조하여 프로젝트의 정보를 세팅할 수 있다. settings.gradle 에 정의하는 내용들을 예로 들어보면 아래와 같다.

- 프로젝트를 싱글 프로젝트로 구성할 것인지 멀티 프로젝트로 구성할 것인지 지정
- 프로젝트 이름 지정 등등... 더 찾아봐야 하는데 아직은 모르는게 많다.



**디렉터리별 참조 순서**  

- 현재 작업중인 루트 디렉터리에 settings.gradle 파일이 없으면 상위 디렉터리에 settings.gradle 파일이 잇는지 검사한다.
- 상위 디렉터리에도 settings.gradle 파일이 없다면 이 빌드는 싱글 프로젝트로 인식하여 실행하게 된다.



## 설정

> 참고자료 :  
>
> 책 \"[엔터프라이즈 빌드 자동화를 위한 Gradle - 윤석진 저](http://www.yes24.com/Product/Goods/20052289)\"의 각 챕터를 따라가면서 기본적인 내용을 주 교재로 삼아서 정리하되 Gradle 공식문서의 내용들을 참고해서 정리했다.
>
> - [Gradle 공식문서 - build lifecycle](https://docs.gradle.org/current/userguide/build_lifecycle.html)

프로젝트 인스턴스화가 끝난 후 설정 정보가 프로젝트에 반영되는 단계이다. Maven 과는 다르게 Gradle은 실행 중(런타임)에도 설정을 반영할 수 있다. Maven 의 경우 선언형 프로젝트 설정이고, Gradle은 Groovy 언어 기반의 스크립트기반 프로젝트 설정이기 때문이다. 이런 이유로 동적인 설정이 가능하다.  

이 때 settings.gradle 내의 설정을 변경하여 동적으로 프로젝트의 속성을 바꾸는 것이 가능하다고 한다.  

  

## 실행

Gradle 은 이전 단계에서 구성된 Task의 부분집합을 이름으로 구분하고, 그 이름이 Gradle에 전달되어 실행된다.



# gradle init

> 참고자료 :  
>
> 책 \"[엔터프라이즈 빌드 자동화를 위한 Gradle - 윤석진 저](http://www.yes24.com/Product/Goods/20052289)\"의 각 챕터를 따라가면서 기본적인 내용을 주 교재로 삼아서 정리하되 Gradle 공식문서의 내용들을 참고해서 정리했다.  

Gradle 프로젝트를 초기화 하는 과정이다. gradle init 명령어 수행시 --type 파라미터에 대한 값으로 아래의 값들을 지정할 수 있다.

- basic
- groovy-library
- groovy-gradle-plugin
- groovy-application
- java-library
- java-application
- java-gradle-plugin
- cpp-application
- cpp-library
- kotlin-application
- kotlin-gradle-plugin
- kotlin-library
- pom



정말 어렵고 골치아파보이는 옵션들이 많이 보인다. 이중에서 Basic, Groovy-library 를 기반으로 예제를 정리해볼 예정이다.  (위와 같은 지원되는 type 들은 gradle help --task :init 명령어로 확인 가능하다.)

  

## gradle 에서 사용 가능한 타입들을 검색해보기

```bash
➜ gradle help --task :init

> Task :help
Detailed task information for :init

Path
     :init

Type
     InitBuild (org.gradle.buildinit.tasks.InitBuild)

Options
     --dsl     Set the build script DSL to be used in generated scripts.
               Available values are:
                    groovy
                    kotlin

     --package     Set the package for source files.

     --project-name     Set the project name.

     --test-framework     Set the test framework to be used.
                          Available values are:
                               junit
                               junit-jupiter
                               kotlintest
                               scalatest
                               spock
                               testng

     --type     Set the type of project to generate.
                Available values are:
                     basic
                     cpp-application
                     cpp-library
                     groovy-application
                     groovy-gradle-plugin
                     groovy-library
                     java-application
                     java-gradle-plugin
                     java-library
                     kotlin-application
                     kotlin-gradle-plugin
                     kotlin-library
                     pom
                     scala-library
                     swift-application
                     swift-library

Description
     Initializes a new Gradle build.

Group
     Build Setup

BUILD SUCCESSFUL in 557ms
1 actionable task: 1 executed
```



## gradle 프로젝트 생성 (CLI)

**프로젝트 생성하기 :: gradle init**

```bash
➜ mkdir ch02-gradle-init-basic
➜ cd ch02-gradle-init-basic
➜ gradle init

Select type of project to generate:
  1: basic
  2: application
  3: library
  4: Gradle plugin
Enter selection (default: basic) [1..4] 2

Select implementation language:
  1: C++
  2: Groovy
  3: Java
  4: Kotlin
  5: Swift
Enter selection (default: Java) [1..5] 3

Select build script DSL:
  1: Groovy
  2: Kotlin
Enter selection (default: Groovy) [1..2] 1

Select test framework:
  1: JUnit 4
  2: TestNG
  3: Spock
  4: JUnit Jupiter
Enter selection (default: JUnit 4) [1..4] 4

Project name (default: ch02-gradle-init-basic):
Source package (default: ch02.gradle.init.basic):

> Task :init
Get more help with your project: https://docs.gradle.org/5.6.4/userguide/tutorial_java_projects.html

BUILD SUCCESSFUL in 36s
2 actionable tasks: 2 executed
```



**Gradle 프로젝트 구성 살펴보기**  

```bash
➜ ls -al
total 48
drwxr-xr-x  9 kyle.sgjung  staff   288  2 11 13:54 .
drwxr-xr-x  3 kyle.sgjung  staff    96  2 11 13:54 ..
-rw-r--r--  1 kyle.sgjung  staff   103  2 11 13:54 .gitignore
drwxr-xr-x  4 kyle.sgjung  staff   128  2 11 13:54 .gradle
-rw-r--r--  1 kyle.sgjung  staff   200  2 11 13:54 build.gradle
drwxr-xr-x  3 kyle.sgjung  staff    96  2 11 13:54 gradle
-rwxr-xr-x  1 kyle.sgjung  staff  5960  2 11 13:54 gradlew
-rw-r--r--  1 kyle.sgjung  staff  2942  2 11 13:54 gradlew.bat
-rw-r--r--  1 kyle.sgjung  staff   371  2 11 13:54 settings.gradle
```

- gradlew.bat, gradlew
  - 래퍼파일이다.
  - Github과 같은 repository 에 공유하면 다른 사용자는 운영체제나, gradle 환경(버전 등등)등과 같은 개발환경에 제약없이 동일한 환경 내에서 실행이 가능해진다.
  - 이 래퍼 파일에 대한 설정은 gradle/wrapper/graddle-wrapper.properties 에 정의되어 있다.
- settings.gradle
  - 멀티 프로젝트를 구성하는 데에 사용되는 파일이다
- build.gradle
  - Gradle 을 사용할 때 가장 중요하고 기본이 되는 파일
  - 빌드 스크립트 파일



## build.gradle 의 일반적인 형식

아래는 gradle init 시에 type 을  application 으로 지정하여 생성한 프로젝트 내의 build.gradle 파일이다. 아래의 내용중에 몇 가지만 살짝 맛만  느낄 정도로 정리해보고 넘어가야 할 것 같다.

```groovy
/*
 * This file was generated by the Gradle 'init' task.
 *
 * This generated file contains a sample Java project to get you started.
 * For more details take a look at the Java Quickstart chapter in the Gradle
 * User Manual available at https://docs.gradle.org/5.6.4/userguide/tutorial_java_projects.html
 */

plugins {
    // Apply the java plugin to add support for Java
    id 'java'

    // Apply the application plugin to add support for building a CLI application
    id 'application'
}

repositories {
    // Use jcenter for resolving dependencies.
    // You can declare any Maven/Ivy/file repository here.
    jcenter()
}

dependencies {
    // This dependency is used by the application.
    implementation 'com.google.guava:guava:28.0-jre'

    // Use JUnit Jupiter API for testing.
    testImplementation 'org.junit.jupiter:junit-jupiter-api:5.4.2'

    // Use JUnit Jupiter Engine for testing.
    testRuntimeOnly 'org.junit.jupiter:junit-jupiter-engine:5.4.2'
}

application {
    // Define the main class for the application
    mainClassName = 'sample.App'
}

test {
    // Use junit platform for unit tests
    useJUnitPlatform()
}
```



저장소

- 일반적으로 http://mvnrepository.com 과 같은 다운로드 경로를 적지만 위의 예제처럼 jcenter() 와 같은 메서드로 대체하는 것 역시 가능하다.
- mavenCentral 메서드 또한 사용하는 경우가 잇다. 자세한 내용은 [엔터프라이즈 빌드 자동화를 위한 Gradle - 윤석진 저](http://www.yes24.com/Product/Goods/20052289) 의 4장에서 친절하게 설명해주고 있다.











