### Meta
2024-10-15 12:30
**Tags:** [[docker]] [[docker_installation]] [[docker_post-installation_steps]]
**Status:** #pending 

### Configure default logging driver
Docker provides [[docker_logging_drivers|logging drivers]] for collecting and viewing log data from all containers running on a host. The default logging driver, `json-file`, writes log data to JSON-formatted files on the host filesystem. Over time, these log files expand in size, leading to potential exhaustion of disk resources.

To avoid issues with overusing disk for log data, consider one of the following options:
- Configure the `json-file` logging driver to turn on [[docker_log_rotation|log rotation]].
- Use an [[docker_alternatiove_logging_drive|alternative logging driver]] such as the [[docker_local_logging_driver|”local” logging driver]] that performs log rotation by default.
- Use a logging driver that sends logs to a remote logging aggregator.