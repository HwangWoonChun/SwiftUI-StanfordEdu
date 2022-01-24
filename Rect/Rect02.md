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
