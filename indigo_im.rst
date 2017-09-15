Infrastructure Manager
======================

The Infrastructure Manager (IM) is a tool that deploys complex and customized virtual infrastructures on IaaS Cloud deployments (such as AWS, OpenStack, etc.). 

Official GitBook documentation: https://www.gitbook.com/book/indigo-dc/im/details

Deployments log
***************

Deployment logs are available in `/var/tmp/.im/<im-id>/<deployment_ip>/ctxt_agent.log`. For instance:

::

  # tail -f /var/tmp/.im/1b0e064c-9a29-11e7-9c45-300000000002/90.147.102.27_0/ctxt_agent.log

.. Note::

   After each ansible role run, the log file is deleted!!
