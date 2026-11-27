<!--    
    ================================================================================================
    README.md
    ================================================================================================
-->

# Libertinus Conda Recipes

*Conda recipes for the Libertinus font family, plus the pixi configurations to build and install them straight from git.*

<!--    
    ================================================================================================
-->

## Project Structure

```sh
conda-recipe-libertinus/
├── otf/                    # Conda recipe for the static OpenType fonts of the
│   │                       # Libertinus family. Installs the `.otf` files into
│   │                       # `share/fonts/otf/` of the target environment.
│   │
│   ├── pixi.toml           # Pixi package manifest declaring the
│   │                       # `pixi-build-rattler-build` backend, so pixi can
│   │                       # build this recipe from a git dependency.
│   │
│   └── recipe.yaml         # Recipe in the v1 format: upstream release
│                           # source with checksum, install script, and
│                           # package metadata.
│
├── ttf/                    # Conda recipe for the static TrueType fonts.
│   │                       # Mirrors `otf/` and installs the `.ttf` files into
│   │                       # `share/fonts/ttf/`.
│   │
│   ├── pixi.toml
│   └── recipe.yaml
│
└── woff2/                  # Conda recipe for the static WOFF2 web fonts.
    │                       # Mirrors `otf/` and installs the `.woff2` files into
    │                       # `share/fonts/woff2/`.
    │
    ├── pixi.toml
    └── recipe.yaml
```

## Installation as a Dependency

### I. Prerequisites

| **Component**               | **Requirement**  |
| :-------------------------- | :--------------- |
| **Operating System**        | `Unix`-like [^1] |
| **Package Management Tool** | [`Pixi`](https://pixi.prefix.dev/latest/#installation) with `pixi-build` feature enabled |

[^1]: Build scripts rely on a POSIX-compliant shell.

<!--    
    ================================================================================================
-->

### II. Adding a package

- To add the OpenType (OTF) package, run:

    ```sh
    pixi add \
        --git https://github.com/snegoviol/libertinus-conda-recipes \
        --rev 0f3101bdf9b3eb4dfc6c2418990922d6488bef51 \
        --subdirectory otf \
        libertinus-otf
    ```

- To add the TrueType (TTF) package, run:

    ```sh
    pixi add \
        --git https://github.com/snegoviol/libertinus-conda-recipes \
        --rev 0f3101bdf9b3eb4dfc6c2418990922d6488bef51 \
        --subdirectory ttf \
        libertinus-ttf
    ```

- To add the WOFF2 package, run:

    ```sh
    pixi add \
        --git https://github.com/snegoviol/libertinus-conda-recipes \
        --rev 0f3101bdf9b3eb4dfc6c2418990922d6488bef51 \
        --subdirectory woff2 \
        libertinus-woff2
    ```

### III. Usage

Once the package is installed, the fonts are placed in the `$CONDA_PREFIX/share/fonts/<format>/` directory of your active environment, and you can start using them in your project.

For example, to use these fonts in a Typst project managed by Pixi:

1. Add the font path to your `pixi.toml` to ensure the Typst compiler can locate these fonts:

    ```toml
    [activation.env]
    TYPST_FONT_PATHS = "$CONDA_PREFIX/share/fonts"
    ```

2. Reference the font in your Typst document:

    ```typst
    #set text(font: "Libertinus Sans")
    ```

<!--    
    ================================================================================================
-->

## License

Each file in this repository is licensed under the [MIT No Attribution License](LICENSE.txt).

<!--    
    ================================================================================================
-->
