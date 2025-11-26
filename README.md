# DataHaskell Starter

A ready-to-use VS Code Dev Container for doing data science in Haskell with Jupyter notebooks.

This repo is batteries included environment for the DataHaskell ecosystem:
- VS Code + Dev Containers
- IHaskell Jupyter kernel
- DataHaskell libraries (e.g. `dataframe`, `hasktorch`, etc.)
- Example notebooks to get you started

---

## Who is this for?

- You prefer an easy to use, pinned environment over installing everything locally.
- You like notebooks (Jupyter / VS Code) for exploration.

If you’re new to DataHaskell, this is the recommended way to get a working setup.

## Setting up VS Code
You can set up a devcontainer in your current folder by running the command below:

- Linux/MacOS: `curl -sSL https://raw.githubusercontent.com/DataHaskell/datahaskell-starter/refs/heads/main/setup.sh | sh`

When you next open VS Code you should see a modal asking if you want to re-open the project in a devcontainer.

## Running GHCi scripts
`hscript` allows you to run GHCi scripts without a main and with inline imports. It enables writing code like:

```haskell
:set -package text
:set -XOverloadedStrings
:set -XTemplateHaskell

import qualified DataFrame as D
import qualified DataFrame.Functions as F
import Data.Text (Text)
import DataFrame ((|>))
import DataFrame.Functions ((.==), (.>))

-- Read Iris dataset
iris <- D.readParquet "../dataframe/data/iris.parquet"

-- Filter large setosas
iris |>
  D.filterWhere (F.col @Text "variety" .== "Setosa") |>
  D.filterWhere (F.col @Double "sepal.length" .> 5.4)

-- Declare column variables
_ = (); F.declareColumns iris

-- Create a new feature
D.derive "ratio" (sepal_width / sepal_length) iris
```

Linux/MacOS: Download `https://raw.githubusercontent.com/DataHaskell/datahaskell-starter/refs/heads/main/setup.sh` and add it to your PATH.

You can then run files like the one above by typing:

```bash
hscript runme.hs
```

### Example notebooks
Check out the example project in the `notebooks` directory.
---

## Requirements

You’ll need:

- **VS Code**
- **Docker** (Docker Desktop on macOS/Windows, or Docker Engine on Linux)
- VS Code extensions:
  - [Jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter)
  - [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
  - [Haskell](https://marketplace.visualstudio.com/items?itemName=haskell.haskell) (recommended)

You **do not** need to install GHC, Cabal, or IHaskell on your host machine. Everything lives inside the container.
