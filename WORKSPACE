###############################################
# Local repositories with RBE configurations. #
###############################################

local_repository(
  name = "rbe_linux_toolchains",
  path = "bazel/toolchains/linux-bazel-4.2.1",
)

local_repository(
  name = "rbe_windows_toolchains",
  path = "bazel/toolchains/windows-bazel-4.2.1",
)

############
# Android. #
############

# Name *must* be "androidndk". The path to the NDK is pulled from $ANDROID_NDK_HOME.
#
# See https://docs.bazel.build/versions/main/android-ndk.html.
android_ndk_repository(
  name = "androidndk",
  api_level = 31,
)

##################################
# Docker rules and dependencies. #
##################################

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "io_bazel_rules_docker",
    sha256 = "1f4e59843b61981a96835dc4ac377ad4da9f8c334ebe5e0bb3f58f80c09735f4",
    strip_prefix = "rules_docker-0.19.0",
    urls = ["https://github.com/bazelbuild/rules_docker/releases/download/v0.19.0/rules_docker-v0.19.0.tar.gz"],
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

# Pulls the Docker image used as the base for SkCMS's Linux RBE toolchain container image.
container_pull(
    name = "ubuntu1804",
    digest = "sha256:e006d8c083684299f1726b47361bfe5acfa0638a226e98b957681a2d135fbd40",
    registry = "gcr.io",
    repository = "cloud-marketplace/google/ubuntu1804",
)