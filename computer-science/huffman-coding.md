# [Huffman Coding](https://en.wikipedia.org/wiki/Huffman_coding)

## Huffman Decoding

Huffman decoding is a way to take compressed data and turn it back into its original form. In order to do this, you need a special "map" called a Huffman tree. This is usually provided along with the compressed data. This tree tells you how to turn the compressed data back into the original data.

Here's a step-by-step process:

1. **Start at the Root of the Huffman Tree:** The root is the very top of the tree.

2. **Read a Bit:** Look at the first bit in the compressed data.

3. **Move in the Tree:** If the bit is 0, go to the left branch of the tree. If it's 1, go to the right.

4. **Found a Letter?** If you've landed on a leaf (a node with no more branches), you've found a letter (or other piece of data). Write down the letter.

5. **Repeat:** Go back to the top of the tree and repeat the process with the next bit in the compressed data. Do this until you've processed all the bits.

Here's an example:

Let's say we have the following Huffman tree:

```
        *(root)
       /      \
      *        *
    /   \     /  \
   A     B   C    D
```

The path from the root to each letter represents its Huffman code:
- A: 00
- B: 01
- C: 10
- D: 11

Now, let's decode the string "0001110110":

1. Start at the root. The first two digits are "00", which lead to 'A'. Write down 'A'.
2. Go back to the root. The next two digits are "01", which lead to 'B'. Write down 'B'.
3. Go back to the root. The next two digits are "11", which lead to 'D'. Write down 'D'.
4. Go back to the root. The next two digits are "01", which lead to 'B'. Write down 'B'.
5. Go back to the root. The final two digits are "10", which lead to 'C'. Write down 'C'.

So, the compressed string "0001110110" decodes to "ABDBC".

### Implementation

Sure, here's a basic implementation of Huffman decoding in Swift. For this example, let's say that we have a `Node` struct that represents a node in the Huffman tree, and a `HuffmanTree` struct that represents the entire tree.

```swift
class Node {
    var left: Node?
    var right: Node?
    var value: Character?

    init(left: Node? = nil, right: Node? = nil, value: Character? = nil) {
        self.left = left
        self.right = right
        self.value = value
    }
}

class HuffmanTree {
    var root: Node

    init(root: Node) {
        self.root = root
    }

    func decode(encodedData: String) -> String {
        var decodedData = ""
        var currentNode = root

        for bit in encodedData {
            if bit == "0" {
                if let left = currentNode.left {
                    currentNode = left
                }
            } else if bit == "1" {
                if let right = currentNode.right {
                    currentNode = right
                }
            }

            if let value = currentNode.value {
                decodedData.append(value)
                currentNode = root
            }
        }

        return decodedData
    }
}
```

To use this code, you would first create a `HuffmanTree` with the appropriate structure, then call the `decode` method with the encoded data:

```swift
let a = Node(value: "A")
let b = Node(value: "B")
let c = Node(value: "C")
let d = Node(value: "D")

let left = Node(left: a, right: b)
let right = Node(left: c, right: d)

let root = Node(left: left, right: right)
let huffmanTree = HuffmanTree(root: root)

let encodedData = "0001110110"
let decodedData = huffmanTree.decode(encodedData: encodedData)

print(decodedData) // Prints: "ABDBC"
```

In the real world, Huffman coding is widely used in applications that benefit from data compression. It's often used in computer networks to reduce the amount of data that needs to be transmitted. It's also used in file compression utilities, like the zip utility, to reduce the size of files. Huffman coding is used in multimedia formats as well. For example, JPEG image files and MP3 audio files both use Huffman coding as part of their compression algorithms.