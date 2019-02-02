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

git_repository(
    name = "com_github_amitarya_rules_boost",
    commit = "d6446dc9de6e43b039af07482a9361bdc6da5237",
    remote = "git@github.com:amitarya/rules_boost",
)


load("@com_github_amitarya_rules_boost//:boost/boost.bzl", "boost_deps")
boost_deps()

# gprc library Release v1.18.0
http_archive(
    name = "com_github_grpc_grpc",
    sha256 = "ccd0ae47b2024bfea0aef452b6025815f8a92070bedda08317bf5e7519cb6fb3",
    urls = [
        "https://github.com/grpc/grpc/archive/007b721f8045ceef4ebf418a2935ab772fbe3708.tar.gz",
    ],
    strip_prefix = "grpc-007b721f8045ceef4ebf418a2935ab772fbe3708",
)

load("@com_github_grpc_grpc//:bazel/grpc_deps.bzl", "grpc_deps")
grpc_deps()
