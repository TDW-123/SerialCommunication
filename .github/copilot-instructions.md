# Copilot instructions — SerialCommunication

## Build, run and debug
- Open the project in Visual Studio 2017+ and press F5 (Start Debugging) or Ctrl+Shift+B (Build).
- MSBuild (Windows):
  - Build: msbuild "SerialCommunication\SerialCommunication.csproj" /p:Configuration=Debug
  - Release: msbuild "SerialCommunication\SerialCommunication.csproj" /p:Configuration=Release
- dotnet CLI (may work on machines with .NET SDK): dotnet build "SerialCommunication\SerialCommunication.csproj" -c Debug
- Run executable: `SerialCommunication\bin\Debug\SerialCommunication.exe` after building.

## Tests and linting
- No test projects or linting configuration detected in this repository.
- If tests are added using MSTest/NUnit/xUnit: use `dotnet test <test-project>` or run the test from Visual Studio. To run a single test use the Test Explorer or filter via `dotnet test --filter "FullyQualifiedName~Namespace.Class.Method"`.

## High-level architecture
- Single WinForms application: project `SerialCommunication` targets .NET Framework 4.7.2.
- Entry point: Program.Main -> launches Form1 (partial class). Form1 contains the UI and serial-port logic.
- Serial-port usage: System.IO.Ports.SerialPort is used to enumerate ports (SerialPort.GetPortNames()) and perform communication; settings (baudrate, parity, stopbits, DTR/RTS) are exposed in the "Instellingen" tab.
- UI layout: top connection controls (comboBoxPoort, comboBoxBaudrate, buttonConnect) and a TabControl with pages: Instellingen, Oefening1..Oefening5 (digital IO, PWM sliders, analog displays, thermostat). Resources (images) are stored under Resources\.
- No separate layers (no web/API/data layer); all app logic resides in Form1 and designer files.

## Key repository conventions
- Naming: controls use type-prefixed camelCase (e.g., comboBoxPoort, buttonConnect, labelPoort). Many identifiers and UI labels are Dutch (Poort, Instellingen, Oefening).
- Events: handler naming follows controlName_Event (e.g., buttonConnect_Click, cboPoort_DropDown).
- Designer pattern: Form1 is split into Form1.cs (logic) and Form1.Designer.cs (auto-generated). Avoid editing Designer.cs manually.
- Resources: images included under Resources\ and referenced by PictureBox controls. App.config is present for configuration.
- Target: Windows desktop; development and debugging are expected on Windows with Visual Studio. Building with msbuild is the recommended CLI path.

## AI / assistant config checks
- No other assistant config files detected (CLAUDE.md, .cursorrules, AGENTS.md, CONVENTIONS.md, etc.).

---

If you want this file adjusted (add build matrix, CI commands, or guidance for adding tests/linting), say which areas to expand.
