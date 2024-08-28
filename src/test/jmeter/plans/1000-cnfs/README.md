# 1000 CNF'S Performance Tests

## Configuration

### Parameters

**skipImageUpload:** upload imageless csar

**packageId:**	csar id

**instanceName:** instance name format (release-test-00)

**namespace:**	namespace format (test-ns-00)

**csarPath:**	csar path for onboard

**cluster:**	cluster for cnfs to be instantiated

**replicaCount:**	replica count for each cnf

**instantiateLoopNum:**	number of total instances to instantiate per thread/user

**instantiateThreadNum:** number of parallel instantiate operations for setup phase

**cleanupThreadNum:** number of  parallel terminate operations for cleanup

## How to run
    mvn clean verify -Pperformance -Dtest-name=1000-cnfs

## How to run JMeter GUI for debugging purposes
    mvn jmeter:configure jmeter:gui -Pperformance -Dtest-name=1000-cnfs