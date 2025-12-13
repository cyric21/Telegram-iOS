# Copilot Instructions for Telegram-iOS

## Architecture Overview
- **Modular Structure**: Core app logic in `Telegram/Telegram-iOS/`, UI components and utilities in `submodules/` (e.g., `ChatListUI/`, `AsyncDisplayKit/`), third-party libraries in `third-party/`.
- **UI Framework**: Uses AsyncDisplayKit (Texture) for declarative UI with nodes (e.g., `ChatListNode` in `submodules/ChatListUI/Sources/`).
- **Data Flow**: AccountContext manages global state; controllers like `ChatController` handle specific features; communication via signals and reactive patterns.
- **Build System**: Bazel-based with custom Apple/Swift rules; generates Xcode projects via `build-system/Make/Make.py`.

## Key Workflows
- **Build**: Use Bazel directly: `bazel build Telegram/Telegram --ios_multi_cpus=sim_arm64 -c dbg`. For Xcode integration, run `python3 build-system/Make/Make.py generateProject --configurationPath=build-system/template_minimal_development_configuration.json`.
- **Debug**: Run `scripts/launch_and_debug.sh` to build, launch simulator app, and attach debugserver on port 6667 for LLDB.
- **Configuration**: Edit JSON configs in `build-system/` for API keys, provisioning; use `openssl rand -hex 8` for identifiers.
- **No Tests**: Project lacks automated tests; validate manually via simulator runs.

## Conventions and Patterns
- **Naming**: PascalCase for types/classes (e.g., `AccountContext`), camelCase for methods/variables.
- **Imports**: Group and sort at file top; prefer explicit imports.
- **Error Handling**: Use Swift's do-catch; redact sensitive data in logs.
- **UI Nodes**: Extend `ASDisplayNode` for components; use `layoutSpecThatFits` for layout (e.g., in `ChatMessageItemNode`).
- **Reactive Programming**: Employ signals for data binding; avoid direct state mutations.
- **File Organization**: One class per file; related utilities in same submodule directory.

## Integration Points
- **External APIs**: Telegram API via MTProto; handle in `submodules/CloudData/`.
- **Dependencies**: Local Bazel overrides for rules; third-party like WebRTC in `third-party/webrtc/`.
- **Extensions**: App extensions in `Telegram/` subdirs (e.g., `Share/`, `NotificationService/`); share code via submodules.

Reference: `CLAUDE.md` for style; `README.md` for build setup.</content>
<parameter name="filePath">/workspaces/Telegram-iOS/.github/copilot-instructions.md