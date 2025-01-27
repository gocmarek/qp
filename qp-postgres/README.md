# Quick Pool for PostgreSQL

> High Performance Async Generic Pool PostgreSQL Adapter

[![Crates.io](https://img.shields.io/crates/v/qp-postgres?style=for-the-badge)](https://crates.io/crates/qp-postgres)
[![Docs.rs](https://img.shields.io/docsrs/qp-postgres?style=for-the-badge)](https://docs.rs/qp-postgres)
[![Rust](https://img.shields.io/badge/rust-2021-black.svg?style=for-the-badge)](https://doc.rust-lang.org/edition-guide/rust-2021/index.html)
[![Rust](https://img.shields.io/badge/rustc-1.56+-black.svg?style=for-the-badge)](https://blog.rust-lang.org/2021/10/21/Rust-1.56.0.html)
[![GitHub Workflow](https://img.shields.io/github/workflow/status/Astro36/qp/CI?style=for-the-badge)](https://github.com/Astro36/qp/actions/workflows/ci.yml)
[![Codecov](https://img.shields.io/codecov/c/gh/Astro36/qp?style=for-the-badge)](https://codecov.io/gh/Astro36/qp)
[![Crates.io](https://img.shields.io/crates/d/qp-postgres?style=for-the-badge)](https://crates.io/crates/qp-postgres)
[![License](https://img.shields.io/crates/l/qp-postgres?style=for-the-badge)](./LICENSE) 

## Usage

### Example

#### Simple Query

```rust
use tokio_postgres::NoTls;

#[tokio::main]
async fn main() {
    let config = "postgresql://postgres:postgres@localhost".parse().unwrap();
    let pool = qp_postgres::connect(config, NoTls, 8);
    let client = pool.acquire().await.unwrap();
    let row = client.query_one("SELECT 1", &[]).await.unwrap();
    let int: i32 = row.get(0);
    dbg!(&int);
}
```

#### Web Frameworks

- [`qp-postgres` + `axum`](/examples/postgres-axum)
- [`qp-postgres` + `hyper`](/examples/postgres-hyper)

## Alternatives

| Backend          | Adapter             | Version                      |
| ---------------- | ------------------- | ---------------------------- |
| [tokio-postgres] | [bb8-postgres]      | ![bb8-postgres-version]      |
| [tokio-postgres] | [deadpool-postgres] | ![deadpool-postgres-version] |
| [tokio-postgres] | [mobc-postgres]     | ![mobc-postgres-version]     |
| [postgres]       | [r2d2-postgres]     | ![r2d2-postgres-version]     |
| [sqlx]           | -                   | ![sqlx-version]              |

### Performance Comparison

> PostgreSQL Total Query Time Benchmark

![Benchmark](/../../../rust-pool-benchmark/blob/main/postgres/results/benchmark(p08_w64).svg)

![Benchmark](/../../../rust-pool-benchmark/blob/main/postgres/results/benchmark(p16_w64).svg)

For more information, see [Rust Pool Benchmark](/../../../rust-pool-benchmark/blob/main/postgres/results/README.md).

## License

```text
Copyright (c) 2022 Seungjae Park

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

*Quick Pool for PostgreSQL* is licensed under the [MIT License](/qp-postgres/LICENSE).

[tokio-postgres]: https://crates.io/crates/tokio-postgres
[postgres]: https://crates.io/crates/postgres
[sqlx]: https://crates.io/crates/sqlx

[bb8-postgres]: https://crates.io/crates/bb8-postgres
[deadpool-postgres]: https://crates.io/crates/deadpool-postgres
[mobc-postgres]: https://crates.io/crates/mobc-postgres
[qp-postgres]: https://crates.io/crates/qp-postgres
[r2d2-postgres]: https://crates.io/crates/r2d2-postgres

[bb8-postgres-version]: https://img.shields.io/crates/v/bb8-postgres?style=for-the-badge
[deadpool-postgres-version]: https://img.shields.io/crates/v/deadpool-postgres?style=for-the-badge
[mobc-postgres-version]: https://img.shields.io/crates/v/mobc-postgres?style=for-the-badge
[qp-postgres-version]: https://img.shields.io/crates/v/qp-postgres?style=for-the-badge
[r2d2-postgres-version]: https://img.shields.io/crates/v/r2d2-postgres?style=for-the-badge
[sqlx-version]: https://img.shields.io/crates/v/sqlx?style=for-the-badge
