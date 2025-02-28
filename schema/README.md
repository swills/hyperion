# Schema

This folder contains the [OpenAPI-compatible JSON Schema](https://swagger.io/specification/#schema) 
that describes they [hyperion 1.0 spec](https://edgio.github.io/hyperion/versions/1.0/) 

## How the tests work

Not only does this folder contain the schema but the schema is tested against a set of json documents
that are predetermined to either pass or fail. Documents that pass validation have no associated golden result.
Documents that are expected to fail have their actual failures compared against their expected failures located
in the `./golden-results` folder.

You can run the tests by executing `go test` within the current folder.

## Golden Results

Golden results describe the expectations of negative test cases in a repeatable way. This helps us to implement
tests with complex output without manually hard coding the expectations.

The expectations are generated by doing the following:

1. Add a json document that expresses what you want to test in the `./test-fixtures` folder
2. Add a test case to the collection in `node_test.go` or `collection_test.go`, depending on what you're testing
3. Provide a `goldenResultPath` that is unique to the test cases. If your test case does not expect any errors then do not specify a `goldenResultPath`.
4. Run `go test --update`. You'll notice a new file written to `./golden-results` that describes the expected failures.
5. Manually verify the generated results before committing it to source

> Note: if you just need to modify or update the golden-results, just run `go test --update` and manually verify the results are correct before commiting.