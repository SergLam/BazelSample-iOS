load(
    "@build_bazel_rules_apple//apple:ios.bzl",
    "ios_application",
    "ios_unit_test",
    "ios_ui_test",
)

load(
    "@build_bazel_rules_apple//apple:apple.bzl", 
    "apple_dynamic_framework_import",
    "apple_static_framework_import",
)

load(
    "@build_bazel_rules_swift//swift:swift.bzl", 
    "swift_library",
)

load("@xchammer//:xchammerconfig.bzl", 
     "gen_xchammer_config",
     "scheme_action_config",
     "execution_action",
     "environment_variable",
     "target_config",
     "project_config",
     "xchammer_config",
)

# load("@xchammer//:xcodeproject.bzl", 
#      "xcode_project",
# )

# Resources

filegroup(
    name = "Resources",
    srcs = glob(["App/Resources/**/*"]),
    visibility = ["//visibility:public"],
)

# Main app

swift_library(
    name = "BazelSample-iOSLib",
    srcs = glob(["App/Sources/**/*.swift"]), 
    deps = [
        "//Modules/SwiftLib:SwiftLib",
        "//Modules/SwiftLibWithResources:SwiftLibWithResources",
    ],
    copts = [] + ["-whole-module-optimization","-Osize"] + ["-swift-version", "5"],
    data = [":Resources"],
    visibility = ["//visibility:public"],
)

ios_application(
    name = "BazelSample-iOS",
    bundle_id = "com.example.BaselSample-iOS",
    minimum_os_version = "11.0",
    families = [
       "iphone",
    ],
    infoplists = [
        ":App/Supporting Files/Info.plist",
    ],
    app_icons = [
         "//App/Resources:AppIcon",
    ],
    resources = [
        "//App/Resources:Assets",
    ],
    deps = [
        ":BazelSample-iOSLib"
    ],
)

# Project file generation
xcode_project(
    name = "BazelSample-iOS-Proj",
    targets = [ 
        "BazelSample-iOS", 
        ":BazelSample-iOS-Tests", 
    ],
    paths = [ "**" ],
)

# Unit tests

swift_library(
    name = "BazelSample-iOSLibTests",
    srcs = glob(["App/Tests/**/*.swift"]),
    deps = [
        "//Modules/SwiftLib:SwiftLib",
        "//Modules/SwiftLibWithResources:SwiftLibWithResources",
    ],
    visibility = ["//visibility:public"],
)

ios_unit_test(
    name = "BazelSample-iOS-Tests",
    deps = [":BazelSample-iOSLib"],
    infoplists = [
        ":App/Supporting Files/Info.plist",
    ],
    minimum_os_version = "11.0",
    visibility = ["//visibility:public"],
)