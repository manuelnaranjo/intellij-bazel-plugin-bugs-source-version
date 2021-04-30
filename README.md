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

And you get something like:
```
$ bazel build     --tool_tag=ijwb:IDEA:ultimate     --keep_going     --noexperimental_run_validations     --aspects=@intellij_aspect//:intellij_info_bundled.bzl%intellij_info_aspect     --override_repository=intellij_aspect=<LOCAL>/share/JetBrains/IntelliJIdea2020.3/ijwb/aspect     --output_groups=intellij-info-generic,intellij-info-java-direct-deps,intellij-resolve-java-direct-deps     -- //:all
INFO: Invocation ID: 8c5bf7eb-a9fe-4d79-96cc-17f053498a9b
ERROR: <BAZEL_CACHE>/a418f061d5b6adb24bd38a0c0437027d/external/local_config_cc/BUILD:47:19: in @intellij_aspect//:intellij_info_bundled.bzl%intellij_info_aspect aspect on cc_toolchain_suite rule @local_config_cc//:toolchain:
Traceback (most recent call last):
	File "<BAZEL_CACHE>/a418f061d5b6adb24bd38a0c0437027d/external/intellij_aspect/intellij_info_bundled.bzl", line 54, column 37, in _aspect_impl
		return intellij_info_aspect_impl(target, ctx, semantics)
	File "<BAZEL_CACHE>/a418f061d5b6adb24bd38a0c0437027d/external/intellij_aspect/intellij_info_impl.bzl", line 1079, column 42, in intellij_info_aspect_impl
		handled = collect_java_toolchain_info(target, ide_info, ide_info_file, output_groups) or handled
	File "<BAZEL_CACHE>/a418f061d5b6adb24bd38a0c0437027d/external/intellij_aspect/intellij_info_impl.bzl", line 913, column 35, in collect_java_toolchain_info
		source_version = toolchain.source_version,
Error: 'ToolchainInfo' value has no field or method 'source_version'
Available attributes: all_files, ar_executable, built_in_include_directories, compiler, compiler_executable, cpu, ld_executable, libc, nm_executable, objcopy_executable, objdump_executable, preprocessor_executable, strip_executable, sysroot, target_gnu_system_name
INFO: Analyzed 3 targets (0 packages loaded, 0 targets configured).
INFO: Found 3 targets...
ERROR: command succeeded, but not all targets were analyzed
INFO: Elapsed time: 0.132s, Critical Path: 0.01s
INFO: 1 process: 1 internal.
FAILED: Build did NOT complete successfully
```
