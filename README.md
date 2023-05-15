# Golang Coverage
Need to be aware that if a pkg doesn't have test file default coverage test will skip it, and therefore causing in correct coverage.

For this repository as an example, we only have test case for b package. We expect our test coverage should be 1/4 (due to each pkg have 8 funcs, and we only test 4 funcs of b pkg).

From the below experiments, we can see the later result is the one we desire.

```sh
go test --coverprofile=coverage.out ./...             
?       localhost/test  [no test files]
?       localhost/test/a        [no test files]
ok      localhost/test/b        0.117s  coverage: 50.0% of statements

go tool cover -func=coverage.out         
localhost/test/b/b.go:3:        B1              100.0%
localhost/test/b/b.go:7:        B2              100.0%
localhost/test/b/b.go:11:       B3              100.0%
localhost/test/b/b.go:15:       B4              100.0%
localhost/test/b/b.go:19:       B5              0.0%
localhost/test/b/b.go:23:       B6              0.0%
localhost/test/b/b.go:27:       B7              0.0%
localhost/test/b/b.go:31:       B8              0.0%
total:                          (statements)    50.0%
```

```sh
go test -coverpkg=./... --coverprofile=coverage.out ./...
?       localhost/test  [no test files]
?       localhost/test/a        [no test files]
ok      localhost/test/b        0.154s  coverage: 25.0% of statements in ./...

go tool cover -func=coverage.out                         
localhost/test/a/a.go:3:        A1              0.0%
localhost/test/a/a.go:7:        A2              0.0%
localhost/test/a/a.go:11:       A3              0.0%
localhost/test/a/a.go:15:       A4              0.0%
localhost/test/a/a.go:19:       A5              0.0%
localhost/test/a/a.go:23:       A6              0.0%
localhost/test/a/a.go:27:       A7              0.0%
localhost/test/a/a.go:31:       A8              0.0%
localhost/test/b/b.go:3:        B1              100.0%
localhost/test/b/b.go:7:        B2              100.0%
localhost/test/b/b.go:11:       B3              100.0%
localhost/test/b/b.go:15:       B4              100.0%
localhost/test/b/b.go:19:       B5              0.0%
localhost/test/b/b.go:23:       B6              0.0%
localhost/test/b/b.go:27:       B7              0.0%
localhost/test/b/b.go:31:       B8              0.0%
localhost/test/main.go:3:       main            0.0%
total:                          (statements)    25.0%
```