load("//tensorflow:tensorflow.bzl", "pybind_extension")

package(
    default_visibility = [
        "//visibility:public",
    ],
    licenses = ["notice"],  # Apache 2.0
)

cc_library(
    name = "hashtable_op_kernels",
    srcs = [
        "hashtable.cc",
        "hashtable_find.cc",
        "hashtable_import.cc",
        "hashtable_ops.cc",
        "hashtable_size.cc",
    ],
    hdrs = [
        "hashtable_ops.h",
    ],
    deps = [
        "//tensorflow/lite:framework",
        "//tensorflow/lite/c:common",
        "//tensorflow/lite/core/api",
        "//tensorflow/lite/experimental/resource",
        "//tensorflow/lite/kernels:kernel_util",
        "//tensorflow/lite/kernels/internal:tensor",
        "//tensorflow/lite/schema:schema_fbs",
        "@flatbuffers",
    ],
)

cc_test(
    name = "hashtable_op_test",
    size = "small",
    srcs = [
        "hashtable_ops_test.cc",
    ],
    deps = [
        ":hashtable_op_kernels",  # buildcleaner: keep
        "//tensorflow/lite:framework",
        "//tensorflow/lite/core/api",
        "//tensorflow/lite/experimental/resource",
        "//tensorflow/lite/kernels:test_main",
        "//tensorflow/lite/kernels:test_util",
        "//tensorflow/lite/kernels/internal:tensor",
        "//tensorflow/lite/testing:util",
        "@com_google_absl//absl/memory",
        "@com_google_absl//absl/strings",
        "@flatbuffers",
    ],
)

pybind_extension(
    name = "pywrap_hashtable_ops",
    srcs = [
        "hashtable_ops_wrapper.cc",
    ],
    hdrs = ["hashtable_ops.h"],
    additional_exported_symbols = ["HashtableOpsRegisterer"],
    link_in_framework = True,
    module_name = "pywrap_hashtable_ops",
    deps = [
        ":hashtable_op_kernels",
        "//tensorflow/lite:framework",
        "//tensorflow/lite/kernels:builtin_ops",
        "//third_party/python_runtime:headers",
        "@pybind11",
    ],
)
