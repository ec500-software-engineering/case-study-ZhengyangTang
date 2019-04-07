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
