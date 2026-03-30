# AndroidStudio-study
# 📱 CS 교육 앱 개발 일지 — Day 1

**2026.03.31** | Android Studio + Kotlin + Jetpack Compose

---

## 오늘 한 것 한줄 요약

> Android Studio 설치부터 실제 Galaxy S22 Ultra에 Hello World 띄우기까지 — 첫 삽을 떴다.

---

## 🛠️ 개발 환경

| 항목 | 내용 |
|------|------|
| 기기 | MacBook Pro 14 (2023) · Apple M2 Pro · 16GB RAM |
| OS | macOS Sequoia 15.7.4 |
| IDE | Android Studio (Apple Silicon 버전) |
| 언어 | Kotlin |
| UI | Jetpack Compose |
| 테스트 기기 | Samsung Galaxy S22 Ultra (Android 15) |

---

## 📦 프로젝트 구조 파악

Android Studio에서 Empty Activity로 프로젝트를 생성하면 기본적으로 이런 구조가 잡힌다.

```
app/
├── manifests/
│   └── AndroidManifest.xml     # 앱 이름·권한·시작화면 등록
├── kotlin+java/
│   └── com.example.myapplication/
│       ├── ui.theme/           # 색상·폰트·테마 자동생성
│       └── MainActivity.kt     # 앱 진입점 (여기서 다 시작됨)
├── res/
│   ├── drawable/               # 이미지 리소스
│   ├── mipmap/                 # 앱 아이콘
│   └── values/                 # 문자열·색상 상수
```

처음엔 파일이 많아 보여서 당황할 수 있는데, 지금 당장 건드릴 파일은 **`MainActivity.kt` 하나뿐**이다.

---

## 🔌 Galaxy S22 Ultra 연결 (USB 디버깅)

에뮬레이터 대신 실제 기기를 연결했다. M2 Mac 환경에서는 에뮬레이터보다 실제 기기가 훨씬 빠르고 안정적이기 때문.

**연결 순서**

1. 설정 → 휴대폰 정보 → 소프트웨어 정보 → **빌드번호 7번 탭** → 개발자 모드 활성화
2. 설정 → 개발자 옵션 → **USB 디버깅 ON**
3. USB-C 케이블로 Mac에 연결
4. 폰에 "USB 디버깅을 허용하시겠습니까?" 팝업 → **항상 허용** 체크 후 확인
5. Android Studio 상단 드롭다운에 **"samsung SM-S908N"** 표시 확인

처음에 `No target device found` 오류가 떴는데, USB 디버깅 설정을 빠뜨려서 생긴 문제였다. 연결하고 나니 바로 해결됐다.

---

## 👋 Hello World 출력

`MainActivity.kt`의 `Greeting` 함수에서 텍스트를 수정하는 것만으로 화면에 원하는 문구를 띄울 수 있다.

```kotlin
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello World!",   // 여기를 바꾸면 화면에 바로 반영
        modifier = modifier
    )
}
```

▶ Run 버튼 → Gradle 빌드 → S22 Ultra에 자동 설치 → 화면에 Hello World 출력 완료.

---

## 🎨 텍스트 꾸미기 (Jetpack Compose)

Compose에서는 `Text()` 컴포넌트에 파라미터를 추가하는 것만으로 스타일을 바꿀 수 있다.
XML 레이아웃 없이 Kotlin 코드만으로 UI를 구성하는 게 Compose의 핵심이다.

### 최종 코드

```kotlin
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello World!",
        fontSize = 32.sp,                    // 글자 크기
        color = Color.White,                 // 글자 색상
        fontWeight = FontWeight.Bold,        // 굵기
        textAlign = TextAlign.Center,        // 가운데 정렬
        modifier = modifier
            .fillMaxWidth()                  // 가로 꽉 채우기
            .background(Color(0xFF1A56DB))   // 배경색
            .padding(16.dp)                  // 안쪽 여백
    )
}
```

### 각 파라미터 설명

| 파라미터 | 역할 |
|----------|------|
| `fontSize = 32.sp` | 글자 크기 (sp 단위 = 사용자 폰트 설정 반영) |
| `color = Color.White` | 글자 색상 |
| `fontWeight = FontWeight.Bold` | 굵게 |
| `textAlign = TextAlign.Center` | 가운데 정렬 |
| `fillMaxWidth()` | 가로 방향으로 최대한 늘리기 |
| `background(Color(...))` | 배경색 (0xFF + 헥스코드) |
| `padding(16.dp)` | 텍스트 안쪽 여백 |

> **팁:** 빨간 줄(import 오류) 뜨면 해당 키워드에 커서 올리고 **Alt + Enter** → Import 클릭하면 자동 해결된다.

---

## 🖥️ Split 모드 (코드 + 미리보기 동시에)

매번 Run 버튼 누르지 않아도 코드 수정 결과를 바로 확인할 수 있는 방법이 있다.

**활성화 방법**

1. 코드 편집창 오른쪽 상단 아이콘에서 **Split** 클릭
2. 오른쪽 미리보기 창에서 **Build & Refresh** 클릭
3. 처음 빌드는 1~3분 소요 — 이후엔 코드 수정 시 바로 반영

> 첫 빌드가 너무 오래 걸리면 **Clean Project** 후 다시 시도하면 해결된다.

---

## ✅ 오늘 달성한 것

- [x] Android Studio 설치 (Apple Silicon 버전)
- [x] Empty Activity 프로젝트 생성
- [x] 프로젝트 폴더 구조 파악
- [x] Galaxy S22 Ultra USB 디버깅 연결
- [x] Hello World 실제 기기 출력
- [x] 텍스트 크기 · 색상 · 굵기 · 배경 꾸미기
- [x] Split 모드 미리보기 설정

---

## 🔜 다음에 할 것

- [ ] 버튼 추가 — 누르면 텍스트 바뀌는 인터랙션 구현
- [ ] `remember` · `mutableStateOf` 로 상태 관리 개념 이해
- [ ] CS 앱 프로젝트 구조 세팅 시작

---

*Android Studio 한 번도 안 써봤는데 설치부터 실제 기기 실행까지 하루에 끝냈다.*
*Kotlin도 Compose도 낯설지만, 일단 돌아가는 걸 보니까 다음이 기대된다.*