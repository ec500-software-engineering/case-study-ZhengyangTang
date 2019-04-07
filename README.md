# Case-Study:Tensorflow
## Technology and Platform used for development:
TensorFlow is an open source software library for numerical computation using data flow graphs. The graph nodes represent mathematical 
operations, while the graph edges represent the multidimensional data arrays (tensors) that flow between them. TensorFlow was developed 
by researchers and engineers working on the Google Brain team within Google's Machine Intelligence Research organization for the purposes 
of conducting machine learning and deep neural networks research. 

### 1. About language:
Tensorflow is built in C++ Programming language, but when developing applications, user can use both C++ and python. You can write some 
basic functions to add to the project in C++ if you want. However, the users are also encouraged to create their own Tensorflow language 
environment, like Go, Lua, Java, Javascript, or R. If the project was start today, my option for programming language would be python.
Python is popular, simple and clean, and really easy to comprehend, and it's the most widely used language for machine learning.

### 2. Building System and Building tools/environment
- Bazel is used to compile Tensorflow
- To use Tensorflow, User's need to install python(version 2.7 or above), pip/docker. The building details are as follows:

  - [Install TensorFlow with pip](https://www.tensorflow.org/install/pip)
  
  - [Install TensorFlow with Docker](https://www.tensorflow.org/install/docker)
  
- User's can also install GPU support (optional)

  - [GPU support](https://www.tensorflow.org/install/gpu)
  
- Windows, Linux/macOS, RaspBerry Pi are avaible for building from source

  - [Build from source (Linux/macOS)](https://www.tensorflow.org/install/source)
  
  - [Build from source (Windows)](https://www.tensorflow.org/install/source_windows)
  
  - [Build from source (Raspberry Pi)](https://www.tensorflow.org/install/source_rpi)
  
### 3. Framework/Libraries

#### Framework
Tensorflow uses graghs to represent assignments, and execute graghs in Sessions. The framework is based on python, which means it's simple 
and comprehensive, and it can be run on both CPU and GPU. It has high efficiency, and has good performance on visualization.

#### Libraries

Tensorflow itself is a library for machine learning and data analyzing. Tensorflow can be used in multiple scenerios, such as Natural 
language processing, image recognition, data processing and analyzing(classification, visualization, pattern recognition).

Here are some other extensions and libraries on tensorflow:
- [Libraries & extensions](https://www.tensorflow.org/resources/libraries-extensions)
These libraries are use for building more advanced and specific models, like machine learning in the field of creating art&music.

## Testing
Tensorflow uses two CI Platforms:
- Jenkins
- Some CI platform on google cloud
TensorFlow team members will be assigned to review pull requests. Once the pull requests are approved and pass continuous 
integration checks, a TensorFlow team member will apply ready to pull label to the change. 

![CI](https://github.com/ec500-software-engineering/case-study-ZhengyangTang/blob/master/case1.PNG?raw=true)

Linux, macOS, Windows, Raspberry Pi, Android are tested on their CI.

## Architecture
- Users are encouraged to add/edit functionality after they get familiar with the architecture. Users can apply tensorflow to their project as an external library, simply by pip install or other ways shown above.

- General architecture:
  - Client: Define the computation as a dataflow graph, and initiate graph execution using a session.
  - Distributed Master: Prune a specific subgraph from the graph, as defined by the arguments to Session.run(), do partitions on 
  the subgraph into multiple pieces that run in different processes and devices, distributes the graph pieces to worker services, and initiates graph piece execution by worker services.
  - Worker Services (one for each task): Schedule the execution of graph operations using kernel implementations appropriate to the available hardware (CPUs, GPUs, etc), and send and receive operation results to and from other worker services.
  - Kernel Implementations: Perform the computation for individual graph operations.
  
  ![layers](https://github.com/ec500-software-engineering/case-study-ZhengyangTang/blob/master/layers.png?raw=true)
  
- interaction of the components:
  - The client builds a graph that applies weights (w) to a feature vector (x), adds a bias term (b) and saves the result in a variable (s). "/job:worker/task:0" and "/job:ps/task:0" are both tasks with worker services. "PS" stands for "parameter server": a task responsible for storing and updating the model's parameters. Other tasks send updates to these parameters as they work on optimizing the parameters. The distributed master prunes the graph to obtain the subgraph required to evaluate the nodes requested by the client,
partitions the graph to obtain graph pieces for each participating device, and caches these pieces so that they may be re-used in subsequent steps. 
  
  ![architechture1](https://github.com/ec500-software-engineering/case-study-ZhengyangTang/blob/master/archi1.PNG?raw=true)

  - This is a example for partition. The distributed master seperate the parameters and inputs, put parameters together and put them to parameter server(PS). Since graph edges are cut by the partition, the distributed master inserts send and receive nodes to pass information between the distributed tasks. 
  
  ![architecture2](https://github.com/ec500-software-engineering/case-study-ZhengyangTang/blob/master/archi2.PNG?raw=true)

  - The distributed master then ships the graph pieces to the distributed tasks.
  
  ![architecture3](https://github.com/ec500-software-engineering/case-study-ZhengyangTang/blob/master/archi3.PNG?raw=true)
  
## Defects

- 1.[Issue #12071](https://github.com/tensorflow/tensorflow/issues/12071): In this issue, while using tf.gradient to calculate gradient
 on tf.norm(X) and X are zero values, the result is NAN. When X are extremely small numbers, like 1e-19, the calculation produces infinite. However, the correct result for both cases should be 1.
 
  - This is caused by square root in definition of tf.norm. While doing norm(X), you are actually doing sqrt(x^2). Gradient of sqrt approaches infinity, whereas gradient of x^2 approaches 0, so computing them separately then multiplying is a problem. i.e., When x is 0, the gradient of sqrt produces 1/0 problem, ended up in NAN, and when X is extremely small, gradient of sqrt approaches infinity. The solution would be to rewrite the automatic gradient function into a stable one:
  
```
@function.Defun(tf.float32, tf.float32)
def norm_grad(x, dy):
    return dy*(x/tf.norm(x))
@function.Defun(tf.float32, grad_func=norm_grad)
def norm(x):
    return tf.norm(x)
```
  
- 2. There is currently no Optimizer in the C++ API compared as the ones that we can find in the Python API, which means we have to do gradients calculation manully while using C++, and it's really frustrating, since retrieving the gradients and applying them is kind of hard and error prone. It would be great if an Optimizer + GradientDescentOptimizer can be developed in the C++ API.

## Demo
  
