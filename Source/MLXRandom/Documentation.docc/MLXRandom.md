# ``MLXRandom``

Collection of functions related to random number generation.

Random sampling functions in MLX use an implicit global PRNG state by default. However, all 
functions take an optional key keyword argument for when more fine-grained control or explicit state management is needed.

For example, you can generate random numbers with:

```swift
for _ in 0 ..< 3:
  print(MLXRandom.uniform())
```

which will print a sequence of unique pseudo random numbers. Alternatively you can explicitly set the key:

```swift
ley key = MLXRandom.key(0)
for _ in 0 ..< 3:
  print(MLXRandom.unfiform(key: key))
```

which will yield the same pseudo random number at each iteration.

Following [JAX’s PRNG design](https://jax.readthedocs.io/en/latest/jep/263-prng.html) we use a
splittable version of Threefry, which is a counter-based PRNG.