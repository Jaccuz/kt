# kt - a Kafka tool

Mostly for consuming messages at the moment. Allows to consume messages at specific offsets and produces output that can be further processed via producer [counterpart](https://github.com/echojc/kp) or via tools like [jq](https://stedolan.github.io/jq/).

## Example usage:

    $ kt -help
    Usage of kt:
      -brokers string
            Comma separated list of brokers. (default "localhost:9092")
      -json
            Print output in JSON format.
      -offset string
            Colon separated offsets where to start and end reading messages.
      -topic string
            Topic to consume.
    $ kt -topic kt-test
    Partition=0 Offset=0 Key= Message=Hello, World 0
    Partition=0 Offset=1 Key= Message=Hallo, Welt
    Partition=0 Offset=2 Key= Message=Bonjour, monde
    ^C2016/01/26 06:29:19 Received interrupt - shutting down...
    $ kt -topic kt-test -offset 1:
    Partition=0 Offset=1 Key= Message=Hallo, Welt
    Partition=0 Offset=2 Key= Message=Bonjour, monde
    ^C2016/01/26 06:29:29 Received interrupt - shutting down...
    $ kt -topic kt-test -offset 1:1
    Partition=0 Offset=1 Key= Message=Hallo, Welt
    $ kt -topic kt-test -json
    {"partition":0,"offset":0,"key":"","message":"Hello, World 0"}
    $

## Installation

You can download kt via the [Releases](https://github.com/fgeller/kt/releases) section.

Alternatively, the usual way via the go tool, for example:

    $ GO15VENDOREXPERIMENT=1 go install github.com/fgeller/kt