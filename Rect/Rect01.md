# SwiftUIRect
SwiftUIRect Recture

1강 Getting started with SwiftUI
===========

1. SwiftUI Concept
* SwiftUI를 이해하기 좋은 객체 지향 개념 - 캡슐화
  * 객체지향의 주요 요소 중 하나가 캡슐화이다. SwiftUI는 객체지향프로그래밍이 아니며 구조체 자료구조를 이용한다.
  * 멤버 변수와 함수를 하나로 묶어 데이터를 구조화 시킨다.
  * 실제로 구조화 된 코드를 확인 할 수 가 있다.
    ``` swift  
      import SwiftUI
      struct ContentView: View {
          var body: some View {
              return Text("")
          }
      }
      ```
* SwfitUI 의 장점 
  * 애니메이션을 다루기가 무지하게 쉽다.
  * 텍스트를 중앙에 두거나 디바이스 로테이션 UI 를 구현하려면 약간의 코드가 필요하지만 SwiftUI 는 이를 자동으로 처리해 준다.

* 프리뷰
  * 실시간 코드를 반영하여 확인 할 수 있는 시스템

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
