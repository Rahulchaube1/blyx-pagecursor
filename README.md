<img src="assets/logo.png" width="112" height="112" alt="Blyx penguin turning to the next page of keys after a bookmarked cursor.">

# PageCursor

Find a keyset page strictly after a cursor in sorted keys. This Blyx library is part of the databases and migrations collection.

Offset pagination on changing data can repeat records. Validate the ordered key and return the final emitted key for the next request. [PostgreSQL, ordered pagination](https://www.postgresql.org/docs/current/queries-limit.html)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-pagecursor.git
cd blyx-pagecursor
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-pagecursor) · [Package page](https://www.blyx-lang.space/packages/pagecursor) · [Handbook](https://doc.blyx-lang.space/guide/grebe)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-pagecursor.git vendor/pagecursor
```

```blyx
use vendor::pagecursor::pagecursor;

fn main() {
    let keys = [1, 4, 7, 9];
    let cursor = 3.0;
    let size = 2.0;
    let result = pagecursor_after(keys, cursor, size);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
1
3
1
```

## API

`pagecursor_after(keys, cursor, size)`

Returns [first index, exclusive end, has more]. Verifies strict ordering, then uses binary search. An absent cursor is valid. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| keys | Vector of values, each a exact signed integer |
| cursor | A exact signed integer |
| size | A positive exact integer |

## In use

[Grebe](https://github.com/Rahulchaube1/blyx-grebe) uses this module to build a repeatable keyset page and return the exact next cursor.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-pagecursor/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). Read the [artwork notice](assets/NOTICE.txt) for credits.

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
