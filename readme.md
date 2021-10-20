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

# Load Knowledge Graph from Neo4j AuraDB

# !pip install --upgrade py2neo
# !pip install --upgrade neo4j
# !pip install neo4jupyter

from py2neo import Graph,Node,Relationship
from neo4j.exceptions import ServiceUnavailable
import neo4jupyter
neo4jupyter.init_notebook_mode()
import pandas as pd

class Knowledgebase():
    
    """
    Knowledgebase is a container to host Knowledge (including nodes, links, and their properties).
    It is connected with neo4j AuraDB API services to access cloud space and knowledge graph data.
    The user will be asked to provide a user ID to connect to the API services.
    """
    
    def __init__(self, user = "neo4j"):
        
    # Berkeley.edu login into Neo4j AuraDB
        uri = "neo4j+s://cfcef656.databases.neo4j.io:7687"
        user = str(input("Please enter your user ID: "))
        pwd = "hDSNBz5Ge4NK6Mo79JRn7jNxlXNh6MSmfaYB2Xobm70"
        graph = Graph(uri, auth=(user, pwd))
        
        qSummary = "MATCH p = (n) - [r] -() \
        RETURN count(*)" # count total links
        
        qStructure = "MATCH (n) \
        RETURN n.level1, n.level2, n.name, count(*) \
        ORDER BY n.level1, n.level2, n.name DESC " # report the full taxonomic structure of all nodes
        
        self.summary = graph.run(qSummary).to_table() # run query to view the count of total links
        self.structure = graph.run(qStructure).to_table() # run query to view the full taxonomic structure of all nodes
        self.whole = graph # load the entire knowledge graph data from API services
    
    def summary(self):
        return self.summary
    
    def structure(self):
        return self.structure
    
    def whole(self):
        return self.whole
    
    def __repr__(self, user = "neo4j"):
        return "The Knowledgebase has been loaded from user " + str(user) + "'s AuraDB API services."
```


    <IPython.core.display.Javascript object>



```python
KB = Knowledgebase()
KB.structure
```

    Please enter your user ID: neo4j
    




<table><tr><th>n.level1</th><th>n.level2</th><th>n.name</th><th>count(*)</th></tr><tr><td style="text-align:left">economic well-being</td><td style="text-align:left">economic reward</td><td style="text-align:left">economic reward</td><td style="text-align:right">10</td></tr><tr><td style="text-align:left">economic well-being</td><td style="text-align:left">employment security</td><td style="text-align:left">employment security</td><td style="text-align:right">3</td></tr><tr><td style="text-align:left">economic well-being</td><td style="text-align:left">others</td><td style="text-align:left">economic reward</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">economic well-being</td><td style="text-align:left">pay satisfaction</td><td style="text-align:left">pay satisfaction</td><td style="text-align:right">7</td></tr><tr><td style="text-align:left">economic well-being</td><td style="text-align:left">unsure</td><td style="text-align:left">economic well-being: others</td><td style="text-align:right">4</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">work team racial composition</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">work load</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">work climate</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">women who perceive a low level of gender equity in departmental decisions will perceive more exclusion from their department</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">women in academic departments with a lower percentage of women will report greater perceptions of exclusion</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">well-designed store-level training and development</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">well-designed store-level performance appraisal</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">well-designed store-level communication</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">union instrumentality</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">uncertainty avoidance</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">than men who perceive a high level of gen- der equity</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">team climate</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">task characteristics</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">subjective referent group absence norms</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">strategic value of occupation groups</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">store-level surface-level similarity</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">stigmatization</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">spousal organizational commitment</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">social climate</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">skill-enhancing practices</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">significant work events (where high and low scores indicate positive and negative events, respectively)</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">significant work events</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">service climate than vice versa</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">service climate</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">resource availability</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">punishment</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">punishers who have a pragmatic reputation</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">psychological climate</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">positive relationship of developmental assignments, training, mentoring, and coaching to organizational commitment</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">poc</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">perceptions of competency model relevance</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">perception of competency model relevance</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">perceived politics</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">perceived job hazards</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">organizational trust</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">organizational reputation</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">observers will trust altruistic punishers</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">negative relationship between significant work events (where high and low scores indicate positive and negative events, respectively)</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">level of perceived supervisor effectiveness</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">leadership style</td><td style="text-align:right">14</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">leadership effectiveness</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">leadership behavior</td><td style="text-align:right">3</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">leader initiating structure</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">leader departures</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">leader consideration</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">job characteristics</td><td style="text-align:right">7</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">its dispersion</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">informal job search</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">inducements</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">hrm systems</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">hrm practice orientation</td><td style="text-align:right">16</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">hrm practice characteristics</td><td style="text-align:right">19</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">hrm effectiveness</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">hpws investment in occupation groups</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">hpws differentiation</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">guidance coaching</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">fwc</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">fun activities</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">follower level of participation in organizational citizenship behaviors</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">firm performance</td><td style="text-align:right">3</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">environment: others</td><td style="text-align:right">16</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">environment change</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">employment in a specialist organization</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">employee perceptions of reputation and time commitment</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">employee perceptions of reputation and organizational identification</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">employee perceptions of reputation</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">diversity</td><td style="text-align:right">6</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">customer perception</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">customer commitment</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">csr</td><td style="text-align:right">5</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">cooperative relations</td><td style="text-align:right">4</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">collective perceptions of social context</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">collective customer perceptions of service quality</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">better performance for these firms, when compared to the prevalence of vertical founder–employee kin ties in new firms.</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">better performance for these firms, when compared to the prevalence of horizontal founder kin ties in new firms.</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">environment</td><td style="text-align:left">environment</td><td style="text-align:left">approval absence norms are weaker</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">autonomy</td><td style="text-align:left">autonomy</td><td style="text-align:right">7</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">career advancement</td><td style="text-align:left">career advancement</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">career satisfaction</td><td style="text-align:left">career satisfaction</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">creativity</td><td style="text-align:left">creativity</td><td style="text-align:right">3</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">engagement</td><td style="text-align:left">engagement</td><td style="text-align:right">13</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">meaningfulness</td><td style="text-align:left">work meaning</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">meaningfulness</td><td style="text-align:left">meaningfulness</td><td style="text-align:right">8</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">personal development</td><td style="text-align:left">personal development</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">self-efficacy</td><td style="text-align:left">self-efficacy</td><td style="text-align:right">3</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">self-esteem</td><td style="text-align:left">self-esteem</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">unsure</td><td style="text-align:left">eudamonic well-being: others</td><td style="text-align:right">24</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">unsure</td><td style="text-align:left">employee pride in the organization</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">eudamonic well-being</td><td style="text-align:left">work motivation</td><td style="text-align:left">work motivation</td><td style="text-align:right">5</td></tr><tr><td style="text-align:left">hedonic well-being</td><td style="text-align:left">job satisfaction</td><td style="text-align:left">job satisfaction</td><td style="text-align:right">23</td></tr><tr><td style="text-align:left">hedonic well-being</td><td style="text-align:left">life satisfaction</td><td style="text-align:left">life satisfaction</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">hedonic well-being</td><td style="text-align:left">negative affect</td><td style="text-align:left">negative affect</td><td style="text-align:right">10</td></tr><tr><td style="text-align:left">hedonic well-being</td><td style="text-align:left">positive affect</td><td style="text-align:left">positive affect</td><td style="text-align:right">15</td></tr><tr><td style="text-align:left">hedonic well-being</td><td style="text-align:left">strain</td><td style="text-align:left">strain</td><td style="text-align:right">24</td></tr><tr><td style="text-align:left">hedonic well-being</td><td style="text-align:left">stress</td><td style="text-align:left">stress</td><td style="text-align:right">11</td></tr><tr><td style="text-align:left">hedonic well-being</td><td style="text-align:left">unsure</td><td style="text-align:left">hedonic well-being: others</td><td style="text-align:right">35</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">trust with observers’ perceptions of the punisher’s</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">time-lagged effect of abusive supervision</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">task interdependency is high as compared to low</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">strategic value</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">positivity interactions</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">negativity interactions</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">misfit</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">leader-member interaction</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">human capital resource fit (complementarity) will be a substitute for the transfer of external social capital resources</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">human capital of those occupation groups</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">human capital of occupation groups</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">fit</td><td style="text-align:right">20</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">facilitation coaching</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">facilication coaching</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">coworker socializing</td><td style="text-align:right">3</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">interaction</td><td style="text-align:left">centrality</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">interaction</td><td style="text-align:left">unsure</td><td style="text-align:left">interaction: others</td><td style="text-align:right">7</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">commitment</td><td style="text-align:left">job embeddedness</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">others</td><td style="text-align:left">time</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">others</td><td style="text-align:left">performance subjectivity</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">others</td><td style="text-align:left">others</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">others</td><td style="text-align:left">ocbs</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">others</td><td style="text-align:left">employer-centered fwas </td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">others</td><td style="text-align:left">employee-centered fwas </td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">others</td><td style="text-align:left">direct voice</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">others</td><td style="text-align:left">difference between ocbo and ocbi</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">others</td><td style="text-align:left">cse</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">performance</td><td style="text-align:left">engaging in ocb</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">turnover</td><td style="text-align:left">the effect of intent to leave</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">others</td><td style="text-align:left">unsure</td><td style="text-align:left">rhp</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">performance</td><td style="text-align:left">performance</td><td style="text-align:left">job performance</td><td style="text-align:right">91</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">work expectations</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">vocational frustration</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">vitality at the end of the workday</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">trait promotion focus</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">trait prevention focus</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">the probability that an employee founds a startup firm</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">tenure in previous positions</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">spouse career support</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">spousal resentment toward the organization</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">spousal resentment toward the job incumbent&#039;s organization</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">spousal resentment</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">spousal commitment to the incumbent’s organization</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">spousal commitment to the incumbent&#039;s organization</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">self-interested punishers</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">remaining time</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">rationalizing hiding</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">pv motives</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">psychological detachment</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">proactive work behavior on vitality</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">proactive work behavior on detachment</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">proactive personality</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">pro-job unethical behavior</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">prevention focus at work (but not by promotion focus at work).</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">prevention focus</td><td style="text-align:right">3</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">power distance</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">positive feeling states</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">positive and negative affect</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">playing dumb</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">perceptions of exclusion from the informal networks</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">perceived prosocial impact of work</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">people who perceive themselves as having open-ended compared with constrained remaining time in their occupational future</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">organizational tenure</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">organizational frustration</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">one&#039;s vitality experienced at the end of the workday</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">one&#039;s detachment in the evening</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">observers will trust punishers who have a principled, value-based reputation</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">negative feeling states</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">narcissistic behavior</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">mobility</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">migrant workers’ urban adjustment</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">migrant workers&#039; urban adjustment</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">migrant workers&#039; rural identity</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">migrant workers&#039; identity strain</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">men who perceive a low level of gender equity in departmental decisions will not perceive more exclusion from their departmen</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">mce</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">knowledge hiding</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">job tenure</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">job search behavior</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">job frustration</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">job crafting (increasing social resources, increasing structural job resources, and increasing job challenges).</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">job crafting</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">in-group collectivism</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">identity strain</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">gender</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">future focus</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">first job crafting</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">evasive hiding</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">employer-centered fwas</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">employees’ ftp</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">employees&#039; ftp</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">employee-centered fwas</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">employee utilization</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">employee perceptions of the strategic value of occupation groups</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">employee per captions of reputation</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">employee knowledge hiding</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">employee experience</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">employee attribution</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">detachment in the evening</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">core self-evaluations</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">core self-evaluation</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">conscientiousness</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">being envied</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">behavior</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">avoidance orientations</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">agreeableness</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">person</td><td style="text-align:left">person</td><td style="text-align:left">age</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">physical well-being</td><td style="text-align:left">health problems</td><td style="text-align:left">insomnia</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">physical well-being</td><td style="text-align:left">health problems</td><td style="text-align:left">health problems</td><td style="text-align:right">6</td></tr><tr><td style="text-align:left">physical well-being</td><td style="text-align:left">health status</td><td style="text-align:left">health status</td><td style="text-align:right">3</td></tr><tr><td style="text-align:left">physical well-being</td><td style="text-align:left">strain</td><td style="text-align:left">emotional exhaustion</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">physical well-being</td><td style="text-align:left">strain </td><td style="text-align:left">job‐related feelings of anxiety</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">physical well-being</td><td style="text-align:left">unsure</td><td style="text-align:left">physical well-being: others</td><td style="text-align:right">9</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">commitment</td><td style="text-align:left">commitment</td><td style="text-align:right">46</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">commitment</td><td style="text-align:left">collective affective commitment</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">commitment</td><td style="text-align:left">affective commitment</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">justice</td><td style="text-align:left">justice</td><td style="text-align:right">13</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">justice</td><td style="text-align:left">employee fairness</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">meaningfulness</td><td style="text-align:left">collective meaningfulness</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">others</td><td style="text-align:left">commitment</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">psychological contract</td><td style="text-align:left">psychological contract</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">social capital</td><td style="text-align:left">social capital</td><td style="text-align:right">14</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">social well-being</td><td style="text-align:left">social well-being</td><td style="text-align:right">2</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">strain</td><td style="text-align:left">citizenship fatigue</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">trust</td><td style="text-align:left">trust</td><td style="text-align:right">7</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">turnover</td><td style="text-align:left">turnover</td><td style="text-align:right">63</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">unsure</td><td style="text-align:left">social well-being: others</td><td style="text-align:right">28</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">unsure</td><td style="text-align:left">envy toward higher-paid others</td><td style="text-align:right">1</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">work relationship quality</td><td style="text-align:left">work relationship quality</td><td style="text-align:right">11</td></tr><tr><td style="text-align:left">social well-being</td><td style="text-align:left">workplace support</td><td style="text-align:left">workplace support</td><td style="text-align:right">16</td></tr><tr><td style="text-align:left">testing</td><td style="text-align:left">testing</td><td style="text-align:left">testing</td><td style="text-align:right">4</td></tr></table>



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


```python
# Object 2 - Knowledge

# Define a query function to return a subset of knowledge in the Knowledgebase:

class Knowledge:
    
    """
    Knowledge is the basic unit inside the Knowledgebase. 
    Each unit of Knowledge has three components: two nodes and one link. 
    Each node is a real-world concept that belongs to the taxonomy of the entire Knowledgebase.
    Each link is a predictive relationship. Node1 is a predictor of Node2.
    """
        
    def __init__(self, node1 = "", node2 = ""):
        
        self.node1 = node1
        self.node2 = node2
    
        if self.node1 == "" and self.node2 == "":

            qSummary = "MATCH p = (n1) - [r] - (n2) \
            RETURN n1.level2, n2.level2, count(*) \
            ORDER BY count(*) DESC " # report total count all links
            
            qReport = "MATCH p = (n1) - [r] - (n2) \
            RETURN n1.level2, n1.measure, n2.level2, n2.measure, \
            r.Direction, r.SampleIndustries, r.SampleCountries, r.PublicationTitle, count(*) \
            ORDER BY count(*) DESC " # report full table of knowledge details of the entire Knowledgebase
            
            qTeacher = "MATCH p = (n1) - [r] - (n2) \
            RETURN r.ResearchTeam, count(*) \
            ORDER BY count(*) DESC " # report the names of Teacher team members of the entire Knowledgebase

        elif self.node1 != "" and self.node2 == "":
            
            n1 = str(self.node1).lower()
            
            qSummary = "MATCH p = (n1) - [r] - (n2) \
            WHERE n1.level2 = '" + n1 + "'\
            RETURN n1.level2, n2.level2, count(*) \
            ORDER BY count(*) DESC " # report total count of links with node1

            qReport = "MATCH p = (n1) - [r] - (n2) \
            WHERE n1.level2 = '" + n1 + "'\
            RETURN n1.level2, n1.measure, n2.level2, n2.measure, \
            r.Direction, r.SampleIndustries, r.SampleCountries, r.PublicationTitle, count(*) \
            ORDER BY count(*) DESC " # report full table of knowledge details including node1
                
            qTeacher = "MATCH p = (n1) - [r] - (n2) \
            WHERE n1.level2 = '" + n1 + "'\
            RETURN r.ResearchTeam, count(*) \
            ORDER BY count(*) DESC " # report the names of Teacher teams that created links with node1
            
        elif node1 != "" and node2 != "":
            
            n1 = str(self.node1).lower()
            n2 = str(self.node2).lower()
            
            qSummary = "MATCH p = (n1) - [r] - (n2) \
            WHERE n1.level2 = '" + n1 + "' AND n2.level2 = '" + n2 + "'\
            RETURN n1.level2, n2.level2, count(*) \
            ORDER BY count(*) DESC " # report total count of links between node1 and node2
            
            qReport = "MATCH p = (n1) - [r] - (n2) \
            WHERE n1.level2 = '" + n1 + "' AND n2.level2 = '" + n2 + "'\
            RETURN n1.level2, n1.measure, n2.level2, n2.measure, \
            r.Direction, r.SampleIndustries, r.SampleCountries, r.PublicationTitle, count(*) \
            ORDER BY count(*) DESC " # report full table of knowledge details for links between node1 and node2

            qTeacher = "MATCH p = (n1) - [r] - (n2) \
            WHERE n1.level2 = '" + n1 + "' AND n2.level2 = '" + n2 + "'\
            RETURN r.ResearchTeam, count(*) \
            ORDER BY count(*) DESC " # report the names of Teacher teams that created links between node1 and node2
        
        # Load default Knowledgebase
#         KB = Knowledgebase()
        g = KB.whole
        
        self.summary = g.run(qSummary).to_table() # run query to view summary
        self.report = g.run(qReport).to_table() # run query to view full table
        self.teacher = g.run(qTeacher).to_table() # run query to view Teacher names
    
    def summary(self):
        return self.summary
    
    def report(self):
        return self.report
    
    def teacher(self):
        return self.teacher
```


```python
?Knowledge
```

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


```python
# Object 3 - Node

# Define a Node as a component of Knowledge, the other being Link:

class Node():
    
    """
    A Node is a subunit of Knowledge.
    It represents an entity of logic concept in the real world.
    Each node's labels are pre-assigned based on an expert taxonomy
    following Zhong, Sandoval, Chen, Woehr, Long, and Tonidandel (2021)'s working paper.
    """
    
    def __init__(self, nodeLevel2 = ""):
        
        if nodeLevel2 == "":
            raise Exception("You need to enter a valid concept.")
        
        else:
            self.nodeLevel2 = nodeLevel2
            
            n = str(self.nodeLevel2).lower()
            
            qName = "MATCH (n) - [r] - () \
            WHERE n.level2 = '" + n + "'\
            RETURN n.name, count(*) \
            ORDER BY count(*) DESC " # report all names under node label

            qMeasure = "MATCH (n) - [r] - () \
            WHERE n.level2 = '" + n + "'\
            RETURN n.measure, count(*) \
            ORDER BY count(*) DESC " # report all measures for node
                
            qTaxonomy = "MATCH (n) - [r] - () \
            WHERE n.level2 = '" + n + "'\
            RETURN n.level1, n.level2, n.name, count(*) \
            ORDER BY n.level1, n.level2, n.name DESC " # report the three-level taxonomy for node
            
        # Load default Knowledgebase
#         KB = Knowledgebase()
        g = KB.whole
        
        self.name = g.run(qName).to_table() # run query to view all names under node
        self.measure = g.run(qMeasure).to_table() # run query to view all measures for node
        self.taxonomy = g.run(qTaxonomy).to_table() # run query to view the three-level taxonomy for node
    
    def name(self):
        return self.name
    
    def measure(self):
        return self.measure
    
    def taxonomy(self):
        return self.taxonomy
```


```python
?Node
```

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


```python
# Object 4 - Link

# Define a Link as a component of Knowledge, the other being Nodes:

class Link:
    
    """
    A link is a subunit of Knowledge. 
    It specifies a predictive relationship between two Nodes. 
    Unless otherwise specified, Node1 predicts Node2.
    """
    
    def __init__(self, node1, node2):
        
        if node1 == "" or node2 == "":
            raise Exception("You need to specify two concepts.")
            
        else:
            self.node1 = node1
            self.node2 = node2
            n1 = str(self.node1).lower()
            n2 = str(self.node2).lower()
            
            qDirection = "MATCH p = (n1) - [r] - (n2) \
            WHERE n1.level2 = '" + n1 + "' AND n2.level2 = '" + n2 + "'\
            RETURN r.Direction, count(*) \
            ORDER BY count(*) DESC " # report the direction of links between node1 and node 2 (positive, negative, nonlinear, or unclear)
            
            qSamplesize = "MATCH p = (n1) - [r] - (n2) \
            WHERE n1.level2 = '" + n1 + "' AND n2.level2 = '" + n2 + "'\
            RETURN r.SampleSize, count(*) \
            ORDER BY count(*) DESC " # report sample size of each study in which the links were statistically estimated.

            qSampleIndustries = "MATCH p = (n1) - [r] - (n2) \
            WHERE n1.level2 = '" + n1 + "' AND n2.level2 = '" + n2 + "'\
            RETURN r.SampleIndustries, count(*) \
            ORDER BY count(*) DESC " # report sample industries of each study in which the links were statistically estimated.
            
            qSampleCountries = "MATCH p = (n1) - [r] - (n2) \
            WHERE n1.level2 = '" + n1 + "' AND n2.level2 = '" + n2 + "'\
            RETURN r.SampleCountries, count(*) \
            ORDER BY count(*) DESC " # report sample countries of each study in which the links were statistically estimated.
        
        # Load default Knowledgebase
#         KB = Knowledgebase()
        g = KB.whole
        
        self.direction = g.run(qDirection).to_table() # run query to report a summary of directions
        self.size = g.run(qSamplesize).to_table() # run query to report a summary of sample size
        self.industry = g.run(qSampleIndustries).to_table() # run query to report a summary of sample industries
        self.country = g.run(qSampleCountries).to_table() # run query to report a summary of sample countries
    
    def direction(self):
        return self.direction
    
    def size(self):
        return self.size
    
    def industry(self):
        return self.industry 
    
    def country(self):
        return self.country
```


```python
?Link
```

## <center>5.	Knowledge Teachers </center>
This class allows a user to create new Knowledge and upload it into the Knowledgebase through API services. 
User will be asked to provide the user ID to connect.

![expand-player-node](https://mk0sharpnotionswseoa.kinstacdn.com/wp-content/uploads/expand-player-node.gif)

Function:

### a.	Review
Review new **Expert Knowledge**


```python
# Object 5 - Knowledge Teacher

class Teacher:
    
    """
    This class allows a user to create new Knowledge and upload it into the Knowledgebase through API services. 
    User will be asked to provide the user ID to connect.
    """
    
    def __init__(self, name = "", node1level1 = "", node2level1 = "", 
               node1level2 = "", node2level2 = "", 
               node1name = "", node2name = "",
               node1measure = "", node2measure = "",
               linkDirection = "", linkSamplesize = "", linkSampleIndustries = "", linkSampleCountries = "",
               linkPublicationTitle = "", code = ""):
        
        name = str(input("Please enter the name(s) of your team:"))
        self.name = name
            
        node1level1 = str(input("Specify the level1 label for Node 1:"))
        node1level2 = str(input("Specify the level2 label for Node 1:"))
        node1name = str(input("Specify the name for Node 1:"))
        node1measure = str(input("Specify the measure for Node 1:"))
        node2level1 = str(input("Specify the level1 label for Node 2:"))
        node2level2 = str(input("Specify the level2 label for Node 2:"))            
        node2name = str(input("Specify the name for Node 2:"))
        node2measure = str(input("Specify the measure for Node 2:"))
        linkDirection = str(input("Specify the direction of the link (positive, negative, nonlinear, or unclear):"))
        linkSamplesize = str(input("Specify sample size:"))
        linkSampleIndustries = str(input("Specify sample industries:"))
        linkSampleCountries = str(input("Specify sample countries:"))
        linkPublicationTitle = str(input("Specify the source of knowledge:"))
        code = str(input("Provide a unique code for your own access for future modification:"))

        self.n1l1 = node1level1
        self.n2l1 = node2level1
        self.n1l2 = node1level2
        self.n2l2 = node2level2
        self.n1 = node1name
        self.n2 = node2name
        self.n1ms = node1measure
        self.n2ms = node2measure
        self.ldir = linkDirection
        self.lsize = linkSamplesize
        self.lind = linkSampleIndustries
        self.lcntry = linkSampleCountries
        self.lpub = linkPublicationTitle
        self.code = code

        Addn1 = "CREATE (n:construct \
        {name: '" + self.n1 + "', \
        level1: '" + self.n1l1 + "', \
        level2: '" + self.n1l2 + "', \
        measure: '" + self.n1ms + "'})" # create a new node1

        Addn2 = "CREATE (n:construct \
        {name: '" + self.n2 + "', \
        level1: '" + self.n2l1 + "', \
        level2: '" + self.n2l2 + "', \
        measure: '" + self.n2ms + "'})" # create a new node2

        AddLink = "MATCH (n1:construct), (n2:construct) \
        WHERE n1.name ='" + self.n1 + "' AND n2.name ='" + self.n2 + "' \
        CREATE (n1) - [r:causes {Direction: '" + self.ldir + "', \
        SampleSize: '" + self.lsize + "', \
        SampleIndustries: '" + self.lind + "', \
        SampleCountries: '" + self.lcntry + "', \
        PublicationTitle: '" + self.lpub + "', \
        Reference: '" + self.code + "', \
        ResearchTeam: '" + self.name + "' \
        }] -> (n2) \
        RETURN type(r)" # create a new link between node1 and node2

        # Load default Knowledgebase
#         KB = Knowledgebase()
        g = KB.whole

        g.run(Addn1).to_table() # add node1 into Knowledgebase KG
        g.run(Addn2).to_table() # add node2 into Knowledgebase KG
        g.run(AddLink).to_table() # add Link into Knowledgebase KG
        
        review = "MATCH p = (n1) - [r] -> (n2) \
        WHERE r.Reference = '" + self.code + "' \
        RETURN n1.level1, n1.level2, n1.name, n1.measure, n2.level1, n2.level2, n2.name, n2.measure, \
        r.Direction, r.SampleSize, r.SampleIndustries, r.SampleCountries, r.PublicationTitle, r.ResearchTeam, count(*)"
        
        self.review = g.run(review).to_table() # review the new link
    
    def review(self):
        return self.review
        
    def __repr__(self):
        return "You have entered a new link to Knowledgebase."
```


```python
?Teacher
```

## <center>6.	Knowledge Learner </center>
This is to confirm a user is a Learner, and record his or her intention of using the Knowledgebase.

Function:

### a.	Purpose
Research question underlying a query request by the **Knowledge Learner**


```python
# Object 6 - Knowledge Learner

# Specify the purpose of knowledge extraction:

class Learner:

    """
    This is to confirm a user is a Learner, and record his or her intention of using the Knowledgebase.
    """

    def __init__(self, intent = None):

        intent = int(input("Are you sure you want to teach now? Yes (1) or No (2)."))

        if intent == 1:
            Teacher() # switch to Teacher mode
            self.purpose = "Thank you, teacher, let's start teaching!"
        else:
            self.purpose = "Hmmm...Maybe learn something first?"

    def purpose(self):
        return self.purpose
```


```python
?Learner
```


```python

```
