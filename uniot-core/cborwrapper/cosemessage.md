# COSEMessage

The `COSEMessage` class encapsulates the structure and functionality of COSE messages within the Uniot project. It leverages the [`CBORObject`](cborobject.md) class for handling CBOR-encoded data and integrates with cryptographic libraries (such as Ed25519) to provide robust signing and verification mechanisms. The class supports the creation, manipulation, signing, and verification of COSE_Sign1 messages, ensuring data integrity and authenticity in communications.

**Constructor and Destructor:**

* **`COSEMessage()`**\
  Constructs an empty `COSEMessage` instance. Initializes a new COSE_Sign1 message, setting up protected and unprotected headers, payload, and signature fields.

* **`COSEMessage(Bytes buf)`**\
  Constructs a `COSEMessage` instance from a given byte buffer. Parses the provided byte buffer to populate the COSE_Sign1 message fields. Sets the read success flag based on the parsing outcome.

* **`virtual ~COSEMessage()`**\
  Destructor that cleans up the COSE message. Frees allocated resources and resets internal pointers to prevent memory leaks.

**Message Handling:**

* **`bool read(const Bytes &buf)`**\
  Decodes the byte buffer and extracts the protected header, unprotected header, payload, and signature fields. Validates the structure and content of the COSE message.

* **`bool wasReadSuccessful() const`**\
  Checks if the last read operation was successful.

**Header Manipulation:**

* **`Bytes getProtectedHeader()`**\
  Extracts the protected header portion of the COSE message for inspection or modification.

* **`CBORObject getUnprotectedHeader()`**\
  Provides access to the unprotected headers, allowing for the addition or modification of header fields.

* **`Bytes getUnprotectedKid()`**\
  Extracts the Key Identifier (`kid`) used for identifying the key associated with the COSE message.

**Payload and Signature:**

* **`Bytes getPayload()`**\
  Retrieves the payload of the COSE message.

* **`Bytes getSignature()`**\
  Retrieves the signature of the COSE message.

**Signing and Verification:**

* **`void sign(const ICOSESigner &signer, const Bytes &external = Bytes())`**\
  Signs the COSE message using the provided signer.

  * **`signer`** (`const ICOSESigner &`): The signer object implementing the [`ICOSESigner`](icosesigner.md) interface.
  * **`external`** (`const Bytes &`, optional): External Additional Authenticated Data (AAD) to include in the signature.

* **`bool verify(const Bytes &publicKey)`**\
  Verifies the signature of the COSE message using the provided public key.

**Serialization:**

* **`Bytes build() const`**\
  Serializes the `COSEMessage` into a byte buffer.

**State Management:**

* **`bool isSigned()`**\
  Checks if the COSE message has been signed.

* **`void clean()`**\
  Resets the `COSEMessage` to its initial state.

**Private Methods:**

* **`bool _read(const Bytes &buf)`**\
  Internal method to parse a byte buffer and populate the COSE message fields.

* **`void _create()`**\
  Initializes the internal CBOR structure for a new COSE_Sign1 message.

* **`void _clean()`**\
  Cleans up the internal CBOR structure and resets pointers.

* **`bool _setProtectedHeader(const CBORObject &pHeader)`**\
  Sets the protected header of the COSE message.

* **`bool _setSignature(const Bytes &signature)`**\
  Sets the signature of the COSE message.

* **`Bytes _toBeSigned(const Bytes &external = Bytes())`**\
  Builds the Sig_structure as defined in the COSE specification, which includes the context, protected header, external AAD, and payload. This sequence is what the signer uses to generate the signature.

  * **`external`** (`const Bytes &`, optional): External Additional Authenticated Data (AAD) to include in the signature.
