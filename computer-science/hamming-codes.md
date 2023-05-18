# [Hamming Codes](https://en.wikipedia.org/wiki/Hamming_code)

At its core, Hamming code is a way to make sure data has been transmitted correctly from one place to another. It does this by adding some extra bits to the data when it's sent. These extra bits are called "parity bits," and they help to check if any of the data bits have been changed during transmission.

A parity bit is a bit that is added to ensure that the number of bits with the value one in a set of bits (including the parity bit) is even or odd. They are used as the simplest form of error detecting code.

Here's a very simple explanation of how Hamming code works:

1. **Add Parity Bits:** When you want to send some data, you first add some extra "parity bits". You add these bits in specific places. For example, you might add them in the 1st position, the 2nd position, the 4th position, the 8th position, and so on.

2. **Calculate Parity Bits:** Next, you calculate what these parity bits should be. Each parity bit checks some of the other bits in the data, including other parity bits and some of the actual data bits. If the number of 1s in the bits it's checking is odd, you set the parity bit to 1. If it's even, you set it to 0. Which bits a parity bit checks depends on its position.

3. **Send the Data:** You then send the data (with the parity bits) to wherever it's going.

4. **Check the Parity Bits:** When the data is received, the receiver does the same parity calculations. They check each parity bit to see if the number of 1s is still odd or even, as it should be.

5. **Find Errors:** If a parity bit doesn't match what the receiver calculates, they know that there's been an error in that part of the data. By looking at which parity bits are wrong, they can even figure out which bit got changed and correct it.

Here's an example:

Let's say you want to send the data 1011.

1. Add parity bits at positions 1, 2, and 4 (for this example): P P 1 P 1 0 1 1 (P stands for parity bit).

2. Calculate the parity bits:
    - The 1st parity bit checks bits 1, 3, 5, 7: P 1 1 1 -> P = 0 (even number of 1s)
    - The 2nd parity bit checks bits 2, 3, 6, 7: P 1 0 1 -> P = 0 (even number of 1s)
    - The 3rd parity bit checks bits 4, 5, 6, 7: P 1 0 1 -> P = 1 (odd number of 1s)

3. So, the data you send is: 0 0 1 1 1 0 1 1.

When the receiver gets the data, they do the same calculations. If their calculated parity bits match the ones you sent, they know the data was transmitted correctly. If not, there was an error.

## How Parity Bits Enable Error Correction

When you receive data that was sent with parity bits, you check the data using the same system that was used to add the parity bits in the first place. You check all the same bits that each parity bit originally checked.

If all the parity bits you calculate match the ones that were sent, then everything is fine. But if one or more of them don't match, then an error occurred.

Here's the cool part: the position of the error is equal to the sum of the positions of the wrong parity bits. So, if parity bit 1 and parity bit 2 are wrong, then the error is in position 1 + 2 = 3. If parity bit 1 and parity bit 4 were wrong, the error would be in position 1 + 4 = 5. And so on.

So, by looking at which parity bits are wrong, you can figure out where the error occurred, and correct it. That's the magic of Hamming codes!
