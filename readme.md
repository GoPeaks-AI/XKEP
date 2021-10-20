# <center>Expert Knowledge Exchange Platform</center> 
#### <center>Victor Zitian Chen</center>
The **<font color='red'>eXpert Knowledge Exchange Platform (XKEP)</font>** is an interface that connects knowledge **Teachers** and knowledge **Learners** with a cumulative knowledgebase, including both Expert Knowledge and empirical evidence.User will interact with **XKEP** through Python Jupyter Notebook by identifying him/herself as a **Knowledge Teacher** or **Knowledge Learner** first, then add, modify, and query **knowledge** from the **Knowledgebase**.

![XKEP](https://user-images.githubusercontent.com/89408945/138008436-d4b40442-f38e-425b-bb38-af77e28e263d.jpg)

Specifically, it has six classes (objectives), as illustrated in Figure above.

## <center>1.	Knowledgebase </center>
Knowledgebase is a container to host Knowledge (including nodes, links, and their properties).
It is connected with neo4j AuraDB API services to access cloud space and knowledge graph data.
The user will be asked to provide a user ID to connect to the API services.

![neo4j-aura-graph](https://dist.neo4j.com/wp-content/uploads/20191105083257/neo4j-aura-graph.jpg)

Functions:

### a. Summary
Return the total counts of knowledge

### b. Structure
Return the taxonomic structure underlying the concepts in the **Knowledgebase**, and counts

### c. Whole
Return all knowledge as a whole from the **Knowledgebase**


```python
# Object 1 - KnowledgeBase

class Knowledgebase():

    """
    Knowledgebase is a container to host Knowledge (including nodes, links, and their properties).
    It is connected with neo4j AuraDB API services to access cloud space and knowledge graph data.
    The user will be asked to provide a user ID to connect to the API services.
    """

## <center>2.	Expert Knowledge</center>
Knowledge is the basic unit inside the Knowledgebase. 
Each unit of Knowledge has three components: two nodes and one link. 
Each node is a real-world concept that belongs to the taxonomy of the entire Knowledgebase.
Each link is a predictive relationship. Node1 is a predictor of Node2.

![Knowledge.jpg](https://miro.medium.com/max/888/1*MPtzE8lfYXfeJ-Axv5Si_w.png)

Functions:

### a.	Summary
Return a summary table of counts by relationships.

### b.	Report
Return a full table of knowledge details, including labels of variables and the knowledge context, and the source.

### c.	Knowledge Teacher Information
Return a list of names of the knowledge creator team members.

## <center>3.	Node</center>
The purpose of a Node is to represent an entity of logic concept.
Each node's labels are pre-assigned based on an expert taxonomy below following Zhong, Sandoval, Chen, Woehr, Long, and Tonidandel (2021)'s working paper.

![taxonomy](https://user-images.githubusercontent.com/89408945/138008635-7ce5e007-6ff4-4836-9397-c833537826af.jpg)

Functions:

### a.	Name
Return all possible names for this concept.

### b. Measure
Return all possible measures for this concept.

### b.	Taxonomy
Return the full taxonomy of labels and measures of this concept.

## <center>4.	Link</center>
A link is a subunit of Knowledge.

It specifies a predictive relationship between two Nodes. 
Unless otherwise specified, Node1 predicts Node2.

Functions:

### a.	Direction
Positive, negative, nonlinear, or unclear relationship between two Nodes

### b.	Total sample size
Total number of observations for drawing the assertions.

### c.	Sample Industries

### d. Sample Countries

## <center>5.	Knowledge Teachers </center>
This class allows a user to create new Knowledge and upload it into the Knowledgebase through API services. 
User will be asked to provide the user ID to connect.

![expand-player-node](https://mk0sharpnotionswseoa.kinstacdn.com/wp-content/uploads/expand-player-node.gif)

Function:

### a.	Review
Review new **Expert Knowledge**


## <center>6.	Knowledge Learner </center>
This is to confirm a user is a Learner, and record his or her intention of using the Knowledgebase.

Function:

### a.	Purpose
Research question underlying a query request by the **Knowledge Learner**

