# docs
## 20200817 SwiftUI の List の複数項目の移動操作が macOS 上で適切に動作しない

SwiftUI を利用して macOS アプリの UI を作成している．
List で表示された複数の項目の移動(並べ替え)操作が期待通りに動作しない．
移動する項目が1つの場合は問題ないが，2つ以上の項目を選択し移動させる操作をしても選択した項目が移動しない．
サンプルコードは以下の通り:

```Swift
import SwiftUI

struct SwiftUIView: View {
    @State var items: [String] = (0...10).map(String.init)
    @State var selected = Set<String>()

    var body: some View {
        List (selection: $selected){
            ForEach(items, id: \.self) { item in
                Text(item)
            }
            .onMove { (indexSet, index) in
                self.items.move(fromOffsets: indexSet, toOffset: index)
            }
        }
    }
}

struct SwiftUIView_Previews: PreviewProvider {
    static var previews: some View {
        SwiftUIView()
    }
}
```

ネットを検索してみたら，同様の問題にハマっている人を発見: [macOS - Moving multiple rows in SwiftUI List](https://stackoverflow.com/questions/60328520/macos-moving-multiple-rows-in-swiftui-list)
解決していない様子．
これはバグなのか？バグレポートすべきなのか悩む．

