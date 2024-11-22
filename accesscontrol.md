# Access Control

## Basically its a way to set where you can **access* certain vars, and funcs

### Swift provides five levels of access control for variables, constants, and functions:

| **Access Level** | **Description**                                                                                          | **Example**                                       |
|-------------------|----------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| `private`         | Accessible only within the enclosing declaration (e.g., a class or struct).                              | `private var myVar = 10`                        |
| `fileprivate`     | Accessible only within the same file.                                                                    | `fileprivate func myFunc() {}`                  |
| `internal`        | Its the default setting and you don even have to really say it                                           | `var myVar = 30`                                |
| `public`          | Accessible from anywhere, but cannot be subclassed or overridden outside the class/struct.               | `public func myFunc() {}`                       |
| `open`            | Same as `public`, but allows subclassing and overriding outside the module.                              | `open class MyClass {}`                         |

### Notes:
- **Default**: If no access level is specified, Swift assumes `internal`.
- `open` is only for classes and class members. SO if you wnan do the override nonsense in structs/enums you gotta use `public`


