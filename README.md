newapp
======

maven commands:-
******************* local **********************
mvn clean install

******************* snapshot *******************
mvn deploy -s ~/.m2/settings-local-nexus.xml

******************* release:minor:rc *********************************************
mvn release:prepare release:perform -s ~/.m2/settings-local-nexus.xml

******************* release:major ************************************************
mvn release:branch -DbranchName=newapp-1.X
// enter  at prompt:  What is the new working copy version for "newapp"? : : 2.0-SNAPSHOT
git pull

git checkout 1.X
mvn deploy -s ~/.m2/settings-local-nexus.xml
mvn release:prepare release:perform -s ~/.m2/settings-local-nexus.xml

git checkout master
mvn deploy -s ~/.m2/settings-local-nexus.xml
mvn release:prepare release:perform -s ~/.m2/settings-local-nexus.xml

git merge newapp-1.X
//resolve conflict in pom.xml version
mvn release:prepare release:perform -s ~/.m2/settings-local-nexus.xml

******************* release:deep-branching ************************************************
git checkout newapp-3.X
mvn release:branch -DbranchName=newapp-3.6.X
// enter  at prompt:  What is the new working copy version for "newapp"? : : 3.6-SNAPSHOT