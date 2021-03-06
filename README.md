# toolkitCpp

This is intented to provide the base for the machine learning kit.  It parses
ARFF files and provides evaluation methods.  A DummyLearner is provided that
will classify each instance as the majority class.  You can use that class as
example to create new learning algorithms.

## Build Instructions for Linux:
1. Clone the repo

   ```git clone https://github.com/cs478ta/toolkitCpp.git```
2. Install g++ and make. (These packages may already be installed)
   
   ```sudo aptitude install g++ make```
3. You may also wish to install a debugger
   
   ```sudo aptitude install kdevelop```
4. Now build it. If you want to build with debug symbols, do ```make dbg```

   If you want to build optimized binaries, do ```make opt```
5. To run it, go into the bin folder
       cd ../bin
       and follow the usage instructions

To test the toolkit, navigate to the project root directory and run:
```
mkdir datasets
cd datasets/
wget http://axon.cs.byu.edu/~martinez/classes/478/stuff/iris.arff
cd ..
./bin/MLSystemManager -L baseline -A datasets/iris.arff -E training
```

## Build Instructions for Windows:
1. Download and install Microsoft Visual Studio 2008 Express Edition
	   (It may work with other versions, but I have not tested it.)
2. Make sure that you have an up-to-date Platform SDK. If you don't
	   know what this means, just cross your fingers and proceed. If
	   it fails to build, then you'd better learn about the Platform SDK.
3. Open Visual Studio.
4. File &rarr; Open Solution
5. Open the file MLSystemManager.sln
6. Set the configuration. Use "Debug" if you want debug symbols, and
	   use "Release" if you want optimized binaries.
7. Build it. (Press F7)

## Usage Instructions:
	MLSystemManager -L [learningAlgorithm] -A [ARFF_File] -E [EvaluationMethod] {[ExtraParamters]}-N {-R [seed]}
        (Note that 3 of the evaluation methods require at least one extra parameter)
	You can also additionally supply the following optional parameters:
	-N          Wrap the learning algorithm in a normalization filter.
	-D          Wrap the learning algorithm in a discretization filter.
	-C          Wrap the learning algorithm in a nominal-to-categorical filter.
	            (It is common to use both -N and -C together. You will do this in
		    the perceptron/neural net lab. The -D filter is useful for the
		    naive Bayes lab.)
	-R [seed]   Specify a seed for the random number generator. (It is a lot easier
	            to debug problems when the algorithm behaves deterministically, so
		    I recommend always specifying a seed.)

	Possible evaluation methods are:
	- Training (using same data set for training and testing)
		MLSystemManager -L [learningAlgorithm] -A [ARFF_File] -E training
	- Static Split (2 distinct datasets/ARFF files; one for training and one for testing
		MLSystemManager -L [learningAlgorithm] -A [ARFF_File] -E static [TestARFF_File]
	- Random Split (1 dataset is split randomly providing x% for training and the rest for testing)
		MLSystemManager -L [learningAlgorithm] -A [ARFF_File] -E random [PercentageForTesting]
	- N-fold Cross-validation (1 dataset is partitioned into N partitions.  The learning algorithm is
	  evaluated on each partion and then the average accuracy is returned.
		MLSystemManager -L [learningAlgorithm] -A [ARFF_File] -E cross [numOfFolds]

### Remarks about the code:
This code is provided to help you learn, not to help you avoid
learning. Hence, you are responsible to become familiar with this
code, not merely to use it blindly. You may opt not to use it. It
is really okay to implement it all yourself from scratch. (That
is how we used to do it, and you just might learn more that way.)
This toolkit should not constrain you. You should plan to modify
it. If you encounter difficulty understanding this code, the TA
can walk you through it. If there are bugs, then you are
responsible to fix them. So "the toolkit is confusing and buggy"
is not a valid excuse for lateness.
