The EvalDLL library provides methods to evaluate pre-trained CNTK models that are saved in the CNTK [model-v1 format](./CNTK-model-format). It is available in C++ (on Windows and Linux) and C# (on Windows only). 

* [EvalDLL evaluation on Windows](./EvalDLL-Evaluation-on-Windows)
* [EvalDLL evaluation on Linux](./EvalDLL-Evaluation-on-Linux)
* [EvalDLL evaluation in Azure](./Evaluate-a-model-in-an-Azure-WebApi)


## Evaluating different data types and layers
Currently the Eval library supports vectors for input and output. That means that the input vector must match the input nodes in the model (features). Some models are trained with images (e.g. CIFAR-10) however, these images are vectorized first then fed into the network. For example, the CIFAR-10 data set is composed of small images (32 pixels by 32 pixels) or RGB values. Although each is a 3 dimensional coordinate (width, height, color), the data is vectorized into a 1-dimensional vector. It is important thus, to convert the raw data to the vector format prior to evaluation. This conversion *should* be done in the same manner as when fed to the network for training.

Please refer to the [Evaluate Image Transforms](./CNTK-Evaluate-Image-Transforms) page for more information, particularly when dealing with images.

Although an already trained model has a specific set of output nodes, it is sometimes desirable to obtain the values of other nodes during evaluation (e.g. hidden layers). This is possible using the programmatic interface, please refer to the [Evaluate Hidden Layers](./CNTK-Evaluate-Hidden-Layers) page for more information.


## Current limitations
- Single threaded evaluation    
The CNTK evaluation library, and by extension the managed EvalWrapper library, are single threaded and single re-entrancy. That means that a single model can only be evaluated by a single thread at a time. However, it is possible to load multiple models in the same process and query each model using a single thread.
- Any program that links the pre-built evaluation libraries (EvalDLL.dll, EvalWrapper.dll in Windows, and libeval.so in Linux) of the CNTK binary package should use the same compiler version as that is used to build the pre-built libraries. 