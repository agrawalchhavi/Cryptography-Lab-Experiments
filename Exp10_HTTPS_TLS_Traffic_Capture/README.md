# Experiment 10: Capture HTTPS Traffic and Identify TLS Handshake, Certificates and Cipher Suites

## Aim
To capture HTTPS traffic using Wireshark and identify the TLS handshake, digital certificate, and cipher suite used during secure communication.

## Software/Tools Required
- Wireshark
- Web Browser
- Internet Connection

## Learning Outcomes
1. Capture HTTPS traffic using Wireshark.
2. Identify TLS handshake packets.
3. Locate and inspect a digital certificate.
4. Identify the selected TLS cipher suite.

## Working Procedure

### Step 1: Start Wireshark
1. Open Wireshark.
2. Select the active network interface, such as Wi-Fi or Ethernet.
3. Click **Start Capturing Packets**.

### Step 2: Generate HTTPS Traffic
1. Open a web browser.
2. Visit https://www.google.com.
3. Browse the website for a few seconds.
4. Return to Wireshark and stop the capture.

### Step 3: Display TLS Traffic
Enter the following display filter:

```text
tls
```

Press Enter to display TLS-related packets.

### Step 4: Identify Client Hello
Use the following filter:

```text
tls.handshake.type == 1
```

Select a Client Hello packet and expand:

Transport Layer Security → Handshake Protocol: Client Hello

Observe the following:
- TLS Version
- Random
- Cipher Suites
- Extensions
- Server Name

**Screenshots:**

![Client Hello 1](screenshots/Client_Hello(1).png)

![Client Hello 2](screenshots/Client_Hello(2).png)

### Step 5: Identify Server Hello
Use the following filter:

```text
tls.handshake.type == 2
```

Select the Server Hello packet and expand:

Transport Layer Security → Handshake Protocol: Server Hello

Locate and record the selected cipher suite.

Example: `TLS_AES_128_GCM_SHA256`

**Screenshots:**

![Server Hello 1](screenshots/Server_Hello(1).png)

![Server Hello 2](screenshots/Server_Hello(2).png)

### Step 6: Identify the Digital Certificate
Use the following filter:

```text
tls.handshake.type == 11
```

Select the Certificate packet and expand:

Transport Layer Security → Handshake Protocol: Certificate → Certificates → Certificate

Locate the X.509 certificate information.

### Step 7: Examine Certificate Information
Examine the certificate and identify the following attributes:

1. **Subject:** Shows the entity or domain for which the certificate was issued.
2. **Issuer:** Shows the Certificate Authority that issued the certificate.
3. **Validity:** Shows the Not Before and Not After dates.
4. **Public Key:** Locate Subject Public Key Info and identify the public-key algorithm.
5. **Signature Algorithm:** Identify the algorithm used to sign the certificate.

**Screenshots:**

![Certificate Details 1](screenshots/Certificate_Details(1).png)

![Certificate Details 2](screenshots/Certificate_Details(2).png)

### Step 8: Identify the Selected Cipher Suite
Use the following filter:

```text
tls.handshake.type == 2
```

Open the Server Hello packet and expand:

Handshake Protocol: Server Hello → Cipher Suite

Record the selected cipher suite.

## Useful Wireshark Filters

| Purpose | Filter |
|---|---|
| TLS Traffic | `tls` |
| Client Hello | `tls.handshake.type == 1` |
| Server Hello | `tls.handshake.type == 2` |
| Certificate | `tls.handshake.type == 11` |
| TLS Handshake | `tls.handshake` |
| HTTPS/TCP Traffic | `tcp.port == 443` |

## Observation Table

| S. No. | Parameter | Observation |
|---|---|---|
| 1 | Website | www.google.com |
| 2 | TLS Version | TLS 1.3 |
| 3 | Client Hello | Identified |
| 4 | Server Hello | Identified |
| 5 | Certificate Subject | CN=www.google.com |
| 6 | Certificate Issuer | Google Trust Services (WE2) |
| 7 | Certificate Valid From | 07 October 2026 |
| 8 | Certificate Valid To | 30 December 2026 |
| 9 | Public Key Algorithm | EC Public Key |
| 10 | Signature Algorithm | ecdsa-with-SHA256 |
| 11 | Selected Cipher Suite | TLS_AES_128_GCM_SHA256 |

## Result
The HTTPS traffic was captured using Wireshark. The TLS handshake packets, digital certificate details, TLS version, and selected cipher suite were examined and identified.
