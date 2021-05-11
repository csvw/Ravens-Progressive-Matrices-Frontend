# Raven's Progressive Matrices
### Rank 8 out of all submissions from 535 CS masters students.
Top ten submission for the final class project in CS 7637 at Georgia Tech.

## Problem Description

Raven's Progressive Matrices (RPM) is an intelligence test that has been the subject of much research within the artificial intelligence community. RPM consists of a series of visual reasoning problems. In each problem, the test taker is presented with an incomplete sequence of images and must select the answer that completes the sequence. An example problem is shown below:

![alt text](https://github.com/csvw/Ravens-Progressive-Matrices-Frontend/blob/main/Basic%20Problem%20D-07.PNG)

Developing cognitive agents that can solve RPM is an open research problem. In CS 7637, Knowledge-Based Artificial Intelligence: Cognitive Systems, students get to try their hand at building just such an agent. In a series of three projects over the course of the semester, students tackle increasingly difficult visual reasoning problems. By the end of the semester, students will have applied the methods and principles taught in class to design and develop a cognitive agent that can solve RPM problems.

## The Project

I have divided the project into three packages. The first package consists of the files provided by the course instructors. These files pass the problem images to the agent that I design and scrutinize the answers returned by my agent. The second package, core, consists of the central modules from which my agent is build. The third package, strategies, consists of a series of independent problem-solving strategies that my agent may choose from as it solves each problem.

The only libraries permitted in this project were numpy and pillow. We were not allowed to use any other third party image processing libraries. Because of this, much of the image processing had to be implemented manually.

### The Agent

My agent processes problems in a series of stages: image processing, problem analysis, strategy selection, and solution ranking.

#### Image Processing

My program is compute intensive. My agent begins each problem by running a shape extraction algorithm on every image in the problem and answer grids. In order to extract shapes, it must first convert the image to grayscale and then convert all pixels to either black or white (gray pixels are flipped either direction according to a threshold value). Then, it iterates over all pixels, extracts contiguous regions, and saves them as numpy arrays. In order to reduce compute time, my program shrinks the images down to reduce the number of pixels it must process.

#### Problem Analysis

After extracting all contiguous regions from each frame, my program proceeds by computing a series of statistics on each shape within those frames. Then, it computes a series of shape-to-shape relationships between the shapes in neighboring frames along the rows and columns of the grid. It then passes all this information to the part of my program that handles strategy selection.

#### Strategy Selection

In order to make the agent extensible and flexible, I used a method called strategy selection and integration. In this framework, the agent is given a repository of solution strategies that it may apply to any given problem. In order to select appropriate strategies, the agent is supplied with a test for every strategy in the repository. If a given problem passes the test associated with a particular strategy, then that strategy is selected as a possible solution for the problem.

A wide variety of strategies are available to my agent, and due to its extensible design, more can be added as needed. It currently can determine whether shapes are being added or removed between successive frames, whether shapes are being scaled or translated, whether certain logical patterns are present in the images, and whether certain relationships within the frames are being shifted to the right or left in each successive row or column.

#### Solution Ranking

Each strategy comes with a test to determine whether it is applicable to the problem at hand. In addition to this, each strategy also comes with two more functions: a function for identifying possible solutions, and a function for ranking the quality of its proposed solutions. This second function computes a number called the coherence score. The coherence score reflects the agent's confidence that the current strategy would select a particular answer.

For each problem, the agent uses the strategy tests to collect two separate pools of possible solution strategies: one for the rows of the problem grid, and one for the columns. It then iterates over each possible pair of solution strategies and uses the answer tests to collect the candidate solutions that each pair would accept as a possible answer. Finally, it computes a coherence score for each possible solution, and selects the candidate with the highest score.

### Problem Set Performance
(Note: The set results from the local problem set are different from the hidden problem set that the instructors used for grading. My performance on the problem set used for local testing are shown in SetResults.csv. The results below reflect my performance on the hidden problem set that was used to rank student performance.)

Basic Problems D: 12/12

Basic Problems E: 12/12

Test Problems D: 8/12

Test Problems E: 10/12

Challenge Problems D: 5/12

Challenge Problems E: 4/12

Ravens Problems D: 8/12

Ravens Problems E: 7/12

Note: This repository provides documentation for the project. The code is in a private repository. Georgia Tech asks their alumni not to share project code publicly. For those who are interested, I can provide a zip file containing the project code.

