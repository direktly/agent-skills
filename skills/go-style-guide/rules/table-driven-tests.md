## Table-Driven Tests

Prefer table-driven tests even when there is only a single test case. This keeps
tests consistent, makes them easier to extend, and follows Go’s idiomatic
testing style.

Instead of writing a one-off test for a single scenario, define your test cases
in a slice and iterate over them using `t.Run`. This makes adding new cases
trivial and improves test readability.

### Bad

```go
func TestIsEmpty(t *testing.T) {
	if got := IsEmpty(""); got != true {
		t.Fatalf("got %v, want %v", got, true)
	}
}
```

### Good

```go
func TestIsEmpty(t *testing.T) {
	tests := []struct {
		name  string
		input string
		want  bool
	}{
		{
			name:  "empty string",
			input: "",
			want:  true,
		},
	}

	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			if got := IsEmpty(tt.input); got != tt.want {
				t.Fatalf("got %v, want %v", got, tt.want)
			}
		})
	}
}
```

### Why this matters

- Keeps all tests following the same structure  
- Makes it easy to add more cases without rewriting the test logic  
- Produces clearer test output with named subtests  
- Matches Go community conventions and large-scale codebase practices  

Even if a test starts with a single case, using a table-driven format prepares
the test for future expansion and keeps the codebase stylistically consistent.
