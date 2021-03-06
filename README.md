## Facial-Recognition-with-Deep-Nueral-Networks

![screen shot 2017-04-17 at 3 24 41 pm](https://user-images.githubusercontent.com/12654784/35335115-8f50c5a8-013a-11e8-8650-5ee8ae4a17a0.png)

This demo does the full face recognition pipeline on every frame. In practice, object tracking like dlib's should be used once the face recognizer has predicted a face.

In the edge case when a single person is trained, the classifier has no knowledge of other people and labels anybody with the name of the trained person.

The web demo does not predict unknown users and the saved faces are only available for the browser session. If you're interested in predicting unknown people, one idea is to use a probabilistic classifier to predict confidence scores and then call the prediction unknown if the confidence is too low.

## Setup with Docker

This repo can be used as a container with Docker for CPU mode. Depending on your Docker configuration, you may need to run the docker commands as root.

Automated Docker Build
The quickest way to getting started is to use our pre-built automated Docker build, which is available from bamos/openface. This does not require or use a locally checked out copy of OpenFace. To use on your images, share a directory between your host and the Docker container.

```
> docker pull bamos/openface
> docker run -p 9000:9000 -p 8000:8000 -t -i bamos/openface /bin/bash
> cd /root/openface
> ./demos/compare.py images/examples/{lennon*,clapton*}
> ./demos/classifier.py infer models/openface/celeb-classifier.nn4.small2.v1.pkl ./images/examples/carell.jpg
> ./demos/web/start-servers.sh
```

Building a Docker Container
This builds a Docker container from a locally checked out copy of OpenFace, which will take about 2 hours on a modern machine. Be sure you have checked out the git submodules. Run the following commands from the openface directory.

```
> docker build -t openface .
> docker run -p 9000:9000 -p 8000:8000 -t -i openface /bin/bash
> cd /root/openface
> ./run-tests.sh
> ./demos/compare.py images/examples/{lennon*,clapton*}
> ./demos/classifier.py infer models/openface/celeb-classifier.nn4.small2.v1.pkl ./images/examples/carell.jpg
> ./demos/web/start-servers.sh
```

## Prerequisites

Be sure you have checked out the submodules and downloaded the models as described above.

1. This project uses python2 because of the opencv and dlib dependencies. Install the packages the Dockerfile uses with your package manager. With pip2, install numpy, pandas, scipy, scikit-learn, and scikit-image.
1.Python2.7 
  i.)  pip2
  ii.) numpy
  iii.)pandas
  iv.) matplotlib
2. OpenCV dependencies 
3. Dlib Dependencies
4. Docker
5. scikit-learn
6. scipy
7. scikit-image

8.Torch
Install Torch from the instructions on their website. At this point, the command-line program th should be available in your shell. Install the dependencies with luarocks install $NAME, where $NAME is as listed below.

* dpnn
* nn
* optim
* csvigo
* cutorch and cunn (only with CUDA)
* fblualib (only for training a DNN)
* tds (only for training a DNN)
* torchx (only for training a DNN)
* optnet (optional, only for training a DNN)

These can all be installed with:
```
**for** NAME **in** dpnn nn optim optnet csvigo cutorch cunn fblualib torchx tds; **do** luarocks install $NAME; **done**
```
