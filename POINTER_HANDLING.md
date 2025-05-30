# Pointer Handling Best Practices

This document outlines best practices for handling pointers in Go, especially when working with the GitHub API client.

## Common Patterns

### Checking for nil pointers

Always check if a pointer is nil before dereferencing it:

```go
if somePointer != nil {
    // Now it's safe to use *somePointer
    value := *somePointer
}
```

### Appending to pointer strings

When appending to a string that's represented as a pointer:

```go
// Wrong:
result.Message += "some text"  // Will fail if result.Message is *string

// Correct:
if result.Message != nil {
    *result.Message += "some text"
}
```

### Boolean pointer conditions

When using a boolean pointer in a condition:

```go
// Wrong:
if boolPointer {  // This checks if the pointer is non-nil, not its value

// Correct:
if boolPointer != nil && *boolPointer {
    // This checks both that the pointer exists and its value is true
}
```

## GitHub API Client Specifics

The GitHub API client often returns pointers to primitive types. This is to distinguish between "field not present" (nil) and "field present but empty" (non-nil pointer to empty/zero value).

### Common GitHub API pointer patterns

```go
// Creating a pointer to a string
stringPtr := github.String("some string")

// Creating a pointer to a bool
boolPtr := github.Bool(true)

// Creating a pointer to an int
intPtr := github.Int(42)
```

Always use these helper functions rather than taking the address of literals directly.
