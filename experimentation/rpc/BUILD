load("@com_google_protobuf//:protobuf.bzl", "cc_proto_library")
load("@com_github_grpc_grpc//:bazel/grpc_build_system.bzl", "grpc_cc_library")
load("@com_github_grpc_grpc//:bazel/grpc_build_system.bzl", "grpc_proto_library")

grpc_proto_library(
    name = 'helloworld',
    srcs = [ 'helloworld.proto' ])

cc_binary(
    name = 'greeter_client',
    srcs = ['greeter_client.cc'],
    deps = [
        ':helloworld',
        '@com_github_grpc_grpc//:grpc++',
    ],
    linkopts = ['-ldl'],
)

cc_binary(
    name = 'greeter_server',
    srcs = ['greeter_server.cc'],
    deps = [
        ':helloworld',
        '@com_github_grpc_grpc//:grpc++',
    ],
    linkopts = ['-ldl'],
)

