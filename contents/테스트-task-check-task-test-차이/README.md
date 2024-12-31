# gradle : task check와 task test의 차이

task test : 단위 테스트 수행

task check : 단위 테스트 + 이외 설정된 검증 작업 수행

## task test 사이클

```
> Task :compileJava UP-TO-DATE
> Task :processResources UP-TO-DATE
> Task :classes UP-TO-DATE
> Task :compileTestJava UP-TO-DATE
> Task :processTestResources NO-SOURCE
> Task :testClasses UP-TO-DATE
> Task :test UP-TO-DATE
```

## task check 사이클

```
> Task :compileJava UP-TO-DATE
> Task :processResources UP-TO-DATE
> Task :classes UP-TO-DATE
> Task :compileTestJava UP-TO-DATE
> Task :processTestResources NO-SOURCE
> Task :testClasses UP-TO-DATE
> Task :test UP-TO-DATE

> Task :spotbugsMain
> Task :spotbugsTest
> Task :spotbugsMain
> Task :check
```

## 공통되는 task

###  클래스 파일, 리소스 파일 -> ./build 이관

- compileJava
- processResources
- classes

### 테스트 용 클래스 파일, 리소스 파일 -> ./build 이관

- compileTestJava
- processTestResources
- testClasses
- test

## task check 만 수행하는 작업

build.gradle에 추가 검증을 위한 플러그인을 세팅해둔만큼 추가 task가 수행된다. 필자는 정적 검증을 위해 SpotBugs 플러그인을 추가하였기에 위 task들 이외에 spotbugsTest와 spotbugsMain를 추가 수행하였다.

- spotbugsTest
- spotbugsMain
- check

