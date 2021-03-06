# Description:
#   singlejar C++ implementation.
package(default_visibility = ["//src:__subpackages__"])

filegroup(
    name = "srcs",
    srcs = glob(["**"]),
    visibility = ["//src:__pkg__"],
)

cc_binary(
    name = "singlejar",
    srcs = [
        "singlejar_main.cc",
    ],
    linkstatic = 1,
    deps = [
        "options",
        "output_jar",
        "//third_party/zlib",
    ],
)

cc_test(
    name = "combiners_test",
    size = "large",
    srcs = [
        "combiners_test.cc",
        ":zip_headers",
        ":zlib_interface",
    ],
    deps = [
        ":combiners",
        ":input_jar",
        "//third_party:gtest",
        "//third_party/zlib",
    ],
)

cc_test(
    name = "input_jar_preambled_test",
    srcs = [
        "input_jar_preambled_test.cc",
    ],
    data = [
        ":test1",
    ],
    deps = [
        ":input_jar",
        ":test_util",
        "//src/main/cpp/util",
        "//third_party:gtest",
    ],
)

cc_test(
    name = "input_jar_scan_jartool_test",
    size = "large",
    srcs = [
        "input_jar_scan_entries_test.h",
        "input_jar_scan_jartool_test.cc",
    ],
    copts = ["-DJAR_TOOL_PATH=\\\"external/local_jdk/bin/jar\\\""],
    data = [
        "//external:jar",
        "//external:jdk-default",
    ],
    # Timing out, see https://github.com/bazelbuild/bazel/issues/1555
    tags = ["manual"],
    deps = [
        ":input_jar",
        ":test_util",
        "//third_party:gtest",
    ],
)

cc_test(
    name = "input_jar_scan_ziptool_test",
    size = "large",
    srcs = [
        "input_jar_scan_entries_test.h",
        "input_jar_scan_ziptool_test.cc",
    ],
    # Timing out, see https://github.com/bazelbuild/bazel/issues/1555
    tags = ["manual"],
    deps = [
        ":input_jar",
        ":test_util",
        "//third_party:gtest",
    ],
)

cc_test(
    name = "input_jar_bad_jar_test",
    srcs = [
        "input_jar_bad_jar_test.cc",
    ],
    deps = [
        ":input_jar",
        ":test_util",
        "//third_party:gtest",
    ],
)

cc_test(
    name = "options_test",
    srcs = [
        "options.h",
        "options_test.cc",
        ":token_stream",
    ],
    deps = [
        ":options",
        ":test_util",
        "//src/main/cpp/util",
        "//third_party:gtest",
    ],
)

cc_test(
    name = "output_jar_simple_test",
    srcs = [
        "output_jar_simple_test.cc",
    ],
    copts = ["-Ithird_party/bazel"],
    data = [
        ":data1",
        ":data2",
        ":test1",
        ":test2",
    ],
    deps = [
        ":input_jar",
        ":options",
        ":output_jar",
        ":test_util",
        "//src/main/cpp:blaze_util",
        "//src/main/cpp/util",
        "//third_party:gtest",
    ],
)

cc_test(
    name = "token_stream_test",
    srcs = [
        "token_stream_test.cc",
        ":token_stream",
    ],
    deps = [
        ":test_util",
        "//third_party:gtest",
    ],
)

cc_test(
    name = "transient_bytes_test",
    size = "large",
    srcs = [
        "transient_bytes_test.cc",
        ":transient_bytes",
        ":zlib_interface",
    ],
    # Timing out, see https://github.com/bazelbuild/bazel/issues/1555
    tags = ["manual"],
    deps = [
        ":input_jar",
        ":test_util",
        "//third_party:gtest",
        "//third_party/zlib",
    ],
)

cc_test(
    name = "zip_headers_test",
    size = "small",
    srcs = [
        "zip_headers_test.cc",
        ":zip_headers",
    ],
    deps = ["//third_party:gtest"],
)

cc_test(
    name = "zlib_interface_test",
    srcs = [
        "zlib_interface_test.cc",
        ":zlib_interface",
    ],
    deps = [
        ":test_util",
        "//third_party:gtest",
        "//third_party/zlib",
    ],
)

cc_library(
    name = "combiners",
    srcs = [
        "combiners.cc",
        ":transient_bytes",
        ":zip_headers",
    ],
    hdrs = ["combiners.h"],
    deps = ["//third_party/zlib"],
)

cc_library(
    name = "input_jar",
    srcs = [
        "diag.h",
        "input_jar.cc",
        "mapped_file.h",
    ],
    hdrs = [
        "input_jar.h",
        "zip_headers.h",
    ],
)

cc_library(
    name = "options",
    srcs = [
        "diag.h",
        "options.cc",
        "options.h",
        ":token_stream",
    ],
    hdrs = ["options.h"],
)

cc_library(
    name = "output_jar",
    srcs = [
        "diag.h",
        "mapped_file.h",
        "output_jar.cc",
        "output_jar.h",
        ":zip_headers",
    ],
    hdrs = ["output_jar.h"],
    deps = [
        ":combiners",
        ":input_jar",
        ":options",
        "//src/main/cpp/util",
        "//third_party/zlib",
    ],
)

cc_library(
    name = "test_util",
    srcs = ["test_util.cc"],
    hdrs = ["test_util.h"],
    deps = [
        "//src/main/cpp:blaze_util",
        "//src/main/cpp/util",
        "//third_party:gtest",
    ],
)

filegroup(
    name = "token_stream",
    srcs = [
        "diag.h",
        "token_stream.h",
    ],
)

filegroup(
    name = "transient_bytes",
    srcs = [
        "diag.h",
        "transient_bytes.h",
        "zlib_interface.h",
        ":zip_headers",
    ],
)

filegroup(
    name = "zip_headers",
    srcs = ["zip_headers.h"],
)

filegroup(
    name = "zlib_interface",
    srcs = [
        "diag.h",
        "zlib_interface.h",
    ],
)

java_library(
    name = "test1",
    resources = [
        "zip_headers.h",
        "zlib_interface.h",
    ],
)

java_library(
    name = "test2",
    resources = [
        "token_stream.h",
        "transient_bytes.h",
    ],
)

java_library(
    name = "data1",
    resources = [
        "data/extra_file1",
        "data/extra_file2",
    ],
)

java_library(
    name = "data2",
    resources = [
        "data/extra_file1",
        "data/extra_file3",
    ],
)
