# gradle : 빌드 시 특정 리소스 제외

## given

![alt text](../../images/20241227_203219.png)

## when

```
sourceSets {
    main {
        resources {
            exclude "**/local/**"
            exclude "**/dev/**"
            exclude "**/prod/**"
        }
    }
}
```

```
./gradlew clean bootJar
```

## then

![alt text](../../images/20241227_203338.png)