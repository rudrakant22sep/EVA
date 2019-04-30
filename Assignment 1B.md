# EVA
Wednesday W6 Batch


*****************************************************************
QUESTION # 1: What are Channels and Kernels (according to EVA)?

*****************************************************************
Answer: CHANNEL:
	- An input image when broken down into individual features and characteristics. Many of these features and characteristics could be similar ones which can be blubbed or bundled together. This one set of features that can be clubbed or containerized together is called a CHANNEL
	- Ex.: An image seen in a book is comprised of different colurs and shades. And all these colours are made out of varied intensity and dilution of 3 basic clours - Red, Green and Blue. If we can uniquely create 3 pages and each page comprises of only 1 colour of varied intensity throughout the page, and when all these 3 colurs are superimposed on top of each other; IF AT THIS POINT; orginal image can be recreated, then, each of 3 pages of Red, Green and Blue coloured pages together form a CHANNEL.
	
	KERNEL:
	- In the above example, each of the Red, Blue, Green paper is called a Kernel Or Feature Extractor
	- A Kernel's objective is to exctract similar features out of an input image
	- A Kernel can additionally be called as a 3*3 matrix
	- Mathematically, result of a kernel operation (also called COnvolution) over an input image is the Sum of multiplcation of all elements of the input image which the Kernel can see

-	Hence, Combination of all similar kind of Feature Extractor will form a Channel.

-	Now, lets assume an input image I1 (say a 7*7 pixeled image) underwent Convolution using a kernel K1, K2 and K3 (each of size 3*3), then, 
	I1 --> K1 --> will result in a new layer, say L1
	This L1 will be a new channel of size 5*5
	L1 --> K2 --> will result in a 2nd new layer, say L2
	This L2 will be a new Channel of size 3*3
	L2 --> K3 --> will result in a 3rd new layer, say L3
	This L3 will also be a new channel, of size 1*1



*****************************************************************
QUESTION # 2: Why should we only (well mostly) use 3x3 Kernels?

*****************************************************************
ANSWER:
	- A general preference before choosing a kernel is to:-
		- have an odd-sized square matrix kernel, as it helps finds the mirror-point to assist in symmetry of left vs. right half of the filter
		- should be of optimal size, so that we don't put lot of parameters causing computational troubles
	- a 3*3 kernel helps in both the ways. 
		- While being an odd-sized square matrix, it uniquely helps identify the mirror-point which helps kernel creators design kernels for efficient feature extraction
		- a size of 3*3 causes multiple iterations of convolution to be run. However, this has an upside when compared against larger sized kernels, say a 5*5 or a 7*7 kernel
		- for an input image of 7*7:-
			- a 7*7 kernel will be needed only once. so it processes 49*1 parameters = 49
			- a 5*5 kernel will be needed twice. So, it will process 25*2 parameters = 50
			- a 3*3 kernel will be needed thrice. So, it will process 9*3 parameters = 27

		- as can be seen, using a 3*3 kernel also helps us achieve same results as would be fetched using a 5*5, 7*7 or 9*9 etc. sized kernels.
		- However, a 3*3 kernel achieves the same result using much lesser parameters thus making less GPU utilization and eventually, faster computation.
	- realizing the benefits of using 3*3 kernels, a lot of Image-processing GPUs today are fine-tuned for optimal performance for the usage of 3*3 kernels.
	- it's a highly optimized kernel kernel of the years and is mostly used for the feature extraction purposes
	- 

**********************************************************************************************************************************
QUESTION # 3: How many times do we need to perform 3x3 convolution operation to reach 1x1 from 199x199 (show calculations)
**********************************************************************************************************************************
ANSWER:
	Assumptions:-
		padding	= 0
		Stride	= 1
		input size = n*n matrix
		filter size= f*f matrix
		No. of elements in the next layer = ((n + p - f)/s + 1)
For an i/p image of 199*199, below will be the calculations:
		A pipe ( | ) shall denote 1 count of convolution using filter f of size 3*3

	199 | 197 | 195 | 193 | 191 | 189
	so,
		after 1st 5 convolutions, we decreased the resolution by 10 = 189
		after 2nd 5 convolutions, we decreased the resolution by 10 = 179
		after 3rd 5 convolutions, we decreased the resolution by 10 = 169
		after 4th 5 convolutions, we decreased the resolution by 10 = 159
		after 5th 5 convolutions, we decreased the resolution by 10 = 149
		after 5th 5 convolutions, we decreased the resolution by 10 = 139
		after 7th 5 convolutions, we decreased the resolution by 10 = 129
		after 8th 5 convolutions, we decreased the resolution by 10 = 119
		after 9th 5 convolutions, we decreased the resolution by 10 = 109
		after 10th 5 convolutions, we decreased the resolution by 10 = 99
		after 11th 5 convolutions, we decreased the resolution by 10 = 89
		after 12th 5 convolutions, we decreased the resolution by 10 = 79
		after 13th 5 convolutions, we decreased the resolution by 10 = 69
		after 14th 5 convolutions, we decreased the resolution by 10 = 59
		after 15th 5 convolutions, we decreased the resolution by 10 = 49
		after 16th 5 convolutions, we decreased the resolution by 10 = 39
		after 17th 5 convolutions, we decreased the resolution by 10 = 29
		after 18th 5 convolutions, we decreased the resolution by 10 = 19
		after 19th 5 convolutions, we decreased the resolution by 10 = 9

	so after 19*5 = 95 convolutions, resulting size is 9*9
	9 | 7 | 5 | 3 | 1 ==> 4 more times.
	
	==> Hence a total of 99 times the convolution was needed for an i/p image of 199*199 to be done using 3*3 filter.
	

