<!--

@license Apache-2.0

Copyright (c) 2024 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# dtrmv

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Perform one of the matrix-vector operations `x = A*x` or `x = A^T*x`.

<section class = "usage">

## Usage

```javascript
var dtrmv = require( '@stdlib/blas-base-dtrmv' );
```

#### dtrmv( order, uplo, trans, diag, N, A, LDA, x, sx )

Performs one of the matrix-vector operations `x = A*x` or `x = A^T*x`, where `x` is an `N` element vector and `A` is an `N` by `N` unit, or non-unit, upper or lower triangular matrix.

```javascript
var Float64Array = require( '@stdlib/array-float64' );

var A = new Float64Array( [ 1.0, 2.0, 3.0, 0.0, 1.0, 2.0, 0.0, 0.0, 1.0 ] );
var x = new Float64Array( [ 1.0, 2.0, 3.0 ] );

dtrmv( 'row-major', 'upper', 'no-transpose', 'unit', 3, A, 3, x, 1 );
// x => <Float64Array>[ 14.0, 8.0, 3.0 ]
```

The function has the following parameters:

-   **order**: storage layout.
-   **uplo**: specifies whether `A` is an upper or lower triangular matrix.
-   **trans**: specifies whether `A` should be transposed, conjugate-transposed, or not transposed.
-   **diag**: specifies whether `A` has a unit diagonal.
-   **N**: number of elements along each dimension of `A`.
-   **A**: input matrix stored in linear memory as a [`Float64Array`][mdn-float64array].
-   **lda**: stride of the first dimension of `A` (a.k.a., leading dimension of the matrix `A`).
-   **x**: input vector [`Float64Array`][mdn-float64array].
-   **sx**: `x` stride length.

The stride parameters determine how elements in the input arrays are accessed at runtime. For example, to iterate over the elements of `x` in reverse order,

```javascript
var Float64Array = require( '@stdlib/array-float64' );

var A = new Float64Array( [ 1.0, 2.0, 3.0, 0.0, 1.0, 2.0, 0.0, 0.0, 1.0 ] );
var x = new Float64Array( [ 1.0, 2.0, 3.0 ] );

dtrmv( 'row-major', 'upper', 'no-transpose', 'unit', 3, A, 3, x, -1 );
// x => <Float64Array>[ 1.0, 4.0, 10.0 ]
```

Note that indexing is relative to the first index. To introduce an offset, use [`typed array`][mdn-typed-array] views.

<!-- eslint-disable stdlib/capitalized-comments -->

```javascript
var Float64Array = require( '@stdlib/array-float64' );

// Initial arrays...
var x0 = new Float64Array( [ 1.0, 1.0, 1.0, 1.0 ] );
var A = new Float64Array( [ 1.0, 2.0, 3.0, 0.0, 1.0, 2.0, 0.0, 0.0, 1.0 ] );

// Create offset views...
var x1 = new Float64Array( x0.buffer, x0.BYTES_PER_ELEMENT*1 ); // start at 2nd element

dtrmv( 'row-major', 'upper', 'no-transpose', 'unit', 3, A, 3, x1, 1 );
// x0 => <Float64Array>[ 1.0, 6.0, 3.0, 1.0 ]
```

#### dtrmv.ndarray( uplo, trans, diag, N, A, sa1, sa2, oa, x, sx, ox )

Performs one of the matrix-vector operations `x = A*x` or `x = A^T*x`, using alternative indexing semantics and where `x` is an `N` element vector and `A` is an `N` by `N` unit, or non-unit, upper or lower triangular matrix.

```javascript
var Float64Array = require( '@stdlib/array-float64' );

var A = new Float64Array( [ 1.0, 2.0, 3.0, 0.0, 1.0, 2.0, 0.0, 0.0, 1.0 ] );
var x = new Float64Array( [ 1.0, 2.0, 3.0 ] );

dtrmv.ndarray( 'upper', 'no-transpose', 'unit', 3, A, 3, 1, 0, x, 1, 0 );
// x => <Float64Array>[ 14.0, 8.0, 3.0 ]
```

The function has the following additional parameters:

-   **sa1**: stride of the first dimension of `A`.
-   **sa2**: stride of the second dimension of `A`.
-   **oa**: starting index for `A`.
-   **ox**: starting index for `x`.

While [`typed array`][mdn-typed-array] views mandate a view offset based on the underlying buffer, the offset parameters support indexing semantics based on starting indices. For example,

```javascript
var Float64Array = require( '@stdlib/array-float64' );

var A = new Float64Array( [ 1.0, 2.0, 3.0, 0.0, 1.0, 2.0, 0.0, 0.0, 1.0 ] );
var x = new Float64Array( [ 1.0, 2.0, 3.0 ] );

dtrmv.ndarray( 'upper', 'no-transpose', 'unit', 3, A, 3, 1, 0, x, -1, 2 );
// x => <Float64Array>[ 1.0, 4.0, 10.0 ]
```

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   `dtrmv()` corresponds to the [BLAS][blas] level 2 function [`dtrmv`][blas-dtrmv].

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
var discreteUniform = require( '@stdlib/random-array-discrete-uniform' );
var dtrmv = require( '@stdlib/blas-base-dtrmv' );

var opts = {
    'dtype': 'float64'
};

var N = 5;

var A = discreteUniform( N*N, -10.0, 10.0, opts );
var x = discreteUniform( N, -10.0, 10.0, opts );

dtrmv( 'column-major', 'upper', 'no-transpose', 'unit', N, A, N, x, 1 );
console.log( x );

dtrmv.ndarray( 'upper', 'no-transpose', 'unit', N, A, 1, N, 0, x, 1, 0 );
console.log( x );
```

</section>

<!-- /.examples -->

<!-- C interface documentation. -->

* * *

<section class="c">

## C APIs

<!-- Section to include introductory text. Make sure to keep an empty line after the intro `section` element and another before the `/section` close. -->

<section class="intro">

</section>

<!-- /.intro -->

<!-- C usage documentation. -->

<section class="installation">

## Installation

```bash
npm install @stdlib/blas-base-dtrmv
```

Alternatively,

-   To load the package in a website via a `script` tag without installation and bundlers, use the [ES Module][es-module] available on the [`esm`][esm-url] branch (see [README][esm-readme]).
-   If you are using Deno, visit the [`deno`][deno-url] branch (see [README][deno-readme] for usage intructions).
-   For use in Observable, or in browser/node environments, use the [Universal Module Definition (UMD)][umd] build available on the [`umd`][umd-url] branch (see [README][umd-readme]).

The [branches.md][branches-url] file summarizes the available branches and displays a diagram illustrating their relationships.

To view installation and usage instructions specific to each branch build, be sure to explicitly navigate to the respective README files on each branch, as linked to above.

</section>

<section class="usage">

### Usage

```c
TODO
```

#### TODO

TODO.

```c
TODO
```

TODO

```c
TODO
```

</section>

<!-- /.usage -->

<!-- C API usage notes. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="notes">

</section>

<!-- /.notes -->

<!-- C API usage examples. -->

<section class="examples">

### Examples

```c
TODO
```

</section>

<!-- /.examples -->

</section>

<!-- /.c -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2024. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/blas-base-dtrmv.svg
[npm-url]: https://npmjs.org/package/@stdlib/blas-base-dtrmv

[test-image]: https://github.com/stdlib-js/blas-base-dtrmv/actions/workflows/test.yml/badge.svg?branch=main
[test-url]: https://github.com/stdlib-js/blas-base-dtrmv/actions/workflows/test.yml?query=branch:main

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/blas-base-dtrmv/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/blas-base-dtrmv?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/blas-base-dtrmv.svg
[dependencies-url]: https://david-dm.org/stdlib-js/blas-base-dtrmv/main

-->

[chat-image]: https://img.shields.io/gitter/room/stdlib-js/stdlib.svg
[chat-url]: https://app.gitter.im/#/room/#stdlib-js_stdlib:gitter.im

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/blas-base-dtrmv/tree/deno
[deno-readme]: https://github.com/stdlib-js/blas-base-dtrmv/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/blas-base-dtrmv/tree/umd
[umd-readme]: https://github.com/stdlib-js/blas-base-dtrmv/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/blas-base-dtrmv/tree/esm
[esm-readme]: https://github.com/stdlib-js/blas-base-dtrmv/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/blas-base-dtrmv/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/blas-base-dtrmv/main/LICENSE

[blas]: http://www.netlib.org/blas

[blas-dtrmv]: https://www.netlib.org/lapack/explore-html/d6/d1c/group__trmv_ga7b90369d2b2b19f78f168e10dd9eb8ad.html#ga7b90369d2b2b19f78f168e10dd9eb8ad

[mdn-float64array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Float64Array

[mdn-typed-array]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypedArray

</section>

<!-- /.links -->
