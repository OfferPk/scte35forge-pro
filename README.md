# SCTE35Forge Pro (v1.0.0)

### SCTE-35 (2024), SCTE-104 & Dynamic Ad Insertion (DAI) Studio

---

## Overview

**SCTE35Forge Pro** is an engineering suite and command-line tool built for broadcast transmission engineers, OTT streaming architects, FAST channel operators, and SSAI platform developers. It provides bit-level synthesis, binary inspection, MPEG-2 CRC-32 verification, and normative compliance checking across:

- **ANSI/SCTE 35 (2024)**: Digital Program Insertion Cueing Message  
- **ANSI/SCTE 104**: Automation to Compression System Interface  
- **Apple HLS (RFC 8216bis)**: `#EXT-X-DATERANGE` and `#EXT-X-CUE-OUT/IN`  
- **MPEG-DASH (ISO/IEC 23009-1)**: `EventStream` (`urn:scte:scte35:2014:xml+bin`)

---

## Key Capabilities

1. **Splice Cue Synthesis**:  
   - Generates compliant `splice_insert` (0x05) and `time_signal` (0x06) binary payloads.  
   - Computes 32-bit CRC using the normative MPEG-2 generator polynomial `0x04C11DB7`.  
   - Formats outputs in Base64 (for OTT manifests) and raw Hexadecimal (for MPEG-TS / VANC).  
2. **Binary Inspection & Dissection**:  
   - Decodes arbitrary SCTE-35 Base64 or Hex messages.  
   - Extracts splice commands, 90 kHz presentation timestamps, break durations, and UPID descriptors.  
3. **OTT Manifest Generation**:  
   - Generates production-ready Apple HLS `#EXT-X-DATERANGE` tags with `SCTE35-OUT` hex payloads.  
   - Generates MPEG-DASH `EventStream` XML blocks for MPD manifest injection.  
4. **10-Point Normative Compliance Auditor**:  
   - Validates MPEG-2 section syntax, protocol version, CRC-32 integrity, PTS horizons, Ad-ID UPID formatting, and preroll margins.  
5. **Headless Python CLI**:  
   - Standalone command-line tool (`scte35-cli.py`) for automated terminal workflows, CI/CD validation, and batch processing.

---

## Getting Started

### Web Studio

Open `source-code/index.html` in any modern web browser. Runs 100% locally with zero external dependencies.

### Command-Line Interface

\# Generate 30s splice\_insert cue

python3 build/scte35-cli.py generate \--event-id 1001 \--pts-seconds 2000.0 \--duration 30.0

\# Decode SCTE-35 payload

python3 build/scte35-cli.py decode "/DAWAAAAAAAAAP/wBQb+AAAAAAAiAiB..."

\# Generate HLS / DASH manifest tags

python3 build/scte35-cli.py manifest \--event-id 1001 \--duration 30.0

### Automated Testing

python3 test\_scte35.py