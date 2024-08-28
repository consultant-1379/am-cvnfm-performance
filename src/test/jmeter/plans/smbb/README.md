# EVNFM SMBB Configuration Performance Test Plan

## Configuration

### Parameters

**onboarding-timeout:** Onboarding timeout

**single-helm-install:** Path to single chart csar for instantiate operation

**single-helm-install-vnfdId:** Vnfd ID of single chart csar for instantiate operation

**single-helm-upgrade:** Path to single chart csar for upgrade operation

**single-helm-upgrade-vnfdId:** Vnfd ID of single chart csar for upgrade operation

**multi-helm-install:** Path to multi chart csar for instantiate operation

**multi-helm-install-vnfdId:** Vnfd ID of multi chart csar for instantiate operation

**multi-helm-upgrade:** Path to multi chart csar for upgrade operation

**multi-helm-upgrade-vnfdId:** Vnfd ID of multi chart csar for upgrade operation

**storage-class:** Cluster PV

## How to run
    mvn clean verify -Pperformance -Dtest-name=smbb -DsingleThreadCount=5 -DmultiThreadCount=5
## Default number of threads for single and multi helms is 5. Pass preferable values via maven parameters singleThreadCount and multiThreadCount

## How to run JMeter GUI for debugging purposes
    mvn jmeter:configure jmeter:gui -Pperformance -Dtest-name=smbb
