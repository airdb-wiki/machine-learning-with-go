# 目录

## Table of Contents

## Preface 
[Page 18-30, 12]

	What this book covers
	What you need for this book
	Who this book is for
	Conventions
	Reader feedback
	Customer support
		Downloading the example code
		Downloading the color images of this book
		Errata
		Piracy
		Questions

## Chapter 01. Gathering and Organizing Data
[Page 31-69, 38]

	Handling data - Gopher style
	Best practices for gathering and organizing data with Go
	CSV files
		Reading in CSV data from a file
		Handling unexpected fields
		Handling unexpected types
		Manipulating
		CSV data with data frames
	JSON
		Parsing JSON
		JSON output
	SQL-like databases
		Connecting to an SQL database
		Querying the database
		Modifying the database
	Caching
		Caching data in memory
		Caching data locally on disk
		Data versioning
		Pachyderm jargon
		Deploying/installing Pachyderm
		Creating data repositories for data versioning
		Putting data into data repositories
		Getting data out of versioned data repositories
	References
	Summary


## Chapter 02. Matrices, Probability, and Statistics
[Page 70-105, 35]

	Matrices and vectors
		Vectors
		Vector operations
		Matrices
		Matrix operations
	Statistics
		Distributions
		Statistical measures
			Measures of central tendency
			Measures of spread or dispersion
		Visualizing distributions
			Histograms
			Box plots
		Probability
			Random variables
			Probability measures
			Independent and conditional probability
			Hypothesis testing
				Test statistics
				Calculating p-values
	References
	Summary


## Chapter 03. Evaluation and Validation
[Page 105-131, 26]

	Evaluation
		Continuous metrics
		Categorical metrics
			Individual evaluation metrics for categorical variablesConfusion matrices, AUC, and ROC
		Validation
			Training and test sets
			Holdout set
			Cross validation
	References
	Summary


## Chapter 04. Regression
[Page 132-165, 33]

	Understanding regression model jargon
	Linear regression
		Overview of linear regression
		Linear regression assumptions and pitfalls
		Linear regression example
			Profiling the data
			Choosing our independent variable
			Creating our training and test sets
			Training our model
			Evaluating the trained model
	Multiple linear regression
	Nonlinear and other types of regression
	References
	Summary


## Chapter 05. Classification
[Page 166-205, 39]

	Understanding classification model jargon
	Logistic regression
		Overview of logistic regression
		Logistic regression assumptions and pitfalls
		Logistic regression example
			Cleaning and profiling the data
			Creating our training and test sets
			Training and testing the logistic regression model
		k-nearest neighbors
			Overview of kNN
			kNN assumptions and pitfalls
			kNN example
		Decision trees and random forests
			Overview of decision trees and random forests
			Decision tree and random forest assumptions and pitfalls
			Decision tree example
			Random forest example
		Naive bayes
			Overview of naive bayes and its big assumption
			Naive bayes example
	References
	Summary


## Chapter 06. Clustering
[Page 206-234, 28]

	Understanding clustering model jargon
	Measuring Distance or Similarity
	Evaluating clustering techniques
		Internal clustering evaluation
		External clustering evaluation
	k-means clustering
		Overview of k-means clustering
		k-means assumptions and pitfalls
		k-means clustering example
			Profiling the data
			Generating clusters with k-means
			Evaluating the generated clusters
	Other clustering techniques
	References
	Summary


## Chapter 07. Time Series and Anomaly Detection
[Page 235-267, 32]

	Representing time series data in Go
	Understanding time series jargon
	Statistics related to time series
		Autocorrelation
		Partial autocorrelation
	Auto-regressive models for forecasting
		Auto-regressive model overview
		Auto-regressive model assumptions and pitfalls
		Auto-regressive model example
			Transforming to a stationary series
			Analyzing the ACF and choosing an AR order
			Fitting and evaluating an AR(2) model
	Auto-regressive moving averages and other time series models
	Anomaly detection
	References
	Summary


## Chapter 08. Neural Networks and Deep Learning
[Page 268-301, 33]

	Understanding neural net jargon
	Building a simple neural network
	Nodes in the network
		Network architecture
		Why do we expect this architecture to work?
		Training our neural network
	Utilizing the simple neural network
		Training the neural network on real data
		Evaluating the neural network
	Introducing deep learning
		What is a deep learning model?
			Deep learning with Go
			Setting up TensorFlow for use with Go
			Retrieving and calling a pretrained TensorFlow model
			Object detection using TensorFlow from Go
			References
	Summary


## Chapter 09. Deploying and Distributing Analyses and Models
[Page 302-341, 39]

	Running models reliably on remote machines
		A brief introduction to Docker and Docker jargon
		Docker-izing a machine learning application
			Docker-izing the model training and export
			Docker-izing model predictions
			Testing the Docker images locally
			Running the Docker images on remote machines
	Building a scalable and reproducible machine learning pipeline
		Setting up a Pachyderm and Kubernetes cluster
		Building a Pachyderm machine learning pipeline
			Creating and filling the input repositories
			Creating and running the processing stages
		Updating pipelines and examining provenance
		Scaling pipeline stages
	References
	Summary


## Chapter 10. Algorithms/Techniques Related to Machine Learning
[Page 342-351, 9]

	Gradient descent
	Entropy, information gain, and related methods
	Backpropagation

