---
last_modified_on: "2020-04-05"
delivery_guarantee: "best_effort"
component_title: "Syslog"
description: "The Vector `syslog` source ingests data through the Syslog protocol and outputs `log` events."
event_types: ["log"]
function_category: "receive"
issues_url: https://github.com/timberio/vector/issues?q=is%3Aopen+is%3Aissue+label%3A%22source%3A+syslog%22
operating_systems: ["Linux","MacOS","Windows"]
sidebar_label: "syslog|[\"log\"]"
source_url: https://github.com/timberio/vector/tree/master/src/sources/syslog.rs
status: "prod-ready"
title: "Syslog Source"
unsupported_operating_systems: []
---

import Alert from '@site/src/components/Alert';
import Fields from '@site/src/components/Fields';
import Field from '@site/src/components/Field';
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

The Vector `syslog` source
ingests data through the [Syslog protocol][urls.syslog_5424] and outputs
[`log`][docs.data-model.log] events.

<!--
     THIS FILE IS AUTOGENERATED!

     To make changes please edit the template located at:

     website/docs/reference/sources/syslog.md.erb
-->

## Requirements

<Alert icon={false} type="danger" classNames="list--warnings">

* This component exposes a configured port. You must ensure your network allows access to this port.

</Alert>

## Configuration

<Tabs
  block={true}
  defaultValue="common"
  values={[{"label":"Common","value":"common"},{"label":"Advanced","value":"advanced"}]}>

<TabItem value="common">

```toml title="vector.toml"
[sources.my_source_id]
  type = "syslog" # required
  address = "0.0.0.0:514" # required, required when mode = "tcp" or mode = "udp"
  mode = "tcp" # required
  path = "/path/to/socket" # required, required when mode = "unix"
```

</TabItem>
<TabItem value="advanced">

```toml title="vector.toml"
[sources.my_source_id]
  # General
  type = "syslog" # required
  address = "0.0.0.0:514" # required, required when mode = "tcp" or mode = "udp"
  mode = "tcp" # required
  path = "/path/to/socket" # required, required when mode = "unix"
  max_length = 102400 # optional, default, bytes

  # Context
  host_key = "host" # optional, default

  # TLS
  tls.ca_path = "/path/to/certificate_authority.crt" # optional, no default
  tls.crt_path = "/path/to/host_certificate.crt" # optional, no default
  tls.enabled = false # optional, default
  tls.key_pass = "${KEY_PASS_ENV_VAR}" # optional, no default
  tls.key_path = "/path/to/host_certificate.key" # optional, no default
  tls.verify_certificate = false # optional, default
```

</TabItem>
</Tabs>

<Fields filters={true}>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["0.0.0.0:514","systemd","systemd#2"]}
  groups={[]}
  name={"address"}
  path={null}
  relevantWhen={{"mode":["tcp","udp"]}}
  required={true}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### address

The TCP or UDP address to listen for connections on, or "systemd#N" to use the
Nth socket passed by systemd socket activation.




</Field>
<Field
  common={false}
  defaultValue={"host"}
  enumValues={null}
  examples={["host"]}
  groups={[]}
  name={"host_key"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### host_key

The key name added to each event representing the current host. This can also
be globally set via the [global [`host_key`](#host_key)
option][docs.reference.global-options#host_key].

 See [Context](#context) for more info.


</Field>
<Field
  common={false}
  defaultValue={102400}
  enumValues={null}
  examples={[102400]}
  groups={[]}
  name={"max_length"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"int"}
  unit={"bytes"}
  warnings={[]}
  >

### max_length

The maximum bytes size of incoming messages before they are discarded.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={{"tcp":"Read incoming Syslog data over the TCP protocol.","udp":"Read incoming Syslog data over the UDP protocol.","unix":"Read uncoming Syslog data through a Unix socker."}}
  examples={["tcp","udp","unix"]}
  groups={[]}
  name={"mode"}
  path={null}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### mode

The input mode.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["/path/to/socket"]}
  groups={[]}
  name={"path"}
  path={null}
  relevantWhen={{"mode":"unix"}}
  required={true}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### path

The unix socket path. *This should be absolute path.*




</Field>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[]}
  groups={[]}
  name={"tls"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"table"}
  unit={null}
  warnings={[]}
  >

### tls

Configures the TLS options for connections from this source.



<Fields filters={false}>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={["/path/to/certificate_authority.crt"]}
  groups={[]}
  name={"ca_path"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

#### ca_path

Absolute path to an additional CA certificate file, in DER or PEM format
(X.509).




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["/path/to/host_certificate.crt"]}
  groups={[]}
  name={"crt_path"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

#### crt_path

Absolute path to a certificate file used to identify this server, in DER or PEM
format (X.509) or PKCS#12. If this is set and is not a PKCS#12 archive,
`key_path` must also be set. This is required if [`enabled`](#enabled) is set to `true`.




</Field>
<Field
  common={true}
  defaultValue={false}
  enumValues={null}
  examples={[false,true]}
  groups={[]}
  name={"enabled"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"bool"}
  unit={null}
  warnings={[]}
  >

#### enabled

Require TLS for incoming connections. If this is set, an identity certificate
is also required.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["${KEY_PASS_ENV_VAR}","PassWord1"]}
  groups={[]}
  name={"key_pass"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

#### key_pass

Pass phrase used to unlock the encrypted key file. This has no effect unless
`key_path` is set.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["/path/to/host_certificate.key"]}
  groups={[]}
  name={"key_path"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

#### key_path

Absolute path to a certificate key file used to identify this server, in DER or
PEM format (PKCS#8).




</Field>
<Field
  common={false}
  defaultValue={false}
  enumValues={null}
  examples={[false,true]}
  groups={[]}
  name={"verify_certificate"}
  path={"tls"}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"bool"}
  unit={null}
  warnings={[]}
  >

#### verify_certificate

If `true`, Vector will require a TLS certificate from the connecting host and
terminate the connection if it is not valid. If `false` (the default), Vector
will ignore the presence of a client certificate.




</Field>
</Fields>

</Field>
</Fields>

## Fields

The `syslog` source ingests data through the [Syslog protocol][urls.syslog_5424] and outputs [`log`][docs.data-model.log] events.
For example:

```javascript
{
  "appname": "app-name",
  "facility": "1",
  "host": "my.host.com",
  "message": "<13>Feb 13 20:07:26 74794bfb6795 root[8539]: i am foobar",
  "msgid": "ID47",
  "procid": "8710",
  "severity": "notice",
  "timestamp": "2019-11-01T21:15:47+00:00",
  "version": 1,
  "custom_field1": "custom value 1"
}
```

More detail on the output schema is below.

<Fields filters={true}>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={["app-name"]}
  groups={[]}
  name={"appname"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### appname

The appname extracted from the Syslog formatted line. If a appname is not
found, then the key will not be added.




</Field>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={["1"]}
  groups={[]}
  name={"facility"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### facility

The facility extracted from the Syslog line. If a facility is not found, then
the key will not be added.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["my.host.com"]}
  groups={[]}
  name={"host"}
  path={null}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### host

The hostname extracted from the Syslog line. If a hostname is not found, then
Vector will use the upstream hostname. In the case where [`mode`](#mode) = `"unix"` the
socket path will be used. This key can be renamed via the [`host_key`](#host_key) option.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["<13>Feb 13 20:07:26 74794bfb6795 root[8539]: i am foobar"]}
  groups={[]}
  name={"message"}
  path={null}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### message

The raw message, unaltered.

 See [Parsing](#parsing) for more info.


</Field>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={["ID47"]}
  groups={[]}
  name={"msgid"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### msgid

The msgid extracted from the Syslog line. If a msgid is not found, then the key
will not be added.




</Field>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={["8710"]}
  groups={[]}
  name={"procid"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### procid

The procid extracted from the Syslog line. If a procid is not found, then the
key will not be added.




</Field>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={["notice"]}
  groups={[]}
  name={"severity"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"string"}
  unit={null}
  warnings={[]}
  >

### severity

The severity extracted from the Syslog line. If a severity is not found, then
the key will not be added.




</Field>
<Field
  common={true}
  defaultValue={null}
  enumValues={null}
  examples={["2019-11-01T21:15:47+00:00"]}
  groups={[]}
  name={"timestamp"}
  path={null}
  relevantWhen={null}
  required={true}
  templateable={false}
  type={"timestamp"}
  unit={null}
  warnings={[]}
  >

### timestamp

The timestamp extracted from the incoming line. If a timestamp is not found,
then Vector will use the current time.




</Field>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[1]}
  groups={[]}
  name={"version"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"int"}
  unit={null}
  warnings={[]}
  >

### version

The version extracted from the Syslog line. If a version is not found, then the
key will not be added.




</Field>
<Field
  common={false}
  defaultValue={null}
  enumValues={null}
  examples={[{"custom_field1":"custom value 1"}]}
  groups={[]}
  name={"`[field-name]`"}
  path={null}
  relevantWhen={null}
  required={false}
  templateable={false}
  type={"*"}
  unit={null}
  warnings={[]}
  >

### `[field-name]`

In addition to the defined fields, any Syslog 5424 structured fields are parsed
and inserted as root level fields.




</Field>
</Fields>

## Examples

Given the following [Syslog 5424][urls.syslog_5424] log line:

```text
<13>1 2020-03-13T20:45:38.119Z dynamicwireless.name non 2426 ID931 [exampleSDID@32473 iut="3" eventSource= "Application" eventID="1011"] Try to override the THX port, maybe it will reboot the neural interface!
```

A `log` event will be produced with the following structure:

```javascript
{
  "severity": "notice",
  "facility": "user",
  "timestamp": "2020-03-13T20:45:38.119Z",
  "host": "dynamicwireless.name", // controlled via the [`host_key`](#host_key) option,
  "appname": "non",
  "procid": "2426",
  "msgid": "ID931",
  "iut": "3",
  "eventSource": "Application",
  "eventID": "1011",
  "message": "Try to override the THX port, maybe it will reboot the neural interface!"
}
```

## How It Works

### Context

By default, the `syslog` source will add context
keys to your events via the [`host_key`](#host_key)
options.

### Environment Variables

Environment variables are supported through all of Vector's configuration.
Simply add `${MY_ENV_VAR}` in your Vector configuration file and the variable
will be replaced before being evaluated.

You can learn more in the
[Environment Variables][docs.configuration#environment-variables] section.

### Line Delimiters

Each line is read until a new line delimiter (the `0xA` byte) is found.

### Parsing

Vector makes a _best effort_ to parse the various Syslog formats out in the
wild. This includes [RFC 5424][urls.syslog_5424], [RFC 3164][urls.syslog_3164],
and other common variations (such as the Nginx Syslog style). It's unfortunate
that the Syslog specification is not more accurately followed, but we hope
Vector insulates you from these diviations.

If parsing fails, Vector will include the entire Syslog line in the [`message`](#message)
key. If you find this happening often, we recommend using the
[`socket` source][docs.sources.socket] combined with the
[`regex_parser` transform][docs.transforms.regex_parser] to implement your own
ingestion and parsing scheme. Or, [open an issue][urls.new_feature_request]
requesting support for your specific format.


[docs.configuration#environment-variables]: /docs/setup/configuration/#environment-variables
[docs.data-model.log]: /docs/about/data-model/log/
[docs.reference.global-options#host_key]: /docs/reference/global-options/#host_key
[docs.sources.socket]: /docs/reference/sources/socket/
[docs.transforms.regex_parser]: /docs/reference/transforms/regex_parser/
[urls.new_feature_request]: https://github.com/timberio/vector/issues/new?labels=type%3A+new+feature
[urls.syslog_3164]: https://tools.ietf.org/html/rfc3164
[urls.syslog_5424]: https://tools.ietf.org/html/rfc5424
