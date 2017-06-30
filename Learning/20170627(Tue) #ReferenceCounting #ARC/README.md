# 패스트캠퍼스 강의 노트 34th ( 20170627 )

# 오늘의 Tip

## Google SpreadSheet로 plist 쉽게 만들기
 - `$`: 고정
 - `&`: 나열
 - `CHAR(10)`: 줄바꿈
 - `#Must_Remember`: &, $, CHAR(10)

#### `[Sample]`
 : `=$B$2&CHAR(10)&$E$1&CHAR(10)&E2&CHAR(10)&$F$1&CHAR(10)&F2&CHAR(10)&$B$3`

 → [구글 스프레드시트 바로가기](https://docs.google.com/spreadsheets/d/144mYHbhKwN1uWV5N3tBn3zHywVo8eivY1g6iL1b26BE/edit?usp=sharing)

---

# Reference counting

## 메모리 관리 방식
 - `레퍼런스 카운팅` : 오너쉽 정책에 의해 객체의 해제 정의

```swift
// Objective-C
NSString *str1 = [[NSString alloc] init]; // 메모리에 공간을 할당하고, retain + 1이 된다.

// retain은 로직의 마지막에서 0이 되어야 한다.
```

## Memory leak의 Sample 1

```swift
// Objective-C
NSString *str1 = [[NSString alloc] init];

```
 - str2에 새로운 인스턴스가 생성되면서, 이전에 만들었던 인스턴스는 주소값이 사라지고, 가리키고 있는 변수도 사라졌다. 그래서 그 녀석에게 접근할 수 있는 방법도 없고, 지울 수도, 수정할 수도 없다. 메모리만 차지하고 있을 뿐이고, 앱을 종료하기 전까지 메모리를 차지한다. 이 현상을 메모리 누수(Memory leak)이라고 한다.

## Memory leak의 Sample 2

```swift
// Objective-C
NSString *str1 = [[NSString alloc] init];
```
 - 위 문제를 해결한다고 해도 Memory leak이 난다.

## Ownership Policy
 - 오너쉽을 가진 객체만 reference count가 증가된다.


# ARC

## Strong & weak
> (한줄요약) Strong은 보통의 변수 선언과 같이 오너십과 참조 포인트를 갖고, Weak는 참조 포인트만을 갖는다.

 - Strong 변수는 무조건 Ownership을 가지고, 객체에 대한 참조 포인트를 갖는다.
 - ARC는 {(중괄호)가 시작되면, 레퍼런스 카운트를 1 올리고, 중괄호가 닫히면, 1 내린다.
 - weak는 약한 참조로 소유권은 없이 참조를 할 수 있는 권한만을 갖는다.

```swift
// Objective-C

// Swift
var p1:Person
```

```swift
p1 = [[Person alloc] init];
```

### weak pointer 사용 이유
 - `Autorelease pool`을 대신해서 자동 해제가 필요한 경우.
 - view의 strong 참조 때문에 --> `@IBOutlet` 할 때, Weak로 선언하는 이유는 뷰 컨트롤러가 사라질 때, 해당 뷰들도 함께 사라지기는 하지만, 싱글턴 등등의 방법으로 뷰 관리를 따로 할 때, 함께 증발되도록 하기 위함이다.

## unowned Keyword
> `weak`가 항상 옵셔널이기 때문에 때에 따라 `unowned`를 사용하기도 한다.

 - weak와 마찬가지로 unowned가 참조하는 인스턴스를 강력하게 보류하지 않는다.
 - unowned keyowrd를 프로퍼티나 변수 앞에 선언하여 표시해준다.
 - unowned는 항상 값이 있다는 것을 의미한다.


# Closure Capture

 - 클로져 안의 모든 상수와 변수에 대한 참조를 캡쳐해서 관리한다.
 - 한 Swift는 캡쳐를 위한 모든 메모리를 관리한다.


```swift

```

---
### 문서 끝 ( by 재성 )