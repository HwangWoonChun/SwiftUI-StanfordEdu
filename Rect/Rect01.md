# SwiftUIRect
SwiftUIRect Recture

1강 Getting started with SwiftUI
===========

1. SwiftUI Concept
   * SwiftUI를 이해하기 좋은 객체 지향 개념
      * SwiftUI 는 구조체이다. 구조체는 캡슐화를 지원하지만 객체지향이 아니다.(상속이 불가능 하기 때문) 하지만 함수형 프로그래밍을 지원한다. 이를 이용해서 UI 레벨에서 함수형 프로그래밍 디자인 모델을 사용하고 Swift는 기본적으로 객체지향 프로그래밍을 지원하기 때문에 비즈니스 로직을 위한 객체지향 프로그래밍을 사용 할 수 있다. 

2. SwfitUI 의 장점 
   * 애니메이션을 다루기가 무지하게 쉽다.
   * 텍스트를 중앙에 두거나 디바이스 로테이션 UI 를 구현하려면 약간의 코드가 필요하지만 SwiftUI 는 이를 자동으로 처리해 준다.
   * SwiftUI 는 UI를 개발하기 위함으로서 존재한다. 비즈니스 로직을 위한 라이브러리가 아니다. SwiftUI는 이를 명확하게 분리해준다.

3. 프리뷰
    * 실시간 코드를 반영하여 확인 할 수 있는 시스템

4. 프로젝트 살펴보기
   * App.swift

    ``` swift 
    import SwiftUI

    @main
    struct MemorizeApp: App {
        var body: some Scene {
            WindowGroup {
                ContentView()
            }
        }
    }
    ```
    * 많이 사용하지는 않는다.
    * 주요깊게 봐야되는 부분
      * @main : 앱이 실행될때 시작하는 메인 c 모듈인 main.c 를 의미한다.
      * WindowGroup : 메인이 되는 화면영역이 어딘지 설정

* ContentView.swift
``` swift 

```
