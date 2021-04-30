load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

version = "0.17.0"

http_archive(
    name = "io_bazel_rules_docker",
    strip_prefix = "rules_docker-%s" % version,
    urls = [
        "https://github.com/bazelbuild/rules_docker/releases/download/v%s/rules_docker-v%s.tar.gz" % (version, version)
    ],
)

load("@io_bazel_rules_docker//repositories:repositories.bzl", container_repositories = "repositories")

container_repositories()

load("@io_bazel_rules_docker//repositories:deps.bzl", container_deps = "deps")

container_deps()

load(
    "@io_bazel_rules_docker//java:image.bzl",
    _java_image_repos = "repositories",
)

_java_image_repos()
