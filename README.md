# Android Application Security Analysis

A practical collection of Android application security assessments covering reverse engineering, static analysis, and dynamic analysis. This repository documents how Android application structure, components, local data handling, runtime behaviour, and network activity can be examined using common mobile security tools.

## Project Scope

- [**Pocket Notes — Static Analysis**](static-analysis/pocket-notes/README.md): APK inspection, manifest and activity review, local storage, logging behaviour, and embedded configuration.
- [**Device Relay — Dynamic Analysis**](dynamic-analysis/device-relay/README.md): observation of application behaviour in an Android emulator, including service activity, diagnostic requests, and network traffic captured during testing.
- [**Pegasus — MobSF Static Analysis**](static-analysis/pegasus-mobsf/README.md): a MobSF-based review of an APK examined during a mobile application security exercise. The name identifies the analysis exercise; it is not a claim that the sample was verified as the Pegasus spyware product.

## Tools and Environment

- JADX-GUI 1.5.6
- MobSF
- Android Studio and Android Emulator
- Burp Suite Community Edition
- Logcat and Android debugging utilities
- Windows 11

Not every tool was used in every case study.

## Repository Structure

```text
android-application-security-analysis/
├── README.md
├── static-analysis/
│   ├── pocket-notes/
│   └── pegasus-mobsf/
└── dynamic-analysis/
    └── device-relay/
```

Individual case-study folders will contain the relevant methodology, observations, screenshots, and reports.

## Analysis Approach

1. Identify application metadata, package information, permissions, and components.
2. Review code and configuration for security-relevant implementation choices.
3. Examine local data storage, logging, and exported components.
4. Observe runtime behaviour in a controlled Android environment.
5. Inspect application network traffic where applicable.
6. Record evidence and distinguish confirmed observations from assumptions.

## Responsible Use

All work is documented for educational and defensive application-security purposes. Testing is performed in controlled environments and focuses on understanding security behaviour, identifying weaknesses, and communicating findings responsibly. This repository does not provide instructions for deploying spyware or accessing devices without authorization.

## Status

Case studies are being documented and expanded as analysis evidence and screenshots are organized. Findings will be added only where supported by the available evidence.
