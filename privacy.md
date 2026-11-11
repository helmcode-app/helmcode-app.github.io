---
layout: page
title: "Privacy Policy"
description: "How HelmCode upholds strict, transparent data privacy for developers across the iPad client and self-hosted runner-core daemon."
keywords: "HelmCode privacy policy, iPad coding privacy, self-hosted data security, runner-core security, zero cloud telemetry"
permalink: /privacy/
---

At **HelmCode**, we believe developer privacy is fundamental. Source code constitutes a creator's core intellectual property, proprietary engineering asset, and professional craft. Our governing principle is unambiguous: **your code and credentials belong entirely to you, and we have neither the desire nor the technical infrastructure to access them.**

This Privacy Policy explains what data HelmCode and the `runner-core` daemon interact with, how credentials are protected on your iPad, and why our decentralized architecture guarantees maximum privacy.

---

## Architectural Privacy by Design

> **The Core Guarantee**: HelmCode does not operate any centralized cloud proxy, repository storage cluster, or source code indexing service. There is no middleman between your iPad and your self-hosted runner.

<div class="architecture-diagram-wrapper">
  <img src="{{ '/assets/images/privacy-architecture.svg' | relative_url }}" alt="HelmCode Architectural Privacy by Design" class="architecture-diagram-img" width="960" height="500" loading="eager">
</div>

---

## 1. Information We Do NOT Collect

We do not collect, monetize, log, or transmit any of the following categories of data:

- **Source Code & Workspace Files**: Neither the HelmCode client nor our organization has access to the contents of your repositories, file trees, Git commits, branches, or code diffs.
- **Keystrokes & Editor Telemetry**: Everything typed in the CodeMirror 6 editor is processed entirely within local client memory. We do not track keystroke timings, cursor positions, or typing habits.
- **No Third-Party Analytics or Tracking SDKs**: The application contains zero commercial tracking SDKs, zero advertising identifiers (such as Apple's IDFA), and zero third-party telemetry libraries.
- **No Account Profiles**: You do not need to register an account with HelmCode to use the client or self-host `runner-core`. We do not collect names, phone numbers, or email addresses.

---

## 2. Information Stored Locally on Your iPad

To provide a seamless developer experience across app restarts, HelmCode stores minimal, strictly necessary data directly on your hardware:

### 2.1 Hardware-Backed Keychain Storage
- **Device Pairing Tokens**: When you pair your iPad client with a `runner-core` instance using a setup code, the resulting authorization Bearer token is written directly to the **Apple Keychain Services** with hardware-level encryption (`kSecAttrAccessibleAfterFirstUnlock`).
- These tokens never appear in plain-text preference files and are inaccessible to other apps.
- Disconnecting a runner in settings permanently purges the associated credentials from your Keychain.

### 2.2 Local App Preferences (`UserDefaults`)
- Non-sensitive UI layout parameters are cached in your local sandbox:
  - Active color theme (Light, Dark, OneDark);
  - Editor font family and font size preferences;
  - Sidebar navigator state (e.g., Files vs. Source Control);
  - Inspector/Commander column visibility toggles;
  - Sanitized project display names and runner host URLs.

### 2.3 Transient Buffer Cache
- While editing, files in active tabs may be cached in transient application memory or sandbox storage to protect against accidental loss during sudden app termination or memory pressure. When synchronized, changes write directly to your runner's Virtual File System (VFS).

---

## 3. Data Flow with the Self-Hosted runner-core Daemon

3.1 **Direct Peer-to-Peer Communication**: All network communication occurs exclusively between your iPad client and the address of the `runner-core` daemon you configure (via HTTP REST and WebSocket connections).

3.2 **Virtual Filesystem (VFS) Confinement**: The Go-based `helm-vfs` engine inside `runner-core` interacts only with the workspace path explicitly mounted into the container (e.g., `/app/workspace`). It does not harvest or index unmounted directories on your host server.

3.3 **Transport Security Recommendation**: Because communication transmits code snippets, file trees, and terminal streams, **we strongly recommend using encrypted transport protocols (HTTPS and WSS)** when accessing your runner over public networks. This can be achieved through reverse proxies (such as Nginx, Caddy, or Cloudflare Tunnel) or encrypted mesh overlays (such as Tailscale or WireGuard).

---

## 4. Third-Party AI Models & ACP Harnesses

When you engage the **Agent Commander** to assist with coding, debugging, or test generation:

4.1 **Context Dispatch**: The runner daemon constructs prompts and attaches relevant workspace context (such as files selected with `@file` or skill invocations with `/skill`) and forwards them directly to the AI model provider you have configured (e.g., Anthropic, OpenAI, Cursor, or OpenCode).

4.2 **Independent Provider Policies**: Data sent to external AI providers is governed by the respective provider's terms of service and privacy policies:
- Anthropic: [anthropic.com/privacy](https://www.anthropic.com/privacy)
- OpenAI: [openai.com/privacy](https://openai.com/privacy)
- Most enterprise and developer API tiers provide contractual commitments that user API inputs and outputs will not be used to train foundational models. We encourage you to review the policy of your chosen harness.

4.3 **API Key Security**: Your third-party model API keys reside on your own `runner-core` server configuration (e.g., in `.env` files or secure environment variables) or inside client Keychain storage. HelmCode maintains no access to these keys.

---

## 5. System Permissions on iPadOS

HelmCode requests only permissions strictly necessary for core engineering functionality on iPad:

| Permission | Purpose | Necessity |
| :--- | :--- | :--- |
| **Local Network** | Enables discovery and direct WebSocket pairing with runner-core instances residing on your local Wi-Fi or home subnet. | Required for LAN runners |
| **Internet Access** | Allows the app to connect to remote self-hosted runners and download offline syntax highlighting grammar bundles. | Essential |
| **Notifications (Optional)** | Delivers alerts when long-running compiler tasks or background Docker builds finish execution. | Optional (can be disabled) |

---

## 6. User Control & Complete Data Deletion

You retain absolute dominion over your data at all times:

- **Unpairing a Runner**: In HelmCode Settings, tap to disconnect or remove any registered runner. All authentication tokens and project caches associated with that runner are immediately erased from the Keychain and local storage.
- **Complete App Deletion**: Uninstalling HelmCode from your iPad removes all sandboxed caches, offline buffers, and user settings stored on the device.
- **Server-Side Teardown**: To remove all traces on your server, simply stop and remove the Docker container and volumes:
  ```bash
  docker compose down -v
  ```

---

## 7. Open Source Verification & Auditability

Trust requires transparency. The complete source code for both the HelmCode iPad client application and the `runner-core` execution engine is open source:

- You are invited to independently audit network calls, Keychain interaction routines, and VFS file handlers in our repositories.
- You can build the application directly from source using Xcode targeting iPad, ensuring that the binaries you run match the open-source codebase exactly.

---

## 8. Changes to this Privacy Policy

We may update this Privacy Policy from time to time to account for architectural enhancements or regulatory requirements. Any modifications will be posted to this page with an updated "Last Updated" revision date.

---

## 9. Contact Us

If you have questions, feedback, or security-related inquiries regarding our privacy practices, please contact us via GitHub:

- **GitHub Organization**: [github.com/helmcode-app](https://github.com/helmcode-app)
- **Security & Privacy Issues**: [github.com/helmcode-app/HelmCode/issues](https://github.com/helmcode-app/HelmCode/issues)
