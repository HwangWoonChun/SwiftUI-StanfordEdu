# SwiftUIRect
SwiftUIRect Recture

1강 Getting started with SwiftUI
===========

1. SwiftUI Concept
   * SwiftUI를 이해하기 좋은 객체 지향 개념
      * SwiftUI 는 구조체이다. 구조체는 캡슐화를 지원하지만 객체지향이 아니다.(상속이 불가능 하기 때문) 하지만 함수형 프로그래밍을 지원한다. 이를 이용해서 UI 레벨에서 함수형 프로그래밍 디자인 모델을 사용하고 Swift는 기본적으로 객체지향 프로그래밍을 지원하기 때문에 비즈니스 로직을 위한 객체지향 프로그래밍을 사용 할 수 있다. 
        * 개인적으로 뷰모델이나 비즈니스 로직을 구조체로 가져가도 상관없지만 멤버변수의 값을 수정할때 mutating 키워드를 써야되는 등의 챙겨야 할 점이 많기 때문에 조심해야 한다. 구조체를 사용함으로서 값 타입이기 때문에 원본 데이터를 유지하는 장점을 가졌지만 우리는 다양한 비동기 라이브러리(Rx, Combine) 등이 있기 때문에 원본 데이터를 유지 할 수 가 있다.

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
        import SwiftUI
        struct ContentView: View {
            var body: some View {
                return Text("")
            }
        }
        ```
    * ContentView는 구조체 일텐데 View를 상속하네?
      * 이는 프로토콜이며 ContentView 야 View 처럼 동작하렴 이라는 의미 이다.
      * View 처럼 동작한다고 했으니 View의 대부분을 사용 하지만 약간의 책임이 따른다. body라는 변수를 꼭 써야되는 것이다.
   
    * View 처럼 동작해라
      * ContentView는 디바이스에 표현되는 직사각형 영역이다.(뷰컨트롤러의 view 처럼) View 는 이 ContentView안에서 표현되는 모든 것들이 View가 될 수 있다.
      * 함수형 프로그래밍이 지원하는 여러 modifier를 통해 ContentView를 구축 해 나갈 것 이다.

    * body: some View
      * body 는 여러 뷰들을 조립하는 역할을 한다. body 는 함수를 실행하여 동작하는 변수이다. 위 코드 처럼 텍스트를 반환하고 화면에 노출 시킨다.
      * some View 는 컴파일러에게 body가 뷰의 일부분이다 라고 알려주는 역할을 한다. 실제로 var body: Text 로 컴파일러는 코드를 변환 시킬 것 이다.
      * some View를 사용하지 않으면 어떤 타입의 뷰가 반환되는지 일일이 지정해줘야 한다.
