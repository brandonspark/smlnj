# Standard ML of New Jersey

This is the main development repository for **SML/NJ**.  We are
currently reworking many components of the system, so it is not
very stable.  For most uses, we recommend the
[legacy version](https://github.com/smlnj/legacy) of the system.

Currently, only Intel-based Macs are known to work.

---

## Contents

- [Building From Source](#building-from-source)
- [Recompiling the System](#recompiling-the-system)

---

## Building From Source

The process for building the system from source code has
changed.

1. clone the repository
    ``` bash
    git clone git@github.com:smlnj/smlnj.git
    ```

2. `cd` to the cloned repository and get the boot files
    ``` bash
    cd smlnj
    curl -O https://smlnj.org/dist/working/$VERSION/boot.amd64-unix.tgz
    ```
    where `$VERSION` is the version that you are building (*e.g.*, `2022.1`).

    We plan to incorporate this step into the [`build.sh`](build.sh) script in the near future.

3. build the installation
    ``` bash
    ./build.sh
    ```
    Use `build.sh -h` to see the list of options accepted by the build script.

    As before, you can modify the [`config/targets`](config/targets) file to add/remove components
    from the build.

After successful running of the [`build.sh`](build.sh) script, `bin/sml` will be the interactive
system.

## Recompiling the System

The process of recompiling the system from source code is fairly similar
to before.

1. Switch to the [`system`](system/) directory and run the `cmb-make` command:
    ``` bash
    cd system
    ./cmb-make ../bin/sml
    ```

    The "`../bin/sml`" argument is optional; if omitted, then the `sml` command in the
    user's `PATH` will be used.  Once can also specify a different path to an `sml`
    command, when appropriate.

2. Bootstrap the system
    ``` bash
    ./makeml
    ```

3. Install the system
    ``` bash
    ./installml -clean -boot
    ```
    The `-boot` option is new (and optional); it causes the existing boot files in the root
    directory (*e.g.*, `boot.amd64-unix.tgz`) to be replaced by the files generated by the
    `cmb-make` command.

4. Rebuild the libraries and tools
    ``` bash
    cd ..
    ./build.sh
    ```

