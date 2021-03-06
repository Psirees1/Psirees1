Skip to content
Why GitHub? 
Team
Enterprise
Explore 
Marketplace
Pricing 
Search
Sign in
Sign up
VishnuBoddapati
/
devops
10
Code
Issues
Pull requests
3
Actions
Projects
Wiki
Security
Insights
devops/1-MAVEN/maven-commands.txt
@devopsdocs
devopsdocs commands added
Latest commit 72c36ae on Sep 20, 2017
 History
 1 contributor
84 lines (53 sloc)  3.1 KB
  
--- maven all commands

mvn clean  // To clean the code i.e target file will be removed

mvn compile  // To compile the code i.e generate the binaries or .class files

mvn verify   //

mvn test    // To run Junit test cases

mvn package  // verify,compile and create the artifacts nothing bug jar,war,zip...etc.

mvn install  // verify, compile,package and put the artifacts in local maven repo(.m2)

mvn install -P <profile-name>  // To compile based on Profile.i.e for every module maintain a profile.

mvn install -Pcoveage-ut,enableunittests,all

//Perticular module dont want to compile
mvn install --projects "!com.aig.dmp:global-parent-java"


// to upload aritfacts into aritifactory server(nexus,artifactory) use

mvn deploy -Dusername= -Dpassword= 

//static code analysis using sonar(sonar profile in settings.xml) and uploads Unit Test results 
    & Code coverage report to Sonar

//static code analysis + code coverage
clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test sonar:sonar

//Just do static code analysis
mvn sonar:sonar
mvn sonar:sonar -Dsonar.login=**** -Dsonar.password=****
mvn sonar:sonar -Psonar
mvn help:effectiv-pom -Psonar

-- Release commands with interactive mode
mvn release:prepare   // To tag the code 
mvn release:perform  // after prepare read for perform i.e deploy release artifacts into nexus server
 
mvn release:prepare -Dusername=username -Dpassword=password // to provide scm username and password while release
mvn release:prepare -DdryRun=true // to make sure before release after this run mvn release:clean 
mvn release:prepare -P css,js // it will create a tag and move to next development version
-- Release commands with non-interactive mode

-B or --batch-mode = Non Interactive mode 
mvn -B release:prepare release:perform // use this to run jenkins
mvn -B release:clean release:prepare release:perform
mvn --batch-mode release:prepare release:perform
mvn --batch-mode release:clean release:prepare release:perform -Dresume=false
mvn --batch-mode -Dtag=dmp-global-12.0.6 release:prepare -DreleaseVersion=12.0.6 -DdevelopmentVersion=12.0.7-SNAPSHOT

-- version update commands

mvn release:update-versions
mvn --batch-mode release:update-versions
mvn --batch-mode release:update-versions -DautoVersionSubmodules=true
mvn release:update-versions -DautoVersionSubmodules=true -DdevelopmentVersion=12.0.4-SNAPSHOT

mvn versions:set -DnewVersion=12.0.3-SNAPSHOT
mvn versions:set -DnewVersion=12.0.3-SNAPSHOT -f enforcer/pom.xml
mvn versions:set -DgroupId=com.aig.dmp -DartifactId=* -DoldVersion=12.* -DnewVersion=12.0.30-SNAPSHOT

mvn clean install -Dproject.version=12.0.50-SNAPSHOT 

--- To increment major,minor,incrementalversions

mvn build-helper:parse-version versions:set -DnewVersion=${parsedVersion.MajorVersion}.${parsedVersion.minorVersion}.${parsedVersion.incrementalVersion} versions:commit

Example: 1.0.0.1 -> 2.0.0.1 (Major release)
         1.0.0.1 -> 1.1.0.1 (Minor release)
         1.0.0.1 -> 1.0.1.1 (Patch release)
         1.0.0.1 -> 1.0.0.2 (Build release)


  [propertyPrefix].nextMajorVersion
  [propertyPrefix].nextMinorVersion
  [propertyPrefix].nextIncrementalVersion




?? 2021 GitHub, Inc.
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
Loading completeSkip to content
Why GitHub? 
Team
Enterprise
Explore 
Marketplace
Pricing 
Search
Sign in
Sign up
VishnuBoddapati
/
devops
10
Code
Issues
Pull requests
3
Actions
Projects
Wiki
Security
Insights
devops/1-MAVEN/maven-commands.txt
@devopsdocs
devopsdocs commands added
Latest commit 72c36ae on Sep 20, 2017
 History
 1 contributor
84 lines (53 sloc)  3.1 KB
  
--- maven all commands

mvn clean  // To clean the code i.e target file will be removed

mvn compile  // To compile the code i.e generate the binaries or .class files

mvn verify   //

mvn test    // To run Junit test cases

mvn package  // verify,compile and create the artifacts nothing bug jar,war,zip...etc.

mvn install  // verify, compile,package and put the artifacts in local maven repo(.m2)

mvn install -P <profile-name>  // To compile based on Profile.i.e for every module maintain a profile.

mvn install -Pcoveage-ut,enableunittests,all

//Perticular module dont want to compile
mvn install --projects "!com.aig.dmp:global-parent-java"


// to upload aritfacts into aritifactory server(nexus,artifactory) use

mvn deploy -Dusername= -Dpassword= 

//static code analysis using sonar(sonar profile in settings.xml) and uploads Unit Test results 
    & Code coverage report to Sonar

//static code analysis + code coverage
clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Pcoverage-per-test sonar:sonar

//Just do static code analysis
mvn sonar:sonar
mvn sonar:sonar -Dsonar.login=**** -Dsonar.password=****
mvn sonar:sonar -Psonar
mvn help:effectiv-pom -Psonar

-- Release commands with interactive mode
mvn release:prepare   // To tag the code 
mvn release:perform  // after prepare read for perform i.e deploy release artifacts into nexus server
 
mvn release:prepare -Dusername=username -Dpassword=password // to provide scm username and password while release
mvn release:prepare -DdryRun=true // to make sure before release after this run mvn release:clean 
mvn release:prepare -P css,js // it will create a tag and move to next development version
-- Release commands with non-interactive mode

-B or --batch-mode = Non Interactive mode 
mvn -B release:prepare release:perform // use this to run jenkins
mvn -B release:clean release:prepare release:perform
mvn --batch-mode release:prepare release:perform
mvn --batch-mode release:clean release:prepare release:perform -Dresume=false
mvn --batch-mode -Dtag=dmp-global-12.0.6 release:prepare -DreleaseVersion=12.0.6 -DdevelopmentVersion=12.0.7-SNAPSHOT

-- version update commands

mvn release:update-versions
mvn --batch-mode release:update-versions
mvn --batch-mode release:update-versions -DautoVersionSubmodules=true
mvn release:update-versions -DautoVersionSubmodules=true -DdevelopmentVersion=12.0.4-SNAPSHOT

mvn versions:set -DnewVersion=12.0.3-SNAPSHOT
mvn versions:set -DnewVersion=12.0.3-SNAPSHOT -f enforcer/pom.xml
mvn versions:set -DgroupId=com.aig.dmp -DartifactId=* -DoldVersion=12.* -DnewVersion=12.0.30-SNAPSHOT

mvn clean install -Dproject.version=12.0.50-SNAPSHOT 

--- To increment major,minor,incrementalversions

mvn build-helper:parse-version versions:set -DnewVersion=${parsedVersion.MajorVersion}.${parsedVersion.minorVersion}.${parsedVersion.incrementalVersion} versions:commit

Example: 1.0.0.1 -> 2.0.0.1 (Major release)
         1.0.0.1 -> 1.1.0.1 (Minor release)
         1.0.0.1 -> 1.0.1.1 (Patch release)
         1.0.0.1 -> 1.0.0.2 (Build release)


  [propertyPrefix].nextMajorVersion
  [propertyPrefix].nextMinorVersion
  [propertyPrefix].nextIncrementalVersion




?? 2021 GitHub, Inc.
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
Loading complete
