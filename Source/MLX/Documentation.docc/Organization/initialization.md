#  Initialization

Creating MLXArrays.

### Scalar Arrays

A scalar ``MLXArray`` is created from a scalar and has zero dimensions:

```swift
let v1 = MLXArray(true)
let v2 = MLXArray(7)
let v3 = MLXArray(8.5)
```

If an `MLXArray` of a different type is needed there is an initializer:

```swift
// dtype is .float32
let v4 = MLXArray(8.5)

// dtype is .float16
let v5 = MLXArray(Float16(8.5))

// dtype is .float16
let v6 = MLXArray(8.5, dtype: .float16)
```

Sometimes scalars can be used in place of arrays (no need to explicitly create them).
Some functions and operators that work on ``MLXArray`` take a ``ScalarOrArray`` argument or have
an overload that does.  A sampling:

- ``MLXArray/+(_:_:)-2vili``
- ``MLXArray/+(_:_:)-1jn5i``
- ``MLX/minimum(_:_:stream:)``
- ``MLX/pow(_:_:stream:)-7pe7j``
- ``MLX/pow(_:_:stream:)-49xi0``

``ScalarOrArray`` is a protocol that various numeric types (`Int`, `Float`, etc.) implement and it
provides a method to convert the scalar to an ``MLXArray`` using a suggested ``DType``.  This allows:

```swift
let values: [Float16] = [ 0.5, 1.0, 2.5 ]

// a has dtype .float16
let a = MLXArray(values)

// b also has dtype .float16 because this translates (roughly) to:
// t = Int(3).asMLXArray(dtype: .float16)
// let b = a + t
let b = a + 3
```

Scalars will not promote results to `float32` using these functions.

### Multi Value Arrays

Typically MLXArrays are created with many values and potentially many dimensions.  You can create
an MLXArray from another array (literal in this case, but swift `Array` variables work as well):

```swift
// create an array of Int64 with shape [3]
let v1 = MLXArray([1, 2, 3])
```

You can also create an array from a swift `Sequence`:

```swift
// create an array of shape [12] from a sequence
let v1 = MLXArray(0 ..< 12)

// this works with various types of sequences
let v2 = MLXArray(stride(from: Float(0.5), to: Float(1.5), by: Float(0.1)))
```

If you have a `Double` array, you have to convert it as `MLXArray` does not support `Double`:

```swift
// this converts to a Float array behind the scenes
let v1 = MLXArray(converting: [0.1, 0.5])
```

If you have `Data` or a `UnsafePointer` (of various kinds) you can also create an `MLXArray`
from that:

```swift
let data = Data([1, 2, 3, 4])

// directly from Data
let v1 = MLXArray(data, type: UInt8.self)

// or via a pointer
let v2 = data.withUnsafeBytes { ptr in
    MLXArray(ptr, type: UInt8.self)
}
```

When creating using an array or sequence you can also control the shape:

```swift
let v1 = MLXArray(0 ..< 12, [3, 4])
```

### Random Value Arrays

See also `MLXRandom` for creating arrays with random data.

### Other Arrays

There are a number of factory methods to create common array patterns.  For example:

```swift
// an array full of zeros
let zeros = MLXArray.zeros([5, 5])

// 2-d identity array
let identity = MLXArray.identity(5)
```

## Topics

### MLXArray Literal Initializers

- ``MLXArray/init(arrayLiteral:)``

### MLXArray Scalar Initializers

- ``MLXArray/init(_:)-9iiz7``
- ``MLXArray/init(_:)-6zp01``
- ``MLXArray/init(_:)-86r8u``
- ``MLXArray/init(_:)-10m``
- ``MLXArray/init(_:)-96nyv``
- ``MLXArray/init(_:dtype:)``

### MLXArray Array Initializers

- ``MLXArray/init(_:_:)-4n0or``
- ``MLXArray/init(_:_:)-dq8h``
- ``MLXArray/init(_:_:)-89jw1``
- ``MLXArray/init(converting:_:)``
- ``MLXArray/init(_:_:type:)-5esf9``
- ``MLXArray/init(_:_:type:)-f9u5``

### MLXArray Factory Methods

- ``MLXArray/zeros(_:type:stream:)``
- ``MLXArray/zeros(like:stream:)``
- ``MLXArray/ones(_:type:stream:)``
- ``MLXArray/ones(like:stream:)``
- ``MLXArray/eye(_:m:k:type:stream:)``
- ``MLXArray/full(_:values:type:stream:)``
- ``MLXArray/full(_:values:stream:)``
- ``MLXArray/identity(_:type:stream:)``
- ``MLXArray/linspace(_:_:count:stream:)-92x6l``
- ``MLXArray/linspace(_:_:count:stream:)-7m7eg``
- ``MLXArray/repeat(_:count:axis:stream:)``
- ``MLXArray/repeat(_:count:stream:)``
- ``MLXArray/tri(_:m:k:type:stream:)``

### MLXArray Factory Free Methods

- ``MLX/zeros(_:type:stream:)``
- ``MLX/zeros(like:stream:)``
- ``MLX/ones(_:type:stream:)``
- ``MLX/ones(like:stream:)``
- ``MLX/eye(_:m:k:type:stream:)``
- ``MLX/full(_:values:type:stream:)``
- ``MLX/full(_:values:stream:)``
- ``MLX/identity(_:type:stream:)``
- ``MLX/linspace(_:_:count:stream:)-7vj0o``
- ``MLX/linspace(_:_:count:stream:)-6w959``
- ``MLX/repeat(_:count:axis:stream:)``
- ``MLX/repeat(_:count:stream:)``
- ``MLX/tri(_:m:k:type:stream:)``