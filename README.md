Minimal Bag of Visual Words Image Classifier
============================================

Implementation of a content based image classifier using the [bag of visual words model][1] in Python. 

This code relies on:

 - SIFT features for local features
 - k-means for generation of the words via clustering
 - SVM as classifier using the LIBSVM library

### Example use:
  
You train the classifier for a specific dataset with: 

    python learn.py -d path_to_folders_with_images

To classify images use:

    python classify.py -c path_to_folders_with_images/codebook.file -m path_to_folders_with_images/trainingdata.svm.model -d path_to_folders_with_images_nested_structure

The dataset (both for the learn.py and the classify.py scripts) should have following structure, where all the images belonging to one class are in the same folder:

    .
    |-- path_to_folders_with_images
    |    |-- class1
    |    |-- class2
    |    |-- class3
    ...
    |    └-- classN

NOTE: The exact distribution used for the anaysis on the plantvillage dataset is available at : https://github.com/salathegroup/plantvillage_deeplearning_paper_dataset/tree/master/data_distribution_for_SVM

### Prerequisites:

To install the necessary libraries run following code from working directory:

    # installing libsvm
    wget -O libsvm.tar.gz http://www.csie.ntu.edu.tw/~cjlin/cgi-bin/libsvm.cgi?+http://www.csie.ntu.edu.tw/~cjlin/libsvm+tar.gz
    tar -xzf libsvm.tar.gz
    mkdir libsvm
    cp -r libsvm-*/* libsvm/
    rm -r libsvm-*/
    cd libsvm
    make
    cp tools/grid.py ../grid.py
    cd ..
    
    # installing sift
    wget http://www.cs.ubc.ca/~lowe/keypoints/siftDemoV4.zip
    unzip siftDemoV4.zip
    cp sift*/sift sift
    

#### Notes
If you get an `IOError: SIFT executable not found` error, try `sudo apt-get install libc6-i386`. `sift` is a 32Bit executable and you need to install additional libraries to make it run on 64Bit systems. [More info and background on the misleading error message on unix.stackexchange](http://unix.stackexchange.com/a/13409/11381)
    
### References:

#### Libsvm:

Chih-Chung Chang and Chih-Jen Lin, LIBSVM : a library for support vector machines. ACM Transactions on Intelligent Systems and Technology, 2:27:1--27:27, 2011. Software available at http://www.csie.ntu.edu.tw/~cjlin/libsvm

#### SIFT:
David G. Lowe, "Distinctive image features from scale-invariant keypoints," International Journal of Computer Vision, 60, 2 (2004), pp. 91-110.

#### sift.py:
Taken from http://www.janeriksolem.net/2009/02/sift-python-implementation.html

#### libsvm.py:
Addapted from easy.py contained in the LIBSVM packet by Chih-Chung Chang and Chih-Jen Lin.

[1]: https://en.wikipedia.org/wiki/Bag-of-words_model_in_computer_vision
[2]: http://www.vision.caltech.edu/Image_Datasets/Caltech101/
[3]: https://github.com/shackenberg/Minimal-Bag-of-Visual-Words-Image-Classifier/blob/master/learn.py
[4]: https://github.com/shackenberg/Minimal-Bag-of-Visual-Words-Image-Classifier/blob/master/classify.py
