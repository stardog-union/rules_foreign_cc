load("@rules_cc//cc:defs.bzl", "cc_binary", "cc_library")
load("@rules_foreign_cc//tools/build_defs:cmake.bzl", "cmake_external")

filegroup(
    name = "srcs",
    srcs = glob(["**"]),
    visibility = ["//src/test/shell/bazel/testdata:__pkg__"],
)

cc_library(
    name = "hello",
    srcs = ["hello.cc"],
)

cmake_external(
    name = "hello_cmake",
    lib_source = "//static:srcs",
    out_include_dir = "include/version123",
    static_libraries = ["libhello.a"],
)

# I do not make it a test, since it is a cross-compilation example,
# requires test that just checks something about output
cc_binary(
    name = "libhello_test",
    # includes just hello.h, include directory: "include/version123"
    srcs = ["//static:hello_client.c"],
    deps = [":hello_cmake"],
)
