# Kubernetes ➡️ Datadog logs sender

Helm chart to set up sending logs from a Kubernetes cluster to Datadog. [Vector](https://vector.dev) is used under the
hood.

This is an example of how to use Vector to send logs to Datadog author couldn't find when
he was trying to set it up.
It's also the author's exercise to learn writing Helm charts.

It is based on Axiom's [instruction](https://axiom.co/docs/send-data/kubernetes) on setting up Vector.

## Features

* Lightweight and fast.
* Supports excluding logs from log collection by service name and log level.

## Installation
1. Create kubernetes secret with Datadog API key:
   ```shell
   kubectl create secret generic datadog-api-key --from-literal=DD_API_KEY=<YOUR_DATADOG_API_KEY>
    ```
2. Add the Helm repository:
   ```shell
   helm repo add kube-logs-datadog-sender https://raw.githubusercontent.com/igor-vovk/kube-logs-datadog-sender/main/helm
   ```
3. Install the chart:
   ```shell
   helm install kube-logs-datadog-sender kube-logs-datadog-sender/kube-logs-datadog-sender
   ```


## Architecture

![Architecture](./docs/architecture-diagram.svg)

Sender-Aggregator pattern is used to send logs to Datadog:

* Senders are deployed on each node in the cluster. They collect logs from the node, process and filter them, and then
  send logs to the aggregator.
* Aggregator collects logs from all senders and then sends them to Datadog.

## Points of Improvement

* Consider having thin senders and doing parsing and filtering in the aggregator instance.

## Referral Links

They help me to pay for the Datadog, so I can see my logs.

* [Hetzner Cloud](https://hetzner.cloud/?ref=iAnthJAtoQ8d) – best cloud provider with the cheapest prices in the EU
* [Bybit](https://www.bybit.nl/invite?ref=EVWANAG) – best crypto exchange