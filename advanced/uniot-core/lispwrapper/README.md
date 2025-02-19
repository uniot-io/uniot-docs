# LispWrapper

The `LispWrapper` module is a crucial component within the Uniot Core, designed to integrate Lisp-based scripting capabilities. It provides a seamless interface between Lisp scripts and the underlying hardware and software functionalities.

### Components

[**DefaultPrimitives**](defaultprimitives.md)

The `DefaultPrimitives` component defines a set of primitives essential for interacting with hardware. These primitives serve as the bridge between Lisp scripts and the underlying system functionalities, enabling seamless communication and control.

[**PrimitiveExpeditor**](primitiveexpeditor.md)

The `PrimitiveExpeditor` class is responsible for defining, describing, and managing Lisp primitives. Serving as an intermediary between Lisp scripts and system functionalities, it facilitates the registration and invocation of primitives, ensuring that Lisp code can effectively interact with the underlying Uniot system.

[**LispHelper**](lisphelper.md)

The `LispHelper` component provides a suite of utility functions and definitions that facilitate the integration and management of Lisp. Serving as a foundational layer, it simplifies the interaction between Lisp scripts and the underlying system by offering type definitions, type-checking mechanisms, and helper functions.

[**unLisp**](unlisp.md)

The `unLisp` class is responsible for managing the Lisp execution environment, handling primitive registrations, and facilitating the evaluation of Lisp scripts. As a singleton, it ensures that only one instance of the Lisp environment exists throughout the application's lifecycle, providing a unified interface for Lisp interactions.
