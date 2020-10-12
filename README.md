
# Graph-Database

## **Using Graph Databases to Investigate Trends in Structure-Activity Relationship Networks**



**Installation steps**:

Download Neo4j 3.4.4 community edition and APOC 3.4.0.1 plugin:

https://neo4j.com/artifact.php?name=neo4j-community-3.4.4-unix.tar.gz

https://github.com/neo4j-contrib/neo4j-apoc-procedures/releases/download/3.4.0.1/apoc-3.4.0.1-all.jar

Download neo4j.conf template and graph_db data dump from Github:

https://github.com/ddsneo4j/Graph-Database


Extract Neo4j:

tar zxvf neo4j-community-3.4.4-unix.tar.gz

Note: adjust neo4j.conf according to your hardware specs!
(The one provided uses 32 GB for heap and 11 GB for page cache.)

cp neo4j.conf neo4j-community-3.4.4/conf/
cp apoc-3.4.0.1-all.jar neo4j-community-3.4.4/plugins/
cp graph_db.dump neo4j-community-3.4.4/import
cd neo4j-community-3.4.4/bin
./neo4j-admin load --from=../import/graph_db.dump --database=graph.db --force

./neo4j start

Open Neo4j Browser to access the imported graph database
(Replace hostname by your server name or localhost):

http://hostname:7474/browser 
login/passwd: neo4j/neo4j

You are supposed to change the password of the graph database user "neo4j" at your first login.

Now you can copy and paste the Cypher queries from the supporting information into the top pane of
the Neo4j Browser and execute them by pressing CTRL+Enter or clicking on the arrow (>) right next to this pane.

You will find the chemical structure pictures in the PNG folder. We used 7zip to split the zip archives due to Github file size limmitations.
In Neo4j, you can set the "image" property for each node as follows to point to your location (e.g. Apache) of the pictures:

**MATCH** (n) 
**WHERE** n:G **OR** n:Transformation **OR** n:Substituent **OR** n:Core **AND** **EXISTS**(n.image)
**SET** n.image = **REPLACE**(n.image,"your_path","my_server_and_port/path");

E.g.:

**MATCH** (n) 
**WHERE** n:G **OR** n:Transformation **OR** n:Substituent **OR** n:Core **AND** **EXISTS**(n.image)
**SET** n.image = **REPLACE**(n.image,"your_path","myserver.mydomain.com:8080/HERG_PNG");

Apache http server download: https://httpd.apache.org/download.cgi

Apache installation instructions: https://httpd.apache.org/docs/


Please be aware that Neo4j Browser cannot display node pictures. Hence, a tool like Graphileon PE or Tom Sawyer Graph 
Database Browser is needed for this task.

Download free Graphileon PE from here: https://graphileon.com/

Follow the installation steps for Graphileon PE: https://docs.graphileon.com/graphileon/Welcome.html

Some of the Cypher query results may come back slowly, which is caused by Neo4j Browser. These queries are actually
fast when execution and data consumption take place in Neo4j's cypher-shell or graph visualization tools such as Graphileon PE or 
Tom Sawyer Graph Database Browser. We highly recommend having the Neo4j graph database and the visualization tool collocated 
on the same machine for best performance.


Enjoy!


