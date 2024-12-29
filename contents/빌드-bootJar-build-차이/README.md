# gradle : taks bootJar과 task build의 차이점

### bootJar 사이클

```
오전 1:40:54: Executing 'bootJar'...

> Task :compileJava UP-TO-DATE
> Task :processResources UP-TO-DATE
> Task :classes UP-TO-DATE
> Task :resolveMainClassName UP-TO-DATE
> Task :bootJar UP-TO-DATE

BUILD SUCCESSFUL in 727ms
4 actionable tasks: 4 up-to-date
오전 1:40:55: Execution finished 'bootJar'.

```

### build 사이클

```
오전 1:39:45: Executing 'build'...

> Task :compileJava UP-TO-DATE
> Task :processResources UP-TO-DATE
> Task :classes UP-TO-DATE
> Task :resolveMainClassName UP-TO-DATE
> Task :bootJar UP-TO-DATE
> Task :jar
> Task :assemble
> Task :compileTestJava
> Task :processTestResources NO-SOURCE
> Task :testClasses
OpenJDK 64-Bit Server VM warning: Sharing is only supported for boot loader classes because bootstrap classpath has been appended
> Task :test
> Task :check
> Task :build

BUILD SUCCESSFUL in 9s
7 actionable tasks: 3 executed, 4 up-to-date
오전 1:39:54: Execution finished 'build'.
```

### 두 task 에서의 공통 작업

- compileJava : `src/main/java`에 있는 java 파일을 컴파일 하여 `build/classes/java/main`에 저장
- processResources : `src/main/resources`에 있는 리소스 파일을 `build/resources/main`에 저장
- classes : class 파일과 리소스 결합
- resolveMainClassName : 애플리케이션의 메인 클래스 식별
- bootJar : 실행 가능한 jar 파일 생성

### task build만 수행하는 작업

- jar : 일반 jar 파일 생성
- assemble : 실행 가능한 jar 파일 + 일반 jar 파일
- compileTestJava : `src/test/java`에 있는 java 파일을 컴파일하여 `build/classes/java/test`에 저장
- processTestResources : `src/test/resources`에 있는 리소스 파일을 `build/resources/test`에 저장
- testClasses : 테스트를 위한 클래스 파일과 리소스 결합
- test : 테스트 수행
- check : 모든 테스트 수행
- build : 테스트를 포함한 완전한 빌드 수행

### 차이점

- 완전한 빌드가 필요한 경우 (실행 가능한 jar, 일반 jar, 테스트) : build
- 실행 가능한 jar만 필요한 경우 : bootJar
