package(default_visibility = ["//visibility:public"])

load("@com_github_amitarya_rules_protobuf//python:rules.bzl", "py_proto_library")
load("@com_github_amitarya_rules_protobuf//cpp:rules.bzl", "cc_proto_library")
load("@pip_grpcio//:requirements.bzl", "requirement")
load("@io_bazel_rules_python//python:python.bzl", "py_binary", "py_library")

filegroup (
    name = "protos",
    srcs = [
        "helloworld.proto",
    ])

py_proto_library(
    name = "helloworld_pby",
    protos = [":protos"],
    verbose = 0,
    with_grpc = True,
)

py_binary(
    name = "greeter_client",
    srcs = [
        "greeter_client.py",
    ],
    deps = [
        "//experimentation/rpc:helloworld_pby",
        requirement("grpcio"),
        requirement("protobuf"),
    ],
)

py_binary(
    name = "greeter_server",
    srcs = [":grpc_server"],
)

py_test(
    name = "test_greeter_server",
    srcs = ["test_greeter_server.py"],
    deps = [":grpc_server"],
    size = "small",
)

# This library is necessary for creating py_test cases o/w if we explicitly add
# "//examples/helloworld/proto:py" in the 'deps' list then bazel complains with:
# "'//examples/helloworld/proto:py' does not have mandatory provider 'py'".
# It's also useful for packaging all the server code in a lib to reuse for the :greeter_server.
py_library(
    name = "grpc_server",
    srcs = [
        "greeter_server.py",
    ],
    deps = [
        "//experimentation/rpc:helloworld_pby",
        requirement("grpcio"),
        requirement("protobuf"),
    ],
)
#load("@com_google_protobuf//:protobuf.bzl", "cc_proto_library")
#load("@com_google_protobuf//:protobuf.bzl", "py_proto_library")
#load("@com_github_grpc_grpc//:bazel/grpc_build_system.bzl", "grpc_cc_library")
#load("@com_github_grpc_grpc//:bazel/grpc_build_system.bzl", "grpc_proto_library")
#load("@com_github_grpc_grpc//:bazel/grpc_build_system.bzl", "grpc_py_binary")
#
#grpc_py_binary(
#    name = 'test',
#    srcs = [ 'greeter_server.py' ],
#    deps = [ 'helloworld' ])
#
#grpc_proto_library(
#    name = 'helloworld',
#    srcs = [ 'helloworld.proto' ])
#
#cc_binary(
#    name = 'greeter_cli',
#    srcs = ['greeter_client.cc'],
#    deps = [
#        ':helloworld',
#        '@com_google_grpc//:grpc++',
#    ],
#    linkopts = ['-ldl'],
#)
#
#cc_binary(
#    name = 'greeter_serv',
#    srcs = ['greeter_server.cc'],
#    deps = [
#        ':helloworld',
#        '@com_google_grpc//:grpc++',
#    ],
#    linkopts = ['-ldl'],
#)
#
