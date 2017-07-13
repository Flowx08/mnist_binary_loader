MNIST loader
=================
This is a simple loader for the MNIST dataset written in C++
To use it you have to include mnist_binary_loader.hpp:

```cpp
#include "mnist_binary_loader.hpp"
```
Then to load the dataset simply call the mnist_binary_loader class constructor and pass as
arguments the paths of the training images, testing images and the paths of the labels:

```cpp
mnist_binary_loader mnist("../../mnist_binary/train-images-idx3-ubyte",
						"../../mnist_binary/t10k-images-idx3-ubyte",
						"../../mnist_binary/train-labels-idx1-ubyte",
					    "../../mnist_binary/t10k-labels-idx1-ubyte");
```
You can then access to all the data using this four functions:
```cpp
mnist.get_train_images();
mnist.get_test_images();
mnist.get_train_labels();
mnist.get_test_labels();
```
Example
====================
This example code load the mnist dataset and print 10 random digits in the console:

```cpp
#include "mnist_binary_loader.hpp"
#include <stdio.h>
#include <stdlib.h>

int main(int argc, const char *argv[])
{
	
	mnist_binary_loader mnist("../../mnist_binary/train-images-idx3-ubyte",
								"../../mnist_binary/t10k-images-idx3-ubyte",
								"../../mnist_binary/train-labels-idx1-ubyte",
								"../../mnist_binary/t10k-labels-idx1-ubyte");

	//print out 10 random images
	for (int i = 0; i < 10; i++) {
		const int image_id = rand() % mnist.get_train_images().size();
		printf("Label: %d\n", (int)mnist.get_train_labels()[image_id]);
		for (int y = 0; y < 28; y++) {
			for (int x = 0; x < 28; x++) {
				if (mnist.get_train_images()[image_id][y * 28 + x] > 125) printf("#");
				else printf(" ");
			}
			printf("\n");
		}
	}

	return 0;
}
```
