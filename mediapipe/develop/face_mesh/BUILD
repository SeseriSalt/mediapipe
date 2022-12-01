load("@build_bazel_rules_apple//apple:ios.bzl", "ios_framework")

ios_framework(
    name = "SYFaceMesh",
    hdrs = [
        "SYFaceMesh.h",
    ],
    infoplists = ["Info.plist"],
    bundle_id = "com.sho8.kthy.FaseMeshFramework",
    families = ["iphone", "ipad"],
    minimum_os_version = "13.0",
    deps = [
        ":SYFaceMeshFramework",
        "@ios_opencv//:OpencvFramework",
    ],
)

objc_library(
    name = "SYFaceMeshFramework",
    srcs = [
        "SYFaceMesh.mm",
    ],
    hdrs = [
        "SYFaceMesh.h",
    ],
    data = [
        "//mediapipe/graphs/face_mesh:face_mesh_mobile_gpu.binarypb",
        "//mediapipe/modules/face_detection:face_detection_short_range.tflite",
        "//mediapipe/modules/face_landmark:face_landmark_with_attention.tflite",
    ],
    sdk_frameworks = [
        "AVFoundation",
        "CoreGraphics",
        "CoreMedia",
        "UIKit"
    ],
    deps = [
        "//mediapipe/objc:mediapipe_framework_ios",
        "//mediapipe/objc:mediapipe_input_sources_ios",
        "//mediapipe/objc:mediapipe_layer_renderer",
    ] + select({
        "//mediapipe:ios_i386": [],
        "//mediapipe:ios_x86_64": [],
        "//conditions:default": [
            "//mediapipe/graphs/face_mesh:mobile_calculators",
            "//mediapipe/framework/formats:landmark_cc_proto",
        ],
    }),
)
