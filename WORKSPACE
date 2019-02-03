load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")
load("@bazel_tools//tools/build_defs/repo:git.bzl", "git_repository")

# proto_library, cc_proto_library, and java_proto_library rules implicitly
# depend on @com_google_protobuf for protoc and proto runtimes.
# This statement defines the @com_google_protobuf repo.
http_archive(
    name = "com_google_protobuf",
    strip_prefix = "protobuf-3.6.1.2",
    urls = ["https://github.com/amitarya/protobuf/archive/v3.6.1.2.zip"],
)
# java_lite_proto_library rules implicitly depend on @com_google_protobuf_javalite//:javalite_toolchain,
# which is the JavaLite proto runtime (base classes and common utilities).
http_archive(
    name = "com_google_protobuf_javalite",
    sha256 = "d8a2fed3708781196f92e1e7e7e713cf66804bd2944894401057214aff4f468e",
    strip_prefix = "protobuf-5e8916e881c573c5d83980197a6f783c132d4276",
    urls = ["https://github.com/google/amitarya/archive/protobuf-5e8916e881c573c5d83980197a6f783c132d4276.zip"],
)
#
#================================================================
# Boost.
#================================================================
git_repository(
    name = "com_github_amitarya_rules_boost",
    commit = "d6446dc9de6e43b039af07482a9361bdc6da5237",
    remote = "git@github.com:amitarya/rules_boost",
)

load("@com_github_amitarya_rules_boost//:boost/boost.bzl", "boost_deps")
boost_deps()
#================================================================
# Protobuf/GRPC
#================================================================
git_repository(
    name = "com_github_amitarya_rules_protobuf",
    commit = "5f6195e83e06db2fd110626b0f2dc64e345e6618",
    remote = "git@github.com:amitarya/rules_protobuf",
)

load("@com_github_amitarya_rules_protobuf//protobuf:rules.bzl", "github_archive")


# ================================================================
# Python GRPC support requires rules_python
# ================================================================

github_archive(
    name = "io_bazel_rules_python",
    commit = "8b5d0683a7d878b28fffe464779c8a53659fc645",
    org = "bazelbuild",
    repo = "rules_python",
    sha256 = "40499c0a9d55f0c5deb245ed24733da805f05aaf6085cb39027ba486faf1d2e1",
)

load("@io_bazel_rules_python//python:pip.bzl", "pip_repositories", "pip_import")

pip_repositories()

pip_import(
   name = "pip_grpcio",
   requirements = "@com_github_amitarya_rules_protobuf//python:requirements.txt",
)

load("@pip_grpcio//:requirements.bzl", pip_grpcio_install = "pip_install")

pip_grpcio_install()

load("@com_github_amitarya_rules_protobuf//python:rules.bzl", "py_proto_repositories")
py_proto_repositories()

# gprc library Release v1.18.0
http_archive(
    name = "com_google_grpc",
    sha256 = "ccd0ae47b2024bfea0aef452b6025815f8a92070bedda08317bf5e7519cb6fb3",
    urls = [
        "https://github.com/grpc/grpc/archive/007b721f8045ceef4ebf418a2935ab772fbe3708.tar.gz",
    ],
    strip_prefix = "grpc-007b721f8045ceef4ebf418a2935ab772fbe3708",
)

load("@com_google_grpc//:bazel/grpc_deps.bzl", "grpc_deps")
grpc_deps()
load("@com_github_amitarya_rules_protobuf//ruby:rules.bzl", "ruby_proto_repositories")

ruby_proto_repositories()
#

#new_http_archive(
#    name = "six_archive",
#    build_file = "@com_google_protobuf//:six.BUILD",
#    sha256 = "105f8d68616f8248e24bf0e9372ef04d3cc10104f1980f54d57b2ce73a5ad56a",
#    url = "https://pypi.python.org/packages/source/s/six/six-1.10.0.tar.gz#md5=34eed507548117b2ab523ab14b2f8b55",
#)
#
#bind(
#    name = "six",
#    actual = "@six_archive//:six",
#)
