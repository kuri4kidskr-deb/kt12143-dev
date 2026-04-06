import SwiftUI

struct ContentView: View {
    @State private var tiles = [1,2,3,4,5,6,7,8,0]

    let columns = [
        GridItem(.flexible()),
        GridItem(.flexible()),
        GridItem(.flexible())
    ]

    var body: some View {
        VStack(spacing: 20) {
            Text("スライドパズル")
                .font(.largeTitle)
                .bold()

            LazyVGrid(columns: columns, spacing: 10) {
                ForEach(0..<9, id: \.self) { index in
                    let value = tiles[index]

                    ZStack {
                        Rectangle()
                            .foregroundColor(value == 0 ? .gray.opacity(0.3) : .blue)
                            .cornerRadius(8)

                        if value != 0 {
                            Text("\(value)")
                                .font(.largeTitle)
                                .foregroundColor(.white)
                        }
                    }
                    .frame(width: 100, height: 100)
                    .onTapGesture {
                        moveTile(at: index)
                    }
                }
            }

            Button("リセット") {
                tiles.shuffle()
            }
            .font(.title2)
            .padding()
        }
        .padding()
    }

    func moveTile(at index: Int) {
        let emptyIndex = tiles.firstIndex(of: 0)!

        let validMoves = [
            emptyIndex - 1, emptyIndex + 1,
            emptyIndex - 3, emptyIndex + 3
        ]

        if validMoves.contains(index) {
            tiles.swapAt(index, emptyIndex)
        }
    }
}# kt12143-dev

