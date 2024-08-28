# EVNFM End of Sprint Endurance Test Plan

## Configuration

### Parameters

**timeout:** Timeout for LCM operations

**single-helm-install:** Path to single chart csar for instantiate operation

**single-helm-install-vnfdId:** Vnfd ID of single chart csar for instantiate operation

**single-helm-upgrade:** Path to single chart csar for upgrade operation

**single-helm-upgrade-vnfdId:** Vnfd ID of single chart csar for upgrade operation

**multi-helm-install:** Path to multi chart csar for instantiate operation

**multi-helm-install-vnfdId:** Vnfd ID of multi chart csar for instantiate operation

**multi-helm-upgrade:** Path to multi chart csar for upgrade operation

**multi-helm-upgrade-vnfdId:** Vnfd ID of multi chart csar for upgrade operation

**clusterConfigsFolder:** Folder with cluster config, which will be used for generating CISM configs

**countsConfig:** Number of generated configs for each CISM configs test thread

**cluster4CNF:** Cluster for deploying CNFs to



## How to run
    mvn clean verify -Pperformance -Dtest-name=endurance -DonboardThreadCount=1 -DmultiThreadCount=30 -DscaleThreadCount=5 -DbatchThreadCount=20
    -DclustersRegThreadCount=30 -DgetClustersThreadCount=30 -DclustersDeregThreadCount=30 -DqueryOperationsThreadCount=20 -DdeletePkgThreadCount=1

#### Default number of threads:
    packages onboarding: 1
    concurrent operations: 30
    scaling: 5
    reg-/deregister cism: 30
    cism query operation: 30
    query operations: 20
    delete packages: 1
    batch upgrade: 20

## How to run JMeter GUI for debugging purposes
    mvn jmeter:configure jmeter:gui -Pperformance -Dtest-name=endurance