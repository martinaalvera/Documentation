INDIGO CLUES
============

CLUES is an elasticity manager system for HPC clusters and Cloud infrastructures that features the ability to power on/deploy working nodes as needed (depending on the job workload of the cluster) and to power off/terminate them when they are no longer needed.

Official GitBook documentation: https://www.gitbook.com/book/indigo-dc/clues-indigo/details

Check worker nodes status
*************************

To check worker node status: 

::

  # sudo clues status
  node                          state    enabled   time stable   (cpu,mem) used   (cpu,mem) total
  -----------------------------------------------------------------------------------------------
  vnode-1                       powon    enabled     00h02'54"      0,0.0            1,1073741824.0
  vnode-2                         off    enabled     00h41'00"      0,0.0            1,1073741824.0

CLUES commands:

::

  # clues --help
  The CLUES command line utility

  Usage: clues [-h] [status|resetstate|enable|disable|poweron|poweroff|nodeinfo|shownode|req_create|req_wait|req_get]

  [-h|--help] - Shows this help
  * Show the status of the platform
  Usage: status 

  * Reset the state of one or more nodes to idle
  Usage: resetstate <nodes>
  <nodes> - names of the nodes whose state want to be reset

  * Enable one or more nodes to be considered by the platform
  Usage: enable <nodes>
  <nodes> - names of the nodes that want to be enabled

  * Disable one or more nodes to be considered by CLUES
  Usage: disable <nodes>
  <nodes> - names of the nodes that want to be disabled

  * Power on one or more nodes
  Usage: poweron <nodes>
  <nodes> - names of the nodes that want to be powered on

  * Power off one or more nodes
  Usage: poweroff <nodes>
  <nodes> - names of the nodes that want to be powered off

  * Show the information about node(s), to be processed in a programmatically mode
  Usage: nodeinfo [-x] <nodes>
  [-x|--xml] - shows the information in XML format
  <nodes> - names of the nodes whose information is wanted to be shown

  * Show the information about node(s) as human readable
  Usage: shownode <nodes>
  <nodes> - names of the nodes whose information is wanted to be shown

  * Create one request for resources
  Usage: req_create --cpu <value> --memory <value> [--request <value>] [--count <value>]
  --cpu|-c <value> - Requested CPU
  --memory|-m <value> - Requested Memory
  [--request|-r] <value> - Requested constraints for the nodes
  [--count|-n] <value> - Number of resources (default is 1)

  * Wait for a request
  Usage: req_wait <id> [timeout]
  <id> - Identifier of the request to wait
  [timeout] - Timeout to wait

  * Get the requests in a platform
  Usage: req_get 

Check worker nodes deployment
*****************************

Worker node deployment log are available to: ``/var/log/clues2/clues2.log``
