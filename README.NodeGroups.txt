== Implementing Node Groups for Hadoop 2 Yarn Based MapReduce V2 Jobs ==
Somewhat similar to "Labels" feature coming up soon in Yarn, 
but this allows fine grained control of maps and reduces to be assigned 
to different node groups for MapReduce jobs.

The CBD mode is enabled by setting the property 
"yarn.app.mapreduce.am.job.cbd-mode.enable" to "true".
A file contains the labels for node groups that can be used
in specifying where the compute (map and reduce) tasks can run in "CBD" mode.
Name for this file can be specified with the property
"yarn.app.mapreduce.am.job.hostgroup.lables.file" in mapred-site.xml file.
The label for host group where compute(map/reduce) tasks are run is specified 
by the property "yarn.app.mapreduce.am.job.compute.hostgroup.label".
The label for storage host groups is specified 
by the property "yarn.app.mapreduce.am.job.compute.hostgroup.label".
You can restrict the map and reduce tasks to their own host groups.
The label for host group where map tasks are run is specified 
by the property "yarn.app.mapreduce.am.job.map.hostgroup.label".
The label for host group where reduce tasks are run is specified 
by the property "yarn.app.mapreduce.am.job.reduce.hostgroup.label".
You can "pushdown" the map tasks to the storage host group by 
setting "yarn.app.mapreduce.am.job.map.pushdown" to "true", which can be
useful in tasks that filter the data and avoid network traffic for reduce
tasks which might be doing the aggregation etc.

The default value for the compute node group is "DefaultComputeHerd".
The default value for the storage node group is "DefaultStorageHerd".
The map and reduce host groups default to compute node group if not specified.
The default value for pushdown is "false".
If a label specified in the property is not found CBD mode is diabled and the regular hadoop
behavior takes place for task placement.
