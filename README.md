# Why this Fork?
In [rust_q_sim](https://github.com/Janekdererste/rust_q_sim) I am using metis-rs as a dependency. Since this crate is a Binding to the Metis-C-Library, the metis-sys crate has a dependency on `bindgen v0.58`. The `rust_q_sim` project also has a dependency on the `rsmpi` crate which itself is a wrapper for the MPI-C api. This project also uses `bindgen` but with `v0.60`. This version conflict resulted in build errors, where `libclan` wasn't loaded correctly. With this fork I changed the `libgen` dependency to `v0.60` to match the one in `rsmpi`. I didn't make a PR into the upstream repository, since the current version of bindgen is `v0.63` which means both, `metis-rs` and `rsmpi` are using outated versions. Since the `metis-rs` repo is quite stable I would think that this is ok for now. 

# metis-rs

Idiomatic bindings to [libmetis][METIS], a graph and mesh partitioner.

## Building

Prerequisites:

- METIS
- clang v3.9 or above

Bindings to METIS are made on the fly.  If METIS is installed in a non-standard
location, please use the following commands:

    export METISDIR=path/to/your/metis/installation
    export CPATH="$METISDIR/include"
    export RUSTFLAGS="-L$METISDIR/lib"

The environment variable `$METISDIR` must point to a directory containing a
`lib/` and a `include/` directory containing the shared libraries and the
headers of METIS, respectively.

Once these variables are set, you can build the bindings with `cargo build`.

### Build the documentation

If your METIS installation lies in a non-standard path, you will need to set
the `RUSTDOCFLAGS` environment variable to build the documentation:

    export RUSTDOCFLAGS="-L$METISDIR/lib"

Then you can call `cargo doc --no-deps --open`.

## License

This program is distributed under the terms of both the MIT license and the
Apache License (Version 2.0).  See `LICENSE-APACHE` and `LICENSE-MIT` for
details.

[METIS]: http://glaros.dtc.umn.edu/gkhome/metis/metis/overview
