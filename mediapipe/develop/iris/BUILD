load("@build_bazel_rules_apple//apple:ios.bzl", "ios_framework")

ios_framework(
    name = "SYIris",
    hdrs = [
        "SYIris.h",
    ],
    infoplists = ["Info.plist"],
    bundle_id = "com.sho8.kthy.IrisFramework",
    families = ["iphone", "ipad"],
    minimum_os_version = "13.0",
    deps = [
        ":SYIrisFramework",
        "@ios_opencv//:OpencvFramework",
    ],
)

objc_library(
    name = "SYIrisFramework",
    srcs = [
        "SYIris.mm",
    ],
    hdrs = [
        "SYIris.h",
    ],
    data = [
        "//mediapipe/graphs/iris_tracking:iris_tracking_gpu.binarypb",
        "//mediapipe/modules/face_detection:face_detection_short_range.tflite",
        "//mediapipe/modules/face_landmark:face_landmark.tflite",
        "//mediapipe/modules/iris_landmark:iris_landmark.tflite",
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
            "//mediapipe/graphs/iris_tracking:iris_tracking_gpu_deps",
            "//mediapipe/framework/formats:landmark_cc_proto",
        ],
    }),
)
