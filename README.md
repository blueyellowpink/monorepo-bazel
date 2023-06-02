# Monorepo Bazel
https://heeten.github.io/hello-monorepo-bazel/index.html

## Run
- Run test (or run all tests)
```bash
bazel test //src/summation:src_summation
( bazel test //... )
```

- Build Rust library
```bash
bazel build //src/summation:src_summation
```

- Run bin
```bash
bazel run //src/summation:executable
bazel run //src/summation:executable -- f64 1 2 3.0
bazel run -c opt //src/summation:executable (run with `--release` flag)
```

## Pulling external crates using cargo-raze
- Install cargo-raze
```bash
cargo install cargo-raze
```

- Run cargo-raze
```bash
cd third_party/rust
cargo raze
```

## Run the gRPC server
```bash
bazel run -c opt //src/services/summation:server

```

- Use `grpcurl` to test
```bash
grpcurl -proto src/proto/summation/summation.proto -plaintext -d '{"value": 5.0, "value": 2.0}' localhost:50051 src_proto_summation.Summation/ComputeSumF64
```
