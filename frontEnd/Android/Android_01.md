---
title: 안드로이드
author : 손현호
date: 2021-06-07
---

# Andorid

- 리눅스 커널에서 모바일에 유용한 기능을 뽑아 안드로이드 OS로 사용
- 모바일 기기에 최적화된 `달빅` 또는 `아트 런타임`을 제공
- 모바일용 데이터베이스 SQLite를 제공
- OpenGL등도 지원

### 안드로이드 구조
- 응용프로그램
    - 안드로이드 스마트폰에서 사용 가능한 일반적인 응용프로그램.
- 응용프로그램 프레임워크
    - 안드로이드 API가 존재하는 곳.
-  안드로이드 런타임 /라이브러리
    - 라이브러리: 안드로이드 시스템 라이브러리 (C로 작성)
    - 안드로이드 런타임: 달빅 또는 아트 런타임, java 코어 라이브러리로 구성.
- 리눅스 커널
    - 하드웨어 운영 관련 시스템관리 기능 제공


### AVD(Android Virtual Devics)

- 안드로이드 가상머신으로 작성한 코드를 컴퓨터 내에서 가상 기기환경으로 확인 할 수 있도록 해준다.



### 모듈
- 안드로이드의 실행 단위
- 다른 모듈은 다른 어플로 판단할 수 있다.

### 안드로이드의 Acitvity
- 안드로이드의 화면 단위라고 할 수 있다.
- 안드로이드는 `Activity`라는 클래스를 상속 받아야만 사용 가능.
- Activity를 만들면 manifests에 등록을 해주어야 한다.

### res(R)
- 사진, 값 , 레이아웃등 안드로이드에서 사용할 리소스를 저장한다.
- res 폴더 아래 있는 파일은 `R.폴더명.id`형식으로 불러 올 수 있다
- res 폴더 아래에 있는 데이터들은 `int final`의 번호를 지닌다.
    - int layoutResID(`setContentView`의 값으로 사용됨)




---

## res

- res파일 내부에 저장된 xml 파일들은 내부에서 자동으로 class로 변경되어 저장된다.


### Attrubutes

- XML의 태그형태로

- `android:id="@+id/checkBox"`
    - 현 태그의 이름을 붙여 식별가능하게 해준다
    - `@+id`는 새로 선언하는 리소스 아이디이므로 반드시 추가해야한다는 의미
    - `@android:id`: 안드로이드에 이미 예약되어 있는 리소스
    - `@id`: 이미 추가된 리소스를 참조하겠다는 의미
    - 지정된 id는 id라는 클래스 내부에 final static int 형으로 저장되는데 id값으로 지정된 값을 변수명으로 하여 지정된다.  
    `public static final int checkBox = (자동 초기화된 중복없는 숫자값)`
    
- `android:layout_width(height)="값"`
    - 안드로이드의 해당 태그의 레이아웃의 가로,세로값을 결정함
    - `match_parent`는 부모 태그의 크기만큼 크게 맞춘다는 의미
    - `wrap_content`는 해당 태그의 컨텐츠 영역만큼의 크기에 맞게 맞춘다는 의미.
-   `android:text="BUTTON"`
    - 콘텐츠 내용에 Text로 "BUTTON"이 들어간다.



    
    
### Activity

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        // 레이아웃 -> Java Code화
        // R클래스 -> 레이아웃 -> activity_main 과 연결. 
        Button btn = findViewById(R.id.button);
        // Buuton 태그를 받을 수 있는 참조형으로 ID 값을 찾아서 참조함.
    }
}
```

