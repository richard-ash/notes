# Convolution

## What is a convolution?

Convolution is a mathematical operation that is fundamental to many areas of both pure and applied mathematics, including but not limited to statistics, physics, computer science, electrical engineering, and signal processing.

In simple terms, convolution is a way of combining two functions to produce a third function. It 'blends' one function with another. It's used for things like smoothing, blurring, or detecting edges in image processing, or for manipulating sound in audio processing. 

Here is a simplified way to understand convolution:

Let's assume we have two signals: one is the input signal (let's call it f) and the other is a filter or kernel (let's call it g). Now, we want to modify the input signal using this filter. Here's what we do:

1. **Flip:** We start by flipping the filter g. This is done because the convolution is a measure of similarity, and flipping ensures we're always comparing the same parts of f and g.
2. **Shift:** We then shift this flipped filter g across the input signal f. At each point, g covers some part of f. 
3. **Multiply and Sum:** At each position, we multiply the overlapping parts of f and g, and sum up these multiplied values. 
4. **Output:** The result of these steps gives us a new signal that's a 'blended' version of f and g.

In the context of image processing, the input signal would be the pixel values of an image, and the filter could be something that blurs or sharpens the image. The convolution operation would then apply this filter to each part of the image, producing a new set of pixel values for a blurred or sharpened image.

In mathematical notation, convolution is often denoted by an asterisk (*), and is defined by an integral that expresses the amount of overlap of one function as it is shifted over another.

## Links

- [But what is a convolution? | 3Blue1Brown](https://www.youtube.com/watch?v=KuXjwB4LzSA&t=1s)