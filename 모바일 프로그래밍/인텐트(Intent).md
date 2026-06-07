# 인텐트(Intent)

### 기본 개념

- 안드로이드 4대 컴포넌트가 서로 통신하거나 데이터를 주고받기 위해 사용하는 ‘메신저/우편배달부’ 역할의 객체
- 새로운 액티비트를 화면에 띄울 때
- 백그라운드 서비스를 시작할 때
- 다른 컴포넌트에 값을 넘겨주거나 처리 결과를 받아올 때

### 명시적 인텐트(Explicit Intent)

- 호출할 대상을 클래스명으로 명확하게 지정하는 인텐트
- 주로 내가 만든 앱 안에서 메인 화면에서 서브 화면으로 전활 할 때 사용

```kotlin
//MainActivity에서 SecondActivity 클래스를 명시적으로 지정하여 실행
val intent = Intent(applicationContext, SecondActivity::class.java)
startActivity(intent)
```

### 암시적 인텐트(Implicit Intent)

- 호출할 대상의 이름을 정확히 모르는 상태에서 안드로이드 시스템에 “**나 이런 ‘행동(action)’을 하고 싶은데, 이거 할 줄 아는 컴포넌트 나와라!”** 하고 요청하는 인텐트
- 웹 브라우저 열기, 전화 걸기, 지도 보기 등 OS 시스템의 기본 앱이나 외부 앱을 실행할 때 사용

```kotlin
//특정 전화번호로 전화를 걸겠다는 '행동(ACTION_DIAL)'을 요청
val intent = Intent(Intent.ACTION_DIAL, Url.parse("tel:01012345678"))
startActivity(intent)
```

### 인텐트를 이용한 데이터 전달(putExtra / getExtra)

- 인텐트는 단순히 화면을 바꾸는 것뿐만 아니라, 새로운 화면으로 데이터(파라미터)를 배달하는 일도 함
- 메인 액티비티에서 서브 액티비티로 데이터 보낼 때
    - `intent.putExtra("Key값", 실제값)` 구조를 사용하여 데이터를 담아 보냄
    
    ```kotlin
    val intent = Intent(applicationContext, SecondActivity::class.java)
    intent.putExtra("Num1", 100) // "Num1"이라는 이름으로 숫자 100을 저장
    intent.putExtra("Num2", 200) // "Num2"이라는 이름으로 숫자 200을 저장
    startActivity(intent)
    ```
    
- 서브 액티비티에서 데이터를 받아서 사용할 때
    - `intent.get데이터타입Extra("Key값")` 메소드로 넘겨받은 값을 꺼냄
    - 값이 없을 대를 대비한 디퐅값을 함께 적어줌
    
    ```kotlin
    //넘겨받은 인텐트에서 값을 꺼냄(디폴트 값은 0)
    val value1 = intent.getIntExtra("Num1", 0)
    val value2 = intent.getIntExtra("Num2", 0)
    ```