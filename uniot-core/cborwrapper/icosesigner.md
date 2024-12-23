# ICOSESigner

The `ICOSESigner` interface defines a contract for COSE message signers. The interface ensures that all signers provide essential functionalities such as retrieving the key identifier, signing data, and specifying the signing algorithm, thereby enabling secure and standardized message authentication across the system.

**Interface Definition:**

```cpp
namespace uniot {
class ICOSESigner {
 public:
  virtual ~ICOSESigner() {}

  // Retrieves the Key Identifier used in the COSE message
  virtual Bytes keyId() const = 0;

  // Signs the provided data and returns the signature
  virtual Bytes sign(const Bytes &data) const = 0;

  // Specifies the cryptographic algorithm used for signing
  virtual COSEAlgorithm signerAlgorithm() const = 0;
};
}  // namespace uniot
