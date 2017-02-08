# Cog

[Cog](https://operable.io) is a ChatOps platform with some really great access control features, and allows writing additional functionality in any language.

This chart is still alpha and will not include a Postgres database container until Helm includes a means of excluding dependent subcharts during deployment.

In the mean time, deploying the [Postgres](https://github.com/kubernetes/charts/tree/master/stable/postgresql) chart from the Kubernetes charts repository will provide a small testing database for Cog's use.

## TL;DR;

```bash
$ git clone https://github.com/ohaiwalt/cog-helm cog
$ helm install cog
```

## Introduction

This chart bootstraps a [Cog](https://github.com/operable/cog) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites

- Kubernetes 1.4+ with Beta APIs enabled
- External Postgresql database
- Slack API token

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release cog-helm
```

The command deploys Cog on the Kubernetes cluster in the default configuration.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables lists the required configuration variables. See the [values.yml](values.yml) file for more detailed information.

| Parameter                  | Description                                | Default                                                    |
| -----------------------    | ----------------------------------         | ---------------------------------------------------------- |
| `cog.secrets.slackAPIToken`                   | API Token for connecting to Slack | None |
| `cog.secrets.databaseURL`                | Database connection string | `ecto://cog:cog@postgres:5432/cog` |
| `relay.config.relay-id` | Relay Id | `00000000-0000-0000-0000-000000000000`


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set cog.secrets.slackAPIToken=token,cog.secrets.databaseURL=connection,relay.config.relay-id=$(uuidgen | tr '[:upper:]' '[:lower:]') \
    cog-helm
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml cog-helm
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Persistence

The [Cog](https://github.com/operable/cog) image stores configuration data and configurations in an external PostgreSQL database. This chart currently does not run a database.
