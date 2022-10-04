# pic-sure-gic

This repository contains overrides and logic to drive the GIC common area UI and the implementation of the GIC Search Resource.

The GIC Search Resource implements the PIC-SURE resource API and provides a single source of search results for the GIC Common Area.  This has been required because not all institution nodes contain the same concepts, so searching a single institution resource does not provide complete or accurate results across the consortium.  
The GIC Search Resource reads the resource table from the PIC-SURE database, and queries each non-hidden resource for a complete data dictionary.  These dictionaries are then merged, providing a unified ontology containing each concept that appears in any institution resource.  
Because this resource is only applicable to the GIC PIC-SURE deployment, the implementation is maintained here in the GIC common area repository, and there are no explicit build jobs in the standard PIC-SURE-ALL-IN-ONE Jenkins server to build it.  The resource is built with standard maven commands (in Jenkins container, "/opt/apache-maven-3.6.3/bin/mvn clean install"), and then the pic-sure-search-resource.war file must be copied into the wildfly deployments directory (typically /usr/local/docker-config/wildfly/deployments/)

A seond note about the common area deployment:  When a new institution is added, we need to reate a new resource for the institution.  We can either copy an existing institution resource war file and rename it, or copy the pic-sure-passthrough-resource.war from the PIC-SURE API project build in jenkins.  In either case, it should be named approriately for the new insititution, and a new configuration folder & resource.properties file must be generated and set up.
