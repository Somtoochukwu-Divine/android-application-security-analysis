# Pocket Notes — Android Static Analysis

## Overview

This case study documents a static security review of the Android application package `org.course.pocketnotes`. The assessment focused on application metadata, manifest configuration, activity behaviour, local data handling, logging, and embedded configuration.

## Analysis Environment

- Operating system: Windows 11
- Decompilation and code review: JADX-GUI 1.5.6
- Analysis type: Static analysis
- Package name: `org.course.pocketnotes`
- Minimum SDK: 23
- Target SDK: 35
- Compile SDK: 35

**Sample SHA-256**

`08A0F73F039530E6B6BF3C6A989F72BC89FEE0A65C5889E93F3F5B00CC22DDA7`

## Methodology

1. Reviewed package metadata and SDK configuration.
2. Examined the Android manifest and declared application components.
3. Inspected activity code and application logic in JADX-GUI.
4. Reviewed local note storage and logging behaviour.
5. Checked embedded configuration and endpoint references.
6. Recorded security-relevant observations for reporting.

## Key Observations

### 1. Client-side access control

The application contains a hardcoded arithmetic access-code check. The value could be recovered through static code inspection; the recovered value was **4831**.

### 2. Activity logging

The `PreviewActivity` implementation logs note content under the tag `PocketNotesLab`. Logging sensitive user-entered content can expose information through device logs.

### 3. Exported activity

The manifest declares `PreviewActivity` as exported without a manifest-level permission restriction. Exported components should be reviewed to determine whether they can be invoked by other applications and whether appropriate access controls are enforced.

### 4. Local storage

The application stores note content in SharedPreferences named `pocket_notes`, using the key `note`. The preferences are held in the application's private sandbox. No application-level encryption was identified during this review.

### 5. Embedded endpoint

A Base64-encoded configuration value resolves to:

`https://telemetry.example.invalid/v1/sync`

The sync functionality was disabled during the review. The presence of this string alone does not demonstrate that the endpoint was contacted.

## Security Considerations

- Client-side access checks should not be treated as strong security boundaries.
- Sensitive note content should not be written to logs.
- Exported components should have appropriate access controls and input validation.
- Sensitive locally stored information should be protected according to its sensitivity and threat model.
- Embedded endpoint strings should be assessed in context; a string reference is not proof of network activity.

## Limitations

This was a static review. No claim is made that the application contacted the embedded endpoint or that runtime exploitation was performed.

## Evidence and Screenshots

Add the screenshots listed below to this folder. The image links will be inserted into this report after the files are uploaded.

| Planned filename | What it should show |
|---|---|
| `P1-01-UnlockPolicy-AccessCode.png` | JADX-GUI code showing the client-side access-code logic and recovered value. |
| `P1-02-NoteStore-Storage.png` | Code showing SharedPreferences name and note key. |
| `P1-03-PreviewActivity-Logging.png` | The note-content logging statement and log tag. |
| `P1-04-LabConfig-Endpoint.png` | The encoded configuration and the decoded placeholder endpoint, if both are visible in your evidence. |
| `P1-05-Manifest-Components.png` | Manifest view showing the exported activity and relevant component attributes. |

## Conclusion

The static review identified areas requiring attention in client-side access control, logging, exported component configuration, and local data protection. These observations are based on code and manifest inspection and should be interpreted within the limits of static analysis.
