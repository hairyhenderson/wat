This demonstrates a weird bug I'm running into...

```console
$ go build
# github.com/hairyhenderson/wat/vendor/github.com/grafana/grafana/pkg/log
vendor/github.com/grafana/grafana/pkg/log/log.go:33: cannot use Root.New(params...) (type log15.Logger) as type Logger in return argument:
        log15.Logger does not implement Logger (missing GetHandler method)
# github.com/hairyhenderson/wat/vendor/gopkg.in/macaron.v1
vendor/gopkg.in/macaron.v1/context.go:428: undefined: com.AESGCMEncrypt
vendor/gopkg.in/macaron.v1/context.go:449: undefined: com.AESGCMDecrypt
```

Even if I add the following to `Gopkg.toml`:

```toml
[[override]]
  name = "github.com/inconshreveable/log15"
  branch = "master"
```

`dep ensure` still insists on picking one of the tags, not `master`:


```console
$ dep ensure -update -v
...
ensure Solve(): No versions of github.com/inconshreveable/log15 met constraints:
        v2.11: Could not introduce github.com/inconshreveable/log15@v2.11, as it is not allowed by constraint master from project github.com/grafana/grafana.
        v2.10: Could not introduce github.com/inconshreveable/log15@v2.10, as it is not allowed by constraint master from project github.com/grafana/grafana.
        v2.9: Could not introduce github.com/inconshreveable/log15@v2.9, as it is not allowed by constraint master from project github.com/grafana/grafana.
        v2.8: Could not introduce github.com/inconshreveable/log15@v2.8, as it is not allowed by constraint master from project github.com/grafana/grafana.
        v2.7: Could not introduce github.com/inconshreveable/log15@v2.7, as it is not allowed by constraint master from project github.com/grafana/grafana.
        v2.6: Could not introduce github.com/inconshreveable/log15@v2.6, as it is not allowed by constraint master from project github.com/grafana/grafana.
        v2.5: Could not introduce github.com/inconshreveable/log15@v2.5, as it is not allowed by constraint master from project github.com/grafana/grafana.
        v2.4: Could not introduce github.com/inconshreveable/log15@v2.4, as it is not allowed by constraint master from project github.com/grafana/grafana.
        v2.3: Could not introduce github.com/inconshreveable/log15@v2.3, as it is not allowed by constraint master from project github.com/grafana/grafana.
        v2.2: Could not introduce github.com/inconshreveable/log15@v2.2, as it is not allowed by constraint master from project github.com/grafana/grafana.
        v2.1: Could not introduce github.com/inconshreveable/log15@v2.1, as it is not allowed by constraint master from project github.com/grafana/grafana.
        v2: Could not introduce github.com/inconshreveable/log15@v2, as it is not allowed by constraint master from project github.com/grafana/grafana.
```
