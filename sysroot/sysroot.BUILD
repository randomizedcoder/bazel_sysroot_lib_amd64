package(default_visibility = ["//visibility:public"])

filegroup(
    name = "all",
    srcs = glob(["**"]),
)

filegroup(
    name = "include",
    srcs = glob(["include/*"]),
    visibility = ["//visibility:public"],
)

filegroup(
    name = "lib",
    srcs = glob(["lib/*"]),
    visibility = ["//visibility:public"],
)

cc_library(
    name = "system_libs",
    srcs = glob(["lib/*.so*"]),
    linkstatic = 1,
    visibility = ["//visibility:public"],
)
