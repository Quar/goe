goe
=======
A gopher's meddling on developing Golang project "outside" of `$GOPATH`.

*Note: this is a prototype, still under improvement.*

Normally Golang expects gophers to put projects under `$GOPATH/src`, which
by default looks like `$HOME/.go/src`. Thus every project will have working
directory looks like `$HOME/.go/src/my_go_package_project`.

For no reason a gopher may want to develop a Golang project located at, say
`$HOME/git_code/my_go_package_project`, which can host git-repository and
published naturally.


`goe` is a gophers hope to make this happen.

#### Install:

``` bash
wget -4 quar.github.io/goe/goe -O /path/included/in/PATH/goe
chmod u+x /path/included/in/PATH/goe
```

#### Usage (same as `go`):

``` bash
goe env [variable] -- show go env
goe run main.go -- run go project as if it was under `$GOPATH/src`
goe build -- go build current project
goe get -- get libs
goe test -- test
goe list -- list packages
```

#### Note:

  run `goe` inside go project root folder like this

```
  my-go-project/
      main.go
      vendor/
          folder1/
              package1/
                  package1-code.go
          package2/
              package2-code.go
```

  where within `main.go`, one can import packages like:

``` go
import (
    "fmt"

    "folder1/package1"
    "package2"
)
```

#### Caveats:

  `goe` meddles `$GOPATH` by using `GOPATH=$HOME/.go.local/`, and then create
  simlink of current project directory under `$HOME/.go.local/`, which allows
  go-tools to do path searching, as if this project was created under
  `$GOPATH/src`.


<a href="https://github.com/Quar/goe"><img style="position: absolute; top: 0; border: 0; right: 0;" src="data:image/png;base64,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"/></a>

