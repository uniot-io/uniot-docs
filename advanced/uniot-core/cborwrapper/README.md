# CBORWrapper

The `CBORWrapper` module is designed to facilitate efficient and structured data serialization and deserialization using CBOR. This module provides robust classes for managing CBOR data structures, handling COSE messages, and integrating cryptographic signing mechanisms.

### Components

[**CBORObject**](cborobject.md)

The `CBORObject` class provides a flexible and intuitive interface for creating, manipulating, and parsing CBOR data structures. It abstracts the complexities of the underlying CBOR library (`cn-cbor`), enabling developers to work with CBOR maps, arrays, integers, strings, and binary data effortlessly. The class also supports nested structures, allowing for the creation of complex and hierarchical data representations.

[**COSE**](cose.md)

The `COSE` header defines enumerations and constants related to COSE messages. These definitions standardize the identification and handling of different COSE message components, ensuring consistent message formatting, parsing, and cryptographic operations across the system.

[**COSEMessage**](cosemessage.md)

The `COSEMessage` class encapsulates the structure and functionality of COSE messages within the Uniot project. It leverages the [`CBORObject`](cborobject.md) class for handling CBOR-encoded data and integrates with cryptographic libraries (such as Ed25519) to provide robust signing and verification mechanisms. The class supports the creation, manipulation, signing, and verification of COSE_Sign1 messages, ensuring data integrity and authenticity in communications.

[**ICOSESigner**](icosesigner.md)

The `ICOSESigner` interface defines a contract for COSE message signers. The interface ensures that all signers provide essential functionalities such as retrieving the key identifier, signing data, and specifying the signing algorithm, thereby enabling secure and standardized message authentication across the system.
