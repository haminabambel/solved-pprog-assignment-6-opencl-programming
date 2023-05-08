Download Link: https://assignmentchef.com/product/solved-pprog-assignment-6-opencl-programming
<br>
The purpose of this assignment is to familiarize yourself with OpenCL programming.

<hr>

Get the source code:

<pre><code class="sh language-sh">$ cd &lt;your_workplace&gt;$ wget https://nycu-sslab.github.io/PP-f21/HW6/HW6.zip$ unzip HW6.zip -d HW6</code></pre>

<h2 id="1imageconvolutionusingopencl">1. Image convolution using OpenCL</h2>

Convolution is a common operation in image processing. It is used for blurring, sharpening, embossing, edge detection, and more. The image convolution process is accomplished by doing a convolution between a small matrix (which is called a <em>filter kernel</em> in image processing) and an image. You may learn more about the convolution process at <a href="https://en.wikipedia.org/wiki/Convolution" target="_blank" rel="noopener">Wikipedia: Convolution</a>.

Figure 1 shows an illustration of the concept of applying a convolution filter to a specific pixel, value of which is <code>3</code>. After the convolution process, the value of the pixel becomes <code>7</code>—how the resulting value is computed is illustrated on the right of the figure.

<img decoding="async" alt="Convolution Demo" data-recalc-dims="1" data-src="https://i0.wp.com/user-images.githubusercontent.com/18013815/101978949-f7c9f900-3c93-11eb-8cc8-9b99db425b01.png?w=400&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/user-images.githubusercontent.com/18013815/101978949-f7c9f900-3c93-11eb-8cc8-9b99db425b01.png?w=400&amp;ssl=1" alt="Convolution Demo" data-recalc-dims="1">

 </noscript>

Figure 1. Applying a convolution filter to the dark gray pixel of the source image (value of which is <code>3</code>).

In this assignment, you will need to implement a GPU kernel function for convolution in OpenCL by using the zero-padding method. A serial implementation of convolution can be found in <code>serialConv()</code> in <code>serialConv.c</code>. You can refer to the implementation to port it to OpenCL. You may refer to <a href="https://www.geeksforgeeks.org/cnn-introduction-to-padding/" target="_blank" rel="noopener">this article</a> to learn about the zero-padding method. Figure 2 shows an example of applying the zero-padding method to the source image (on the left) and thereby resulting a same-size, filtered output image (on the right).

<img decoding="async" alt="Zero Padding Visualization" data-recalc-dims="1" data-src="https://i0.wp.com/miro.medium.com/max/1050/1*GwxhjA7-FLIRrtl__RkRgg.png?w=400&amp;ssl=1" class="lazyload" src="data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw==">

 <noscript>

  <img decoding="async" src="https://i0.wp.com/miro.medium.com/max/1050/1*GwxhjA7-FLIRrtl__RkRgg.png?w=400&amp;ssl=1" alt="Zero Padding Visualization" data-recalc-dims="1">

 </noscript>

Figure 2. Applying the zero-padding method to a source image.

Your job is to parallelize the computation of the convolution using OpenCL. A starter code that spawns OpenCL threads is provided in function <code>hostFE()</code>, which is located in <code>hostFE.c</code>. <code>hostFE()</code> is the host front-end function that allocates memories and launches a GPU kernel, called <code>convolution()</code>, which is located in <code>kernel.cl</code>.

Currently <code>hostFE()</code> and <code>convolution()</code> do not do any computation and return immediately. You should complete these two functions to accomplish this assignment.

You can build the program by typing <code>make</code>, and run the program via <code>./conv</code>. Your program should read an input image from <code>input.bmp</code>, perform image convolution, and output the result image into <code>output.bmp</code>.

You can use the following command to test your own image:

<pre><code>ffmpeg -i output.bmp(or your own image file) -pix_fmt gray -vf scale=600:400 destination.bmp</code></pre>

You can use a different filter kernel by adding option <code>-f N</code> when running the program (i.e., <code>./conv -f N</code>), where N is either 1 (by default), 2, or 3, and indicates which filter kernel is used. Each filter kernel is defined in a CSV file (<code>filter1.csv</code>, <code>filter2.csv</code>, or <code>filter3.csv</code>). The first line of the CSV file defines the width (or height) of the filter kernel, and the remaining lines define the values of the filter kernel.

<h2 id="2requirements">2. Requirements</h2>

You will modify only <code>hostFE.c</code> and <code>kernel.cl</code>.

<strong>Q1 (<em>5 points</em>)</strong>: Explain your implementation. How do you optimize the performance of convolution?

<strong>[Bonus] Q2 (<em>10 points</em>)</strong>: Rewrite the program using CUDA. (1) Explain your CUDA implementation, (2) plot a chart to show the performance difference between using OpenCL and CUDA, and (3) explain the result.

Answer the questions marked with <strong>Q1</strong> (and <strong>Q2</strong>) in a <strong>REPORT</strong> using <a href="https://hackmd.io/" target="_blank" rel="noopener">HackMD</a>. Notice that in this assignment a higher standard will be applied when grading the quality of your report.

<strong>Note: You cannot print any message in your program.</strong>