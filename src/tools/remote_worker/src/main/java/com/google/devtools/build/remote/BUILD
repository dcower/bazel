filegroup(
    name = "srcs",
    srcs = glob(["**"]),
    visibility = ["//src/tools/remote_worker:__pkg__"],
)

java_library(
    name = "remote",
    srcs = glob(["*.java"]),
    data = ["//src:libunix"],
    visibility = ["//src/tools/remote_worker:__subpackages__"],
    deps = [
        "//src/main/java/com/google/devtools/build/lib:build-base",
        "//src/main/java/com/google/devtools/build/lib:concurrent",
        "//src/main/java/com/google/devtools/build/lib:events",
        "//src/main/java/com/google/devtools/build/lib:io",
        "//src/main/java/com/google/devtools/build/lib:os_util",
        "//src/main/java/com/google/devtools/build/lib:packages-internal",
        "//src/main/java/com/google/devtools/build/lib:runtime",
        "//src/main/java/com/google/devtools/build/lib:shell",
        "//src/main/java/com/google/devtools/build/lib:util",
        "//src/main/java/com/google/devtools/build/lib:vfs",
        "//src/main/java/com/google/devtools/build/lib/remote",
        "//src/main/java/com/google/devtools/common/options",
        "//src/main/protobuf:remote_protocol_java_proto",
        "//third_party:guava",
        "//third_party:hazelcast",
        "//third_party:netty",
        "//third_party/grpc:grpc-jar",
        "//third_party/protobuf",
    ],
)
