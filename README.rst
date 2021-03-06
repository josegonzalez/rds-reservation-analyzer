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

    # override the default threshold percentage (default: 25)
    bin/rds-reservation-analyzer --check cpu --threshold 50

    # override the default days to check average over (default: 90)
    bin/rds-reservation-analyzer --check cpu --days-to-check 90

    # override the default tag key/value (default: environment:production)
    bin/rds-reservation-analyzer --check cpu --tag-key environment --tag-value production

    # disable tag filtering
    bin/rds-reservation-analyzer --check cpu --tag-key none

    # override the default sort (default: id) (options: id, type, cost, savings, resource_usage, reserve)
    bin/rds-reservation-analyzer --check cpu --sort-by type
    bin/rds-reservation-analyzer --check cpu --sort-by cost
    bin/rds-reservation-analyzer --check cpu --sort-by savings
    bin/rds-reservation-analyzer --check cpu --sort-by resource_usage
    bin/rds-reservation-analyzer --check cpu --sort-by reserve

    # override the reservation type (default: 1yr-no-upfront)
    bin/rds-reservation-analyzer --check cpu --reservation-type all
    bin/rds-reservation-analyzer --check cpu --reservation-type 1yr-no-upfront
    bin/rds-reservation-analyzer --check cpu --reservation-type 1yr-partial-upfront
    bin/rds-reservation-analyzer --check cpu --reservation-type 1yr-all-upfront
    bin/rds-reservation-analyzer --check cpu --reservation-type 3yr-partial-upfront
    bin/rds-reservation-analyzer --check cpu --reservation-type 3yr-all-upfront

    # override the output format (default: stdout)
    # xls will output to a reservations.xls file
    bin/rds-reservation-analyzer --check cpu --format xls

    # override the output fields shown (default: id,type,cost,savings,resource_usage,reserve,sparklines)
    bin/rds-reservation-analyzer --check cpu --fields id,cost,savings,resource_usage

Credits
=======

Thanks to Garret Heaton for maintaining `EC2Instances.info
<http://www.ec2instances.info/>`_.
