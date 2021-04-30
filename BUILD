load("@io_bazel_rules_docker//java:image.bzl", "java_image")

java_library(
    name = "lib",
    srcs = ['com.example.main/Main.java']
)

java_image(
    name = "java_image",
    runtime_deps=[":lib"],
    main_class = "com.booking.main.Main",
    stamp=True
)
