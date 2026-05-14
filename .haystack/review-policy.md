# Review Policies

## Manual review for platform detection and toolchain logic
- **Paths**: `platform/**/detect.py`, `methods.py`, `SConstruct`, `modules/*/config.py`
- **Severity**: high
- **Reason**: Build detection and compiler/linker flag changes can silently break portability and cross-compilation in ways CI may miss.

## Manual review for Windows titlebar/display server integration
- **Paths**: `platform/windows/display_server_windows.*`, `editor/editor_node.cpp`, `editor/project_manager/project_manager.cpp`, `scene/gui/caption_button_overlay.*`, `scene/main/window.cpp`
- **Severity**: high
- **Reason**: DPI metrics, window event loops, and OS integration changes can cause subtle runtime regressions (e.g., freezes/resize loops) not well-covered by tests.

## Manual review for Android lifecycle and embedded editor flow
- **Paths**: `platform/android/**`, `editor/export/export_plugin.cpp`
- **Severity**: high
- **Reason**: Android lifecycle/JNI/init-order changes are failure-prone and often only reproducible at runtime on-device.

## Manual review for third-party vendored and license-sensitive files
- **Paths**: `thirdparty/**`, `COPYRIGHT.txt`
- **Severity**: critical
- **Reason**: Edits may introduce licensing/compliance risk or unintended divergence from upstream vendored sources.

## Instructions
- If a change removes null checks, validity checks, or crash-prevention guards, require human review to confirm the reliability/performance tradeoff is intentional and safe.
- If a change downgrades errors to warnings or suppresses warnings, require human judgment on whether the new failure mode is acceptable.
- If defaults or path restrictions are changed in ways that may break existing workflows, require human review of migration and backward-compatibility impact.
