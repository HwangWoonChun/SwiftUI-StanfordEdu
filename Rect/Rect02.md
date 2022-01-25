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

5.  외부에서 초기화 하도록 변경

    ``` swift 
    struct ContentView: View {

        var body: some View {
            HStack {
                CardView(content: 🦼)
                CardView(content: 🛴)
                CardView(content: 🚠)
                CardView(content: 🛰)
            }
            .padding(.horizontal)
            .foregroundColor(.red)
        }
    }

    struct CardView: View {
        var content: String
        @State var isFaceUp: Bool = false
        var body: some View {
            ZStack {
                let shape = RoundedRectangle(cornerRadius: 20)
                if isFaceUp {
                    shape.fill().foregroundColor(.white)
                    shape.stroke(lineWidth: 3)
                    Text(content).font(.largeTitle)
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
    
6.  for-Loop 이용 초기화 - forEach

    ``` swift 
    struct ContentView: View {
        let emjois = ["🛴", "🚠", "🚨"]
        var body: some View {
            HStack {
                ForEach(emjois, id: \.self, content: { item in
                    CardView(content: item)
                })
            }
            .padding(.horizontal)
            .foregroundColor(.red)
        }
    }
    ```
    
    * forEach 는 identifier 를 지정하여 특정 뷰들이 구분되어 질 수 있도록 해야한다.
    * \.self 는 데이터의 identfier 를 알아서 참조하도록 해준다.

7. 추가 삭제 기능

    <img src = "https://github.com/HwangWoonChun/SwiftUI-StanfordEdu/blob/main/Img/Simulator%20Screen%20Shot%20-%20iPod%20touch%20(7th%20generation)%20-%202022-01-25%20at%2013.59.15.png" width = 160 height = 240>

    ``` swift 
    struct ContentView: View {

        let emjois = ["🚗","🚕", "🚙", "🚌", "🚎", "🏎", "🚓", "🚑", "🚒", "🚐", "🛻", "🚚", "🚛", "🚜", "🦯", "🦽", "🦼", "🛴", "🚲", "🛵", "🏍", "🛺"]

        @State var emojiCount = 4

        var body: some View {
            VStack {
                HStack {
                    ForEach(emjois[0..<emojiCount], id: \.self, content: { item in
                        CardView(content: item)
                    })
                }
                Spacer()
                HStack {
                    add
                    Spacer()
                    remove
                }
                .padding(.horizontal)
            }
            .padding(.horizontal)
            .foregroundColor(.red)
        }

        var remove: some View {
            Button {
                if emojiCount > 1 {
                    emojiCount -= 1
                }
            } label: {
                VStack {
                    Image(systemName: "minus.circle")
                }
            }
        }

        var add: some View {
            Button {
                if emojiCount < emjois.count {
                    emojiCount += 1
                }
            } label: {
                VStack {
                    Image(systemName: "plus.circle")
                }
            }
        }
    }

    struct CardView: View {
        var content: String
        @State var isFaceUp: Bool = false
        var body: some View {
            ZStack {
                let shape = RoundedRectangle(cornerRadius: 20)
                if isFaceUp {
                    shape.fill().foregroundColor(.white)
                    shape.stroke(lineWidth: 3)
                    Text(content).font(.largeTitle)
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

8. Stroke vs Stroke Border
    * stroke - 보더를 뷰 밖에 그림
        * <img src = "https://github.com/HwangWoonChun/SwiftUI-StanfordEdu/blob/main/Img/Simulator%20Screen%20Shot%20-%20iPod%20touch%20(7th%20generation)%20-%202022-01-25%20at%2014.02.53.png" width = 160 height = 240>

    * stroke border - 보더를 뷰 안에 그림
        * <img src = "https://github.com/HwangWoonChun/SwiftUI-StanfordEdu/blob/main/Img/Simulator%20Screen%20Shot%20-%20iPod%20touch%20(7th%20generation)%20-%202022-01-25%20at%2014.02.37.png" width = 160 height = 240>

9. LazyVGrid 를 통해 격자 모형으로 리스트 구현

    * 3열만 보이기
        ``` swift 
        LazyVGrid(columns: [GridItem(), GridItem(), GridItem()]) { }
        ```
    * minimum 값 이상의 사이즈로 열마다 가능한 많이 아이템을 배치
        ``` swift 
        GridItem(.adaptive())
        ```
        
    * minimum 값 이상의 사이즈로 열마다 컬럼 수를 조절
        ``` swift 
        GridItem(.flexible())
        ```
            
    * 컬럼수와 크기 직접 조절
        ``` swift 
        GridItem(.fixed())
        ```
        
    * 예제

        * <img src = "https://github.com/HwangWoonChun/SwiftUI-StanfordEdu/blob/main/Img/Simulator%20Screen%20Shot%20-%20iPod%20touch%20(7th%20generation)%20-%202022-01-25%20at%2014.10.11.png"  width = 240 height = 160>
        
        * <img src = "https://github.com/HwangWoonChun/SwiftUI-StanfordEdu/blob/main/Img/Simulator%20Screen%20Shot%20-%20iPod%20touch%20(7th%20generation)%20-%202022-01-25%20at%2014.10.05.png"  width = 160 height = 240>

        ``` swift 
        struct ContentView: View {

            let emjois = ["🚗","🚕", "🚙", "🚌", "🚎", "🏎", "🚓", "🚑", "🚒", "🚐", "🛻", "🚚", "🚛", "🚜", "🦯", "🦽", "🦼", "🛴", "🚲", "🛵", "🏍", "🛺", "🚚", "🚛", "🚜", "🦯", "🦽", "🦼", "🛴", "🚲", "🛵", "🏍", "🛺"]

            @State var emojiCount = 20

            var body: some View {
                VStack {
                    ScrollView {
                        LazyVGrid(columns: [GridItem(.adaptive(minimum: 65))]) {
                            ForEach(emjois[0..<emojiCount], id: \.self, content: { item in
                                CardView(content: item).aspectRatio(2/3, contentMode: .fit)
                            })
                        }
                    }
                    .foregroundColor(.red)
                    Spacer()
                    HStack {
                        add
                        Spacer()
                        remove
                    }
                    .padding(.horizontal)
                }
                .padding(.horizontal)

            }

            var remove: some View {
                Button {
                    if emojiCount > 1 {
                        emojiCount -= 1
                    }
                } label: {
                    VStack {
                        Image(systemName: "minus.circle")
                    }
                }
            }

            var add: some View {
                Button {
                    if emojiCount < emjois.count {
                        emojiCount += 1
                    }
                } label: {
                    VStack {
                        Image(systemName: "plus.circle")
                    }
                }
            }
        }

        struct CardView: View {
            var content: String
            @State var isFaceUp: Bool = false
            var body: some View {
                ZStack {
                    let shape = RoundedRectangle(cornerRadius: 20)
                    if isFaceUp {
                        shape.fill().foregroundColor(.white)
                        shape.strokeBorder()
                        Text(content).font(.largeTitle)
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
