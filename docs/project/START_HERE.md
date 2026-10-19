# Mir 3 mercenary project — start here

## Direction

Build on Suprcode Zircon with our own server-controlled mercenary system. The Godot fork's BotRunner is a research reference, not the project base. Reuse validated game actions rather than implement a second combat engine.

Player ownership, equipment, progression, hiring contracts and deployment limits are the intended foundations. Exact balance values remain undecided. Do not assume free-roaming server-owned residents or LLM calls are required for the first version.

## Repository workflow

- Original upstream: https://github.com/Suprcode/Zircon
- Project fork: https://github.com/sK1-school/Zircon
- Keep master as the integration baseline; changes start on feature branches.
- Initial branch: setup/server-baseline.
- Read root AGENTS.md and the relevant source documentation before changes.
- Submit changes as pull requests within this fork, not to upstream.
- This is a public repository: never commit credentials, private account databases, personal information or unreviewed asset bundles.
- Preserve upstream attribution. Establish applicable code, dependency and asset permissions before distribution.

## Local checkout

Install Git and the .NET 10 SDK, then run:

```text
git clone https://github.com/sK1-school/Zircon.git
cd Zircon
git remote add upstream https://github.com/Suprcode/Zircon.git
git switch setup/server-baseline
dotnet --info
dotnet restore ServerCore/ServerCore.csproj
dotnet build ServerCore/ServerCore.csproj --configuration Release --no-restore
```

The console server references ServerLibrary and LibraryCore. Start with this project rather than the entire Windows solution. See [project map](../PROJECT_MAP.md) and [verification routing](../VERIFICATION.md).

The Windows client and administration/editor tools need their own dependency setup, including checking DevExpress requirements for the editor. Do not assume a successful console build validates these applications.

## Baseline acceptance gates

1. Clean console-server restore and build on Linux and Windows.
2. Identify and document compatible System.db, map files, configuration and runtime working directory from the actual startup code.
3. Start an isolated development server with disposable data.
4. Connect a matching Windows client; create a character; move, fight and collect an item.
5. Shut down cleanly, restart and verify character position/progression/inventory persistence.
6. Record source revision, SDK version, data provenance and exact commands.

Compilation is not proof of server startup, client interoperability or playable content. Runtime configuration and game assets are not supplied by this setup change.

## Implementation milestones

| Stage | Deliverable | Evidence required |
| --- | --- | --- |
| Baseline | Reproducible original server and client | All baseline gates above |
| First mercenary | One server-controlled character follows and assists a human | Movement, combat rules, disconnect and map-change scenarios |
| Ownership | Persistent owner, equipment and progression | Save/reload and item-transfer invariants |
| Hiring | Exclusive contract, owner permission, price and expiry | Concurrent hiring, payment and cancellation checks |
| Deployment | Configurable limits and costs | No duplicate deployment or reward exploits |
| Expansion | More roles and optional factions/world activities | Performance and economy measurements |

## Next Codex task

Establish the baseline before modifying gameplay. Inspect ServerCore startup and the relevant server-runtime guide; run the console build; fix only reproducible blockers on a separate branch. Identify required runtime data and obtain matching files without committing private data or large game assets. Report separately: source inspected, build passed, server started, login passed and gameplay verified. Do not describe unexecuted checks as successful.
