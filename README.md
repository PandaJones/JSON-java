Milestone 3


All functions are in XML.java

All unit tests are in XMLTest.java

To use, you can build it through gradle or maven.

For maven, type in "mvn clean test" in the directory that the library is in.

For gradle, type in "gradlew clean build test" in the directory that the library is in.


There is a definite benefit to being inside the library vs the client code for replacing all the keys. 
In the client code, I had to iterate through the JSONObject (which included JSONArrays) just so I could make a new JSONObject with whatever modification was used the keys. This essentially means that I made 2 JSONObjects through 2 passes (one with the xml, one with the JSONObject). Not very efficient and having both JSONObjects in memory can impact the system if the JSONObject is big.

Meanwhile in the library, I can directly go inside the xml using the function to transform the keys and then convert to an JSONObject. One pass through the parsing of xml and only one instance of a JSONObject being made. Much better than what I did in the client code. 
The only snag it hits is if the XML has a value that has no tags, this results in parse putting content as the key for that value in the JSONObject. As I don't know if content is or isn't consider a key, my code nevertheless check and transforms it if it exists. Adding another smaller pass and another JSONObject made (however, this replace the other JSONObject so reality is that there is still only one JSONObject in memory). Still less expensive than client code.

MileStone 4

New stream class and method in JSONObject.java

All unit tests are in XMLTest.java

My stream only streams the leaf nodes of the JSONObject (includes support for JSONArrays as well)

You should be able to chain stream operations once you do jsonObject.toStream().
