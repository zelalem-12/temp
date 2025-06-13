#!/bin/bash
set -euo pipefail

# ───────────────────────────────
# 🗂️ Config
# ───────────────────────────────
CERT_DIR=./config/certs
KEY_BITS=4096
DAYS_VALID=3650

TLS_PRIVATE_KEY_FILE="$CERT_DIR/idp_tls_private_key.pem"
TLS_CERT_FILE="$CERT_DIR/idp_tls_certificate.pem"

# ───────────────────────────────
# 📁 Ensure directory exists
# ───────────────────────────────
mkdir -p "$CERT_DIR"

# ───────────────────────────────
# 🔐 Generate TLS private key
# ───────────────────────────────
echo "🔐 Generating RSA ${KEY_BITS}-bit private key for TLS..."
openssl genpkey -algorithm RSA -out "$TLS_PRIVATE_KEY_FILE" -pkeyopt rsa_keygen_bits:$KEY_BITS

# ───────────────────────────────
# 📄 Create self-signed certificate (for local/dev)
# ───────────────────────────────
echo "📄 Creating self-signed TLS certificate..."
openssl req -x509 \
  -new \
  -key "$TLS_PRIVATE_KEY_FILE" \
  -out "$TLS_CERT_FILE" \
  -days $DAYS_VALID \
  -subj "/CN=idp.getchkd.local/O=GetChkd/C=US"

# ───────────────────────────────
# ✅ Done
# ───────────────────────────────
echo "✅ TLS certificate and private key created:"
ls -lh "$CERT_DIR"




https://today-api.proskillowner.com
https://today-api.proskillowner.com/token/top-gainers

