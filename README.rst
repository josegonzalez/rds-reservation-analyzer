========================
rds-reservation-analyzer
========================

performs naive analysis on average rds resource utilization to inform reservation decisions Edit

Requirements
============

* Python 2.7+

Installation
============

- create a ``virtualenv``
- ``pip install -r requirements.txt``

Usage
=====

This project supports checking any of three metrics as a percentage of total resources:

- ``cpu``: via the ``CPUUtilization`` cloudwatch metric
- ``disk``: via the ``FreeStorageSpace`` cloudwatch metric (WIP)
- ``memory``: via the ``FreeableMemory`` cloudwatch metric

For ``disk`` and ``memory``, the percentage values are interpolated based on RDS data
and information from the `EC2Instances.info
<http://www.ec2instances.info/>`_. website.

Just execute the binary with the correct arguments::

    # check any of three classes of metric
    bin/rds-reservation-analyzer --check cpu
    bin/rds-reservation-analyzer --check disk
    bin/rds-reservation-analyzer --check memory

    # override the default threshold percentage (25)
    bin/rds-reservation-analyzer --check cpu --threshold 50

    # override the default days to check average over (90)
    bin/rds-reservation-analyzer --check cpu --days-to-check 90

    # override the default tag key/value (environment:production)
    bin/rds-reservation-analyzer --check cpu --tag-name environment --tag-value production

    # override the default sort (name) (options: name, percentage, reserve)
    bin/rds-reservation-analyzer --check cpu --sort-by percentage

    # remove sparklines from output
    bin/rds-reservation-analyzer --check cpu --no-sparklines

Credits
=======

Thanks to Garret Heaton for maintaining `EC2Instances.info
<http://www.ec2instances.info/>`_.
