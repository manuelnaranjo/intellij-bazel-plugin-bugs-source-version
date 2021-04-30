# Sample bazel project to show IntelliJ Plugin bug

This is a bare minimal project that I created to show a bug in the IntelliJ Bazel Plugin. To reproduce
you can either sync from the bazel menu or run something like this:

```
bazel build \
    --tool_tag=ijwb:IDEA:ultimate \
    --keep_going \
    --noexperimental_run_validations \
    --aspects=@intellij_aspect//:intellij_info_bundled.bzl%intellij_info_aspect \
    --override_repository=intellij_aspect=<path-to-intellij-plugins>/ijwb/aspect/ \
    --output_groups=intellij-info-generic,intellij-info-java-direct-deps,intellij-resolve-java-direct-deps \
    -- //:all
```
