# mergo

Package mergo merges same-type structs and maps by setting default values in zero-value fields.

Mergo won't merge unexported (private) fields but will do recursively any exported one. It also
won't merge structs inside maps (because they are not addressable using Go reflection).

#### Usage

From my own work-in-progress project:

```go
type networkConfig struct {
	Protocol string
	Address string
	ServerType string `json: "server_type"`
	Port uint16
}

type FssnConfig struct {
	Network networkConfig
}

var fssnDefault = FssnConfig {
	networkConfig {
		"tcp",
		"127.0.0.1",
		"http",
		31560,
	},
}

// Inside a function [...]

if err := mergo.Merge(&config, fssnDefault); err != nil {
	log.Error(err)
}

// More code [...]
```


---

Created by [goreadme](https://github.com/apps/goreadme)
