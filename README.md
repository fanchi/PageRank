# PageRank
Given an initial page rank (weight) and transition matrix, it iteratively updates the page rank based on the previous page rank and transition matrix.  
#### Formula:  
$$PageRank_{n} = (1-\beta) * PageRank_{n-1} * TransitionMatrix + \beta * PageRank_{n-1}$$  
where beta is a teleporting factor to avoid dead ends (all page ranks become 0) or spider traps (page rank dominated by one page). It is implemented on Hadoop by two MapReduce jobs - unitMultiplication and unitSum.  
#### To run:
1. *Create directory for the transition matrix on HDFS*
`hdfs dfs -mkdir /transition`  
2. *Put the transition matrix (transition.txt) into the "transition" directory*
`hdfs dfs -put ./transition/transition.txt /transition`  
3. *Create directory for the initial page rank on HDFS*
`hdfs dfs -mkdir /pagerank0`  
4. *Put the initial page rank (pr.txt) into the "pagerank0" directory*
`hdfs dfs -put ./pr0/pr.txt /pagerank0`  
5. *Compile*
`hadoop com.sun.tools.javac.Main *.java`  
6. *Pack classes to jar*
`jar cf pr.jar *.class`  
7. *Run*
`hadoop jar pr.jar Driver /transition /pagerank /output 40 0.2  
//args0: dir of transition.txt  
//args1: dir of pagerank*.txt  
//args2: output dir of the first MapReduce job  
//args3: number of iterations  
//args4: beta
`