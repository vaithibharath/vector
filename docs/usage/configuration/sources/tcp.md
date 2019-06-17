---
description: Accept log events through the TCP protocol
---

<!---
!!!WARNING!!!!

This file is autogenerated! Please do not manually edit this file.
Instead, please modify the contents of `dist/config/schema.toml`.
-->

# tcp source

![](../../../.gitbook/assets/tcp-source.svg)


The `tcp` source allows you to ingest [`log`][log_event] through the TCP protocol.

## Example

{% code-tabs %}
{% code-tabs-item title="vector.toml (examples)" %}
```coffeescript
[sources.my_tcp_source]
  # REQUIRED - General
  type = "tcp"

  # OPTIONAL - General
  address = "0.0.0.0:9000" # no default
  max_length = 102400 # default, bytes
  shutdown_timeout_secs = 30 # default, seconds

  # OPTIONAL - Context
  host_key = "host" # default
```
{% endcode-tabs-item %}
{% code-tabs-item title="vector.toml (schema)" %}
```coffeescript
[sources.<source-id>]
  # REQUIRED - General
  type = "<string>"

  # OPTIONAL - General
  address = "<string>"
  max_length = <int>
  shutdown_timeout_secs = <int>

  # OPTIONAL - Context
  host_key = "<string>"
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Options

| Key  | Type  | Description |
| :--- | :---: | :---------- |
| **OPTIONAL** - General | | |
| `address` | `string` | The address to bind the socket to.<br />`no default` `example: "0.0.0.0:9000"` |
| `max_length` | `int` | The maximum bytes size of incoming messages before they are discarded.<br />`default: 102400` `unit: bytes` |
| `shutdown_timeout_secs` | `int` | The timeout before a connection is forcefully closed during shutdown.<br />`default: 30` `unit: seconds` |
| **OPTIONAL** - Context | | |
| `host_key` | `string` | The key name added to each event representing the current host.<br />`default: "host"` |

## Output

### Log

The `tcp` source outputs [`log`][log_event] events with the following schema:

| Key  | Type  | Description |
| :--- | :---: | :---------- |
| `host` | `string` | The local machine's hostname.You can customize the name via the `host_key` config option.<br />`example: "10.23.22.122"` |
| `message` | `string` | The raw line received<br />`example: "Hello world"` |
| `timestamp` | `timestamp` | The current time in nanosecond precision. To extract a timestamp from your logs see the [transforms][transforms] section.<br />`example: "2019-05-02T12:31:22.132554431Z"` |

## Delivery Guarantee

Due to nature of ingesting data through the TCP protocol, the `tcp` source
makes a [best effort delivery guarantee][best_effort_delivery].



## How It Works

### Line Delimiters

Each line is read until a new line delimiter (the `0xA` byte) is found.

### Performance

The `tcp` source has been involved in the following performance tests:

* [`file_to_tcp_performance`][file_to_tcp_performance_test]
* [`tcp_to_blackhole_performance`][tcp_to_blackhole_performance_test]
* [`tcp_to_tcp_performance`][tcp_to_tcp_performance_test]

Learn more in the [Performance][performance] sections.

## Troubleshooting

The best place to start with troubleshooting is to check the
[Vector logs][monitoring_logs]. This is typically located at
`/var/log/vector.log`, then proceed to follow the
[Troubleshooting Guide][troubleshooting].

### Getting help

If the [Troubleshooting Guide][troubleshooting] does not resolve your
issue, please:

1. Check for any [open source issues](https://github.com/timberio/vector/issues?q=is%3Aopen+is%3Aissue+label%3A%22Source%3A+tcp%22).
2. [Search the forum][search_forum] for any similar issues.
2. Reach out to the [community][community] for help.

## Resources

* [**Issues**](https://github.com/timberio/vector/issues?q=is%3Aopen+is%3Aissue+label%3A%22Source%3A+tcp%22) - [enhancements](https://github.com/timberio/vector/issues?q=is%3Aopen+is%3Aissue+label%3A%22Source%3A+tcp%22+label%3A%22Type%3A+Enhancement%22) - [bugs](https://github.com/timberio/vector/issues?q=is%3Aopen+is%3Aissue+label%3A%22Source%3A+tcp%22+label%3A%22Type%3A+Bug%22)
* [**Source code**](https://github.com/timberio/vector/tree/master/src/source/tcp.rs)


[log_event]: "../../../about/data-model.md#log"
[transforms]: "../../../usage/configuration/transforms"
[best_effort_delivery]: "../../../about/guarantees.md#best-effort-delivery"
[file_to_tcp_performance_test]: "https://github.com/timberio/vector-test-harness/tree/master/cases/file_to_tcp_performance"
[tcp_to_blackhole_performance_test]: "https://github.com/timberio/vector-test-harness/tree/master/cases/tcp_to_blackhole_performance"
[tcp_to_tcp_performance_test]: "https://github.com/timberio/vector-test-harness/tree/master/cases/tcp_to_tcp_performance"
[performance]: "../../../comparisons/performance.md"
[monitoring_logs]: "../../../administration/moonitoring.md#logs"
[troubleshooting]: "../../../usages/guides/troubleshooting.md"
[search_forum]: "https://forum.vectorproject.io/search?expanded=true"
[community]: "https://vectorproject.io/community"
