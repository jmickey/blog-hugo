---
date: "2019-11-04"
authors: ["jmickey"]
slug: "go-build-tags-testing"
title: "Separate Your Go Tests with Build Tags"
description: "Separate and run different test types with Go build tags."
categories: ["Development"]
tags: [
    "Go",
    "Testing",
    "HowTo"
]
---

Have you ever wanted to separate your unit tests from your integration or smoke tests? Go has a built-in mechanism for allowing you to logically separate your tests, in addition to adding conditionals (e.g. operating system or CPU architecture) with Build Tags.

## What are Build Tags

Build tags are a directive provided, in the form of a single line comment, at the top of a `.go` source file that tells the Go compiler important information about how it should deal with that file when `go build` is run.

For example, the following file will only be included in the build if the `GOOS=linux` environment variable is set:

```go
// +build linux

package mypackage

...
```

The build tag needs to be placed as close to the top of the file as possible, and must have a blank line beneath it.

Tags can also be negated with the `!` operator. E.g. A file with `// +build !linux` will be included in all builds that aren't on linux.

Tags can contain multiple conditions. If the conditions are on the same line then they are evaluated as an OR condition. If they're on separate lines they're evaluated as an AND condition.

```go
// +build linux darwin
// +build amd64

package mypackage

...
```

The above example file will only be included in `linux/amd64` and `darwin/amd64` builds.

## Separating Tests

Build tags can also be used to separate different types of tests, such as unit and integration tests, within separate `_test.go` files.

Let's continue with the example of unit and integration tests.

`myfile_test.go`:
```go
package mypackage

import "testing"

...
```

`myfile_integration_test.go`:
```go
// +build integration

package mypackage

import "testing"

...
```

There are two file examples shown above, the `myfile_integration_test.go` file contains a build tag of `// +build integration`, while the `myfile_test.go` file, where unit tests will be stored, contains no build tag. 

When running `go test` in the directory where these files are stored the Go test runner will only run the tests in `myfile_test.go`. To run the tests within `myfile_integration_test.go` the `--tags` flag will need to be provided - `go test --tags=integration`. 

There is one small problem though. Those following along probably would have picked up on this already. When running `go test --tags=integration` the Go test runner still runs the unit tests! To avoid this you can add a negation to the non-integration tests files, like so:

`myfile_test.go`
```go
// +build !integration

package mypackage

import "testing"

...
```

With the above build tag included in all unit test files, the Go test runner will continue to run the tests when `go test` is used, but they will be excluded when running `go test --tags=integration`.

## Why?

There are plenty of reasons developers might want to separate tests. Some simple example might be:

- Integration tests are often slower, so you may want to only run them after the unit test (which are often much faster) have passed.
- Smoke tests that are run against the live application, generally after a deployment.
- Deploying the same app to different tenants.

Of course, this is by no means an exhaustive list!

## Conclusion

Build tags are a very useful tool within the Go ecosystem, and there are plenty of other possibilities above and beyond this one example. Head over to the [`go/build` package](https://golang.org/pkg/go/build/) documentation for more information!

Thanks for reading.
