Imagine you have a class that has options.

### Boring Approach

One way of doing this is:

```c++
struct Options {
    bool option_a;
    bool option_b;
    bool option_c;
    bool option_d;
    bool option_e;
};
```

You would set the options like this:

```c++
Options options;
options.option_a = false;
options.option_b = false;
options.option_c = true;
options.option_d = false;
options.option_e = true;
```

Alternatively, you could use an initializer list, but you lose the ability to clearly know which option you are setting (unless you have documentation or an LSP, but that’s beside the point):

```c++
Options options = Options{false, false, true, false, true};
```

### Improved Approach with Enums and Bitwise Operations

A more efficient and expressive way to handle this is by using enums and bitwise operations:

```c++
enum Options {
    OPTION_A = 1 << 0,
    OPTION_B = 1 << 1,
    OPTION_C = 1 << 2,
    OPTION_D = 1 << 3,
    OPTION_E = 1 << 4,
};
```

#### Setting Options
You can combine options using bitwise OR (`|`):

```c++
Options options = OPTION_C | OPTION_A;
```

#### Checking Options
You can check for specific options using bitwise AND (`&`):

```c++
if (options & OPTION_A) { /* do stuff with option_a */ }
if (options & OPTION_B) { /* do stuff with option_b */ }
if (options & OPTION_C) { /* do stuff with option_c */ }
if (options & OPTION_D) { /* do stuff with option_d */ }
if (options & OPTION_E) { /* do stuff with option_e */ }
```

The principle lies in the use of bitwise OR (`|`) to combine options and bitwise AND (`&`) to check for specific options.

---

## In-Depth Explanation of Bitwise Operations

### Binary Representation and Flags
Each option in the `enum` is assigned a unique bit position using the left shift operator (`1 << n`). Here’s what the binary representation looks like:

- `OPTION_A = 1 << 0` (binary: `00001`)
- `OPTION_B = 1 << 1` (binary: `00010`)
- `OPTION_C = 1 << 2` (binary: `00100`)
- `OPTION_D = 1 << 3` (binary: `01000`)
- `OPTION_E = 1 << 4` (binary: `10000`)

These unique binary values ensure that each option corresponds to a distinct bit in the integer representation of the enum.

### Combining Options
When you use the bitwise OR operator (`|`), the binary values are combined. For example:

```c++
Options options = OPTION_A | OPTION_C;
```

Here’s how the operation works:

- `OPTION_A` = `00001`
- `OPTION_C` = `00100`
- Result: `00101`

The result, `00101`, represents both `OPTION_A` and `OPTION_C` being set.

### Checking Options
To check whether a specific option is set, you use the bitwise AND operator (`&`). For example:

```c++
if (options & OPTION_C) {
    // Do something if OPTION_C is enabled
}
```

Here’s how the operation works:

- `options` = `00101` (from the previous example)
- `OPTION_C` = `00100`
- Result: `00100` (non-zero, meaning `OPTION_C` is set)

If the result is non-zero, the condition evaluates to `true`.

### Advantages of This Approach
1. **Efficiency**: Bitwise operations (`|` and `&`) are extremely fast.
2. **Clarity**: Using enums makes the code more expressive and easier to read compared to raw integers or multiple booleans.
3. **Scalability**: Adding more options is straightforward as long as the underlying type has sufficient bits.

### Pitfalls

- **Limited Bits**: Ensure you don’t exceed the number of bits in the underlying type (e.g., 32 for `int`).
- **Type Safety**: Using plain `enum` can lead to unscoped identifiers, implicit conversions and a wide range of other issues. To avoid this, use `enum class` for better type safety. However, `enum class` doesn’t support bitwise operators by default.

#### Enabling Bitwise Operators for `enum class`
You need to define the operators explicitly:

```c++
inline Options operator|(Options lhs, Options rhs) {
    return static_cast<Options>(
        static_cast<std::underlying_type_t<Options>>(lhs) |
        static_cast<std::underlying_type_t<Options>>(rhs)
    );
}

inline bool operator&(Options lhs, Options rhs) {
    return static_cast<std::underlying_type_t<Options>>(lhs) &
           static_cast<std::underlying_type_t<Options>>(rhs);
}
```

### Alternative: Using a Namespace
An alternative to `enum class` is to use a namespace for defining options, which keeps the syntax clean while avoiding the down sides of plain `enum`s.

```c++
namespace Options {
    enum : int {
        A = 1 << 0,
        B = 1 << 1,
        C = 1 << 2,
        D = 1 << 3,
        E = 1 << 4,
    };
}

// ...

Options options = Options::C | Options::A;

// ...

if (options & Option::A) { /* do stuff with option_a */ }
if (options & Option::B) { /* do stuff with option_b */ }
if (options & Option::C) { /* do stuff with option_c */ }
if (options & Option::D) { /* do stuff with option_d */ }
if (options & Option::E) { /* do stuff with option_e */ }

```

This approach provides a simple and effective way to manage bitwise options while keeping the code readable and maintainable.
