# Go-Nmap

Go-Nmap is a Go library designed for parsing Nmap XML data into structured and easy-to-use Go structs. It simplifies the process of working with Nmap scan results programmatically.

## Features

- Comprehensive mapping of Nmap XML data to Go structs.
- Easy integration with Go applications.
- Supports various Nmap scan data including host details, ports, services, OS information, and more.

## Installation

To use Go-Nmap in your project, you can install it using `go get`:

```bash
$ go get github.com/tomsteele/go-nmap
```

## Documentation

The library's documentation is available at [GoDoc](http://godoc.org/github.com/tomsteele/go-nmap).

## Usage

Here is an example of how to use Go-Nmap to parse Nmap XML data:

```go
package main

import (
    "fmt"
    "io/ioutil"
    "github.com/tomsteele/go-nmap"
)

func main() {
    // Load the XML data from a file
    data, err := ioutil.ReadFile("scan.xml")
    if err != nil {
        panic(err)
    }

    // Parse the XML data
    nmapRun, err := nmap.Parse(data)
    if err != nil {
        panic(err)
    }

    // Access parsed data
    fmt.Printf("Nmap Scanner: %s\n", nmapRun.Scanner)
    fmt.Printf("Number of Hosts: %d\n", len(nmapRun.Hosts))
}
```

## API Overview

The library provides a rich set of types and functions for accessing Nmap scan data. Below is a summary of the primary types and their purposes:

### Core Types

- **`NmapRun`**: Contains all data for a single Nmap scan.
  - Example: `nmapRun.Hosts` to access scanned hosts.
- **`Host`**: Represents a single host in the scan results.
  - Example: `host.Addresses` to get the host's IP addresses.
- **`Port`**: Provides details about scanned ports.
  - Example: `port.Service` to get the service running on the port.
- **`Os`**: Contains fingerprinted operating system details.

### Functions

- **`Parse(content []byte) (*NmapRun, error)`**: Parses Nmap XML data into an `NmapRun` struct.

### Example Structs

#### Host

```go
type Host struct {
    StartTime     Timestamp     `xml:"starttime,attr" json:"starttime"`
    EndTime       Timestamp     `xml:"endtime,attr" json:"endtime"`
    Status        Status        `xml:"status" json:"status"`
    Addresses     []Address     `xml:"address" json:"addresses"`
    Ports         []Port        `xml:"ports>port" json:"ports"`
    Os            Os            `xml:"os" json:"os"`
}
```

#### Port

```go
type Port struct {
    Protocol string   `xml:"protocol,attr" json:"protocol"`
    PortId   int      `xml:"portid,attr" json:"id"`
    State    State    `xml:"state" json:"state"`
    Service  Service  `xml:"service" json:"service"`
}
```

## Contributing

We welcome contributions from the community! If you find a bug, have a feature request, or want to contribute code:

1. Fork the repository.
2. Create a new branch for your changes.
3. Submit a pull request with a detailed explanation of your changes.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.


## Resources

- [Nmap Official Website](https://nmap.org/)
- [Nmap XML Output Format](https://nmap.org/book/output-formats-xml-output.html)
- [Go Programming Language](https://go.dev/)


