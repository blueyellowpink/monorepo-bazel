# This command tells bazel to load the http_archive rule which is used
# to download other rulesets like rules_rust below
load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

# This pulls down rules_rust
# The path and sha256 come from https://github.com/bazelbuild/rules_rust/releases
http_archive(
    name = "rules_rust",
    sha256 = "950a3ad4166ae60c8ccd628d1a8e64396106e7f98361ebe91b0bcfe60d8e4b60",
    urls = ["https://github.com/bazelbuild/rules_rust/releases/download/0.20.0/rules_rust-v0.20.0.tar.gz"],
)

#What to load and run to setup rust are documented at https://bazelbuild.github.io/rules_rust/
load("@rules_rust//rust:repositories.bzl", "rules_rust_dependencies", "rust_register_toolchains")

rules_rust_dependencies()

rust_register_toolchains(edition = "2021")

### Cargo raze deps
###
load("//third_party/rust:crates.bzl", "raze_fetch_remote_crates")

# Note that this method's name depends on your gen_workspace_prefix setting.
# `raze` is the default prefix.
raze_fetch_remote_crates()

### rules_proto
### Release info from https://github.com/bazelbuild/rules_proto/releases
http_archive(
    name = "rules_proto",
    sha256 = "dc3fb206a2cb3441b485eb1e423165b231235a1ea9b031b4433cf7bc1fa460dd",
    strip_prefix = "rules_proto-5.3.0-21.7",
    urls = [
        "https://github.com/bazelbuild/rules_proto/archive/refs/tags/5.3.0-21.7.tar.gz",
    ],
)
load("@rules_proto//proto:repositories.bzl", "rules_proto_dependencies", "rules_proto_toolchains")
rules_proto_dependencies()
rules_proto_toolchains()

### rules_docker setup
### FROM https://github.com/bazelbuild/rules_docker#setup
###
http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "b1e80761a8a8243d03ebca8845e9cc1ba6c82ce7c5179ce2b295cd36f7e394bf",
    urls = ["https://github.com/bazelbuild/rules_docker/releases/download/v0.25.0/rules_docker-v0.25.0.tar.gz"],
)

load(
    "@io_bazel_rules_docker//repositories:repositories.bzl",
    container_repositories = "repositories",
)
container_repositories()

load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_deps()

load(
    "@io_bazel_rules_docker//container:container.bzl",
    "container_pull",
)

# rust_image
load(
    "@io_bazel_rules_docker//rust:image.bzl",
    _rust_image_repos = "repositories",
)

_rust_image_repos()
