# SwiftUIRect
SwiftUIRect Recture

``` swift 
```


2강 Learning more about SwiftUI
===========

1. Horizontal 형태로 표현

    ``` swift 
    struct ContentView: View {
        var body: some View {
            HStack {
                ZStack(content: {
                    RoundedRectangle(cornerRadius: 20).stroke(lineWidth: 3)
                    Text("Hello Word")
                })
                ZStack(content: {
                    RoundedRectangle(cornerRadius: 20).stroke(lineWidth: 3)
                    Text("Hello Word")
                })
                ZStack(content: {
                    RoundedRectangle(cornerRadius: 20).stroke(lineWidth: 3)
                    Text("Hello Word")
                })
                ZStack(content: {
                    RoundedRectangle(cornerRadius: 20).stroke(lineWidth: 3)
                    Text("Hello Word")
                })
            }
        }
    }
    ```

2. 리팩토링 - 반복되는 코드를 위한 구조체

    <img src = "https://github.com/HwangWoonChun/SwiftUI-StanfordEdu/blob/main/Img/Simulator%20Screen%20Shot%20-%20iPod%20touch%20(7th%20generation)%20-%202022-01-25%20at%2010.50.02.png" width = 160 height = 240>
    
    <img src = "https://github.com/HwangWoonChun/SwiftUI-StanfordEdu/blob/main/Img/Simulator%20Screen%20Shot%20-%20iPod%20touch%20(7th%20generation)%20-%202022-01-25%20at%2011.03.03.png" width = 160 height = 240>


    ``` swift 
    struct ContentView: View {

        var body: some View {
            HStack {
                CardView()
                CardView()
                CardView()
            }
            .padding(.horizontal)
            .foregroundColor(.red)
        }
    }

    struct CardView: View {
        var body: some View {
            ZStack(content: {
                RoundedRectangle(cornerRadius: 20).stroke(lineWidth: 3)
                Text("🏗")
            })
        }
    }
    ```

3. 다크 모드 고려 카드에 배경색 지정

    <img src = "https://github.com/HwangWoonChun/SwiftUI-StanfordEdu/blob/main/Img/Simulator%20Screen%20Shot%20-%20iPod%20touch%20(7th%20generation)%20-%202022-01-25%20at%2011.04.44.png" width = 160 height = 240>
    
    ``` swift 
    struct CardView: View {
        var body: some View {
            ZStack(content: {
                RoundedRectangle(cornerRadius: 20).fill().foregroundColor(.white)
                RoundedRectangle(cornerRadius: 20).stroke(lineWidth: 3)
                Text("🏗").font(.largeTitle)
            })
        }
    }
    ```
    * 하나의 RoundRectangle를 이용해 처리를 하는것이 아니라 RoundRectangle을 두개 생성 하는 방식이다.

4. Face Up, Down 기능 개발하기 - @State

    ``` swift 
    struct CardView: View {
        @State var isFaceUp: Bool = false
        var body: some View {
            ZStack {
                let shape = RoundedRectangle(cornerRadius: 20)
                if isFaceUp {
                    shape.fill().foregroundColor(.white)
                    shape.stroke(lineWidth: 3)
                    Text("🏗").font(.largeTitle)
                } else {
                    shape.fill()
                }
            }
            .onTapGesture {
                isFaceUp = !isFaceUp
            }
        }
    }
    ```
    * 구조체는 기본적으로 self 가 immutable이다. SwiftUI 에선 이를 가변화 하기위해 @State 키워드를 사용한다.
    * A property wrapper type that can read and write a value managed by SwiftUI.
        * cf) wrapper Type : primitive type 의 데이터를 객체화 하기위한 포장 해주는 클래스
