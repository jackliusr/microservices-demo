load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "io_bazel_rules_go",
    sha256 = "2b1641428dff9018f9e85c0384f03ec6c10660d935b750e3fa1492a281a53b0f",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/rules_go/releases/download/v0.29.0/rules_go-v0.29.0.zip",
        "https://github.com/bazelbuild/rules_go/releases/download/v0.29.0/rules_go-v0.29.0.zip",
    ],
)

http_archive(
    name = "bazel_gazelle",
    sha256 = "de69a09dc70417580aabf20a28619bb3ef60d038470c7cf8442fafcf627c21cb",
    urls = [
        "https://mirror.bazel.build/github.com/bazelbuild/bazel-gazelle/releases/download/v0.24.0/bazel-gazelle-v0.24.0.tar.gz",
        "https://github.com/bazelbuild/bazel-gazelle/releases/download/v0.24.0/bazel-gazelle-v0.24.0.tar.gz",
    ],
)

load("@io_bazel_rules_go//go:deps.bzl", "go_register_toolchains", "go_rules_dependencies")
load("@bazel_gazelle//:deps.bzl", "gazelle_dependencies", "go_repository")

############################################################
# Define your own dependencies here using go_repository.
# Else, dependencies declared by rules_go/gazelle will be used.
# The first declaration of an external repository "wins".
############################################################

load("//:deps.bzl", "go_dependencies")

# gazelle:repository_macro deps.bzl%go_dependencies
go_dependencies()

http_archive(
    name = "go_googleapis",
    patch_args = [
        "-E",
        "-p1",
    ],
    patches = [
        # releaser:patch-cmd find . -name BUILD.bazel -delete
        #"@io_bazel_rules_go//third_party:go_googleapis-deletebuild.patch",
        # set gazelle directives; change workspace name
        #"@io_bazel_rules_go//third_party:go_googleapis-directives.patch",
        # releaser:patch-cmd gazelle -repo_root .
        #"@io_bazel_rules_go//third_party:go_googleapis-gazelle.patch",
    ],
    sha256 = "3adf7795d87baf68903ca9489768a59945ae93754ece7db5dc32b922959ff7b0",
    strip_prefix = "googleapis-73da6697f598f1ba30618924936a59f8e457ec89",
    urls = [
        "https://mirror.bazel.build/github.com/googleapis/googleapis/archive/73da6697f598f1ba30618924936a59f8e457ec89.zip",
        "https://github.com/googleapis/googleapis/archive/73da6697f598f1ba30618924936a59f8e457ec89.zip",
    ],
)

http_archive(
    name = "com_google_googleapis",
    patch_args = [
        "-E",
        "-p1",
    ],
    patches = [
        # releaser:patch-cmd find . -name BUILD.bazel -delete
        #"@io_bazel_rules_go//third_party:go_googleapis-deletebuild.patch",
        # set gazelle directives; change workspace name
        #"@io_bazel_rules_go//third_party:go_googleapis-directives.patch",
        # releaser:patch-cmd gazelle -repo_root .
        #"@io_bazel_rules_go//third_party:go_googleapis-gazelle.patch",
    ],
    sha256 = "3adf7795d87baf68903ca9489768a59945ae93754ece7db5dc32b922959ff7b0",
    strip_prefix = "googleapis-73da6697f598f1ba30618924936a59f8e457ec89",
    urls = [
        "https://mirror.bazel.build/github.com/googleapis/googleapis/archive/73da6697f598f1ba30618924936a59f8e457ec89.zip",
        "https://github.com/googleapis/googleapis/archive/73da6697f598f1ba30618924936a59f8e457ec89.zip",
    ],
)

load("@com_google_googleapis//:repository_rules.bzl", "switched_rules_by_language")

switched_rules_by_language(
    name = "com_google_googleapis_imports",
    go = True,
    grpc = True,
)

go_rules_dependencies()

go_register_toolchains(version = "1.17.2")

gazelle_dependencies()

http_archive(
    name = "io_grpc_grpc_java",
    sha256 = "f00c05f7c5477d5c31cd2483628e81ba599d2b93d17aa0c5266fc5547f4c22e9",
    strip_prefix = "grpc-java-1.43.1",
    url = "https://github.com/grpc/grpc-java/archive/v1.43.1.zip",
)

http_archive(
    name = "rules_jvm_external",
    sha256 = "cd1a77b7b02e8e008439ca76fd34f5b07aecb8c752961f9640dea15e9e5ba1ca",
    strip_prefix = "rules_jvm_external-4.2",
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/4.2.zip",
)

load("@rules_jvm_external//:defs.bzl", "maven_install")
load("@io_grpc_grpc_java//:repositories.bzl", "IO_GRPC_GRPC_JAVA_ARTIFACTS")
load("@io_grpc_grpc_java//:repositories.bzl", "IO_GRPC_GRPC_JAVA_OVERRIDE_TARGETS")
load("@io_grpc_grpc_java//:repositories.bzl", "grpc_java_repositories")

grpc_java_repositories()

http_archive(
    name = "com_google_protobuf",
    sha256 = "87407cd28e7a9c95d9f61a098a53cf031109d451a7763e7dd1253abf8b4df422",
    strip_prefix = "protobuf-3.19.1",
    urls = [
        "https://mirror.bazel.build/github.com/protocolbuffers/protobuf/archive/v3.19.1.tar.gz",
        "https://github.com/protocolbuffers/protobuf/archive/v3.19.1.tar.gz",
    ],
)

load("@com_google_protobuf//:protobuf_deps.bzl", "PROTOBUF_MAVEN_ARTIFACTS", "protobuf_deps")

protobuf_deps()

maven_install(
    artifacts = IO_GRPC_GRPC_JAVA_ARTIFACTS + [
        "org.apache.logging.log4j:log4j-core:2.17.0",
        #"com.google.api.grpc:proto-google-common-protos:1.18.1",
        #"io.opencensus:opencensus-api:0.27.0",
        #"io.opencensus:opencensus-contrib-grpc-metrics:0.27.0",
        "io.opencensus:opencensus-contrib-grpc-util:0.27.0",
        "io.opencensus:opencensus-exporter-trace-jaeger:0.27.0",
        "io.opencensus:opencensus-exporter-stats-stackdriver:0.27.0",
        "io.opencensus:opencensus-exporter-trace-stackdriver:0.27.0",
        "io.opencensus:opencensus-exporter-trace-logging:0.27.0",
        "io.grpc:grpc-services:1.27.2",  #//1.43.1",
    ],  # + PROTOBUF_MAVEN_ARTIFACTS,
    generate_compat_repositories = True,
    override_targets = IO_GRPC_GRPC_JAVA_OVERRIDE_TARGETS,
    repositories = [
        "https://repo.maven.apache.org/maven2/",
    ],
)

load("@maven//:compat.bzl", "compat_repositories")

compat_repositories()
