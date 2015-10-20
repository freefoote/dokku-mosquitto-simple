# dokku mosquitto-simple

A simple mosquitto plugin for Dokku. "Simple" because it doesn't use TLS,
nor expose web sockets with the default image.

The original intention of this plugin is to provide an MQTT broker
to connect some Arduino controllers and Node-red running in the cloud.
To enable the outside controllers to connect, expose the port on the host:

    $ dokku mosquitto-simple:expose <service> 1883

It is based off the official Dokku Postgres plugin, with the exception
that it can't export or import data, as that doesn't make much sense for
this.

## Authentication

Authentication is enabled in the default docker image using a password
generated at create time. The username is always "admin". You can't currently
set ACLs or add additional users.

## Environment

The target container gets an MQTT_URL environment variable in the format
mqtt://admin:PASSWORD@IP/, that you can use to connect inside your app.

You can see the password with:

    $ dokku mosquitto-simple:info

## Requirements

- dokku 0.4.0+
- docker 1.8.x

