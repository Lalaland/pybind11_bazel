# pybind11 - Seamless operability between C++11 and Python.
load("@rules_cc//cc:defs.bzl", "cc_library")

package(default_visibility = ["//visibility:public"])

licenses(["notice"])

exports_files(["LICENSE"])

OPTIONS = select({
    ":msvc_compiler": [],
    "//conditions:default": [
        "-fexceptions",
        # Useless warnings
        "-Xclang-only=-Wno-undefined-inline",
        "-Xclang-only=-Wno-pragma-once-outside-header",
        "-Xgcc-only=-Wno-error",  # no way to just disable the pragma-once warning in gcc
    ],
})

INCLUDES = [
    "include/pybind11/*.h",
    "include/pybind11/detail/*.h",
    "include/pybind11/eigen/*.h",
]

EXCLUDES = [
    # Deprecated file that just emits a warning
    "include/pybind11/common.h",
]

cc_library(
    name = "pybind11",
    hdrs = glob(
        INCLUDES,
        exclude = EXCLUDES,
    ),
    copts = OPTIONS,
    includes = ["include"],
    deps = ["@local_config_python//:python_headers"],
)

cc_library(
    name = "pybind11_embed",
    hdrs = glob(
        INCLUDES,
        exclude = EXCLUDES,
    ),
    copts = OPTIONS,
    includes = ["include"],
    deps = ["@local_config_python//:python_embed"],
)

config_setting(
    name = "msvc_compiler",
    flag_values = {"@bazel_tools//tools/cpp:compiler": "msvc-cl"},
)

config_setting(
    name = "osx",
    constraint_values = ["@platforms//os:osx"],
)
