# The QA processes

Explained in the most straight-forward manner, the role of a QA is answering these two questions: **Are we building the right product? Are we building the product right?** To answer these questions, we have to take a look at the software testing life cycle that we apply on all projects:


## Requirement and specification analysis

Analyzing the provided documents/specifications to learn the features to be implemented. This involves a sprint planning discussion and a breakdown of the features.
> Get to know the product.

## Test planning

Deciding what testing types will be used. Deciding what to automate & what not. Deciding the tools and resources that will be used in the given timeframe. In this phase we look over past issues and features to plan out a regression test suite. 
> Plan ahead

## Environment setup and test case development 

Setting up testing environment can mean: making sure that an actual testing environment of the application is ready, setting up a test case platform ( manual / automation or both ), setting up a CI if needed. The main activity of this phase is developing the tests.
> Getting ready

## Test execution

Run the tests and analyze the test results. Decide what is an error and what is a failure. Confirm and close tickets based on the results.
> Make it or break it

## Test maintenance & Test cycle closure

This phase involves refactoring the test cases, finishing up all tickets and making sure that the release criterias are met. 
> Release
