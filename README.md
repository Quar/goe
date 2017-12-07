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
wget quar.github.io/goe/goe -O /path/included/in/PATH/goe
```

#### Usage:

``` bash
goe env [variable] -- show go env
goe run main.go -- run go project as if it was under `$GOPATH/src`
goe build -- go build current project
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


