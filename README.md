# Decision Trees (Prediction with CART)

## Project Objective:

For this project, data from the Assistments Intelligent Tutoring system will be used. This system gives students hints based on how they perform on math problems. We want to see if we can build a decision tree to help teachers decide which students to follow up with, based on students' performance in Assistments. We will create three groups ("teacher should intervene", "teacher should monitor student progress" and "no action") based on students' previous use of the system and how many hints they use. To do this we will be building a decision tree using the "party" package. The party package builds decision trees based on a set of statistical stopping rules.

## Datasets:

  * intelligent_tutor.csv
  * intelligent_tutor_new.csv

### Codebook:

id - student id
prior_prob_count - The number of problems a student has done in the system prior to the surrent session  
score - The score the student achieved in the current session  
hints - The number of hints the student requested in the current session  
hint.y - Whether or not the student asked for hints in the current session  
complete - Whether or not the student completed the cirrent session  
action - The action suggested by the system to a teacher about a given student based on their performance

## Results:

### Decision Trees:

#### Classification Tree:

```
c.tree <- rpart(action ~ hint.y + complete, method="class", data=D1)
```

![tree1](https://github.com/lizarova777/assignment5/blob/master/tree-1.png)

#### Regression Tree:

```
score_ctree <- ctree(factor(advice) ~ prior_prob_count + prior_percent_correct + hints, D1)
```

![tree2](https://github.com/lizarova777/assignment5/blob/master/Score_Tree.png)

The tree with the training data shows that the first behavior that the teacher should pay close attention to the when the student is requesting at most 12 hints and answered less than 63% of problems correctly before the current session, and scored less than 81%. The second behavior is when a student asked for more than 12 hints and still scored less than 81%. In particular, for node 7, 60% of the students are classified into "monitor" group and 30% of the students are placed into "intervene" group. Likewise, for node 9, 60% of the students are classified into "monitor" group and 40% of the students are placed into "intervene" group. 

When compared with the test data, for the observed results, it is supposed to say "no action" for all students since this dataset represents those students that scored higher than 80%, which is indicated by their score of 1. The model predicted the advice correctly 58% of the time. However, the error rate of the model is 42% percent since 42% of the time, the predicted advice was "monitor". This suggests that this regression tree is not overfitted. In other words, it is generalizable.  



