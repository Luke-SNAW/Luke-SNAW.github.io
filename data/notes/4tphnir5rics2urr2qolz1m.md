
> https://ecostack.dev/posts/wasm-tinygo-vs-rust-vs-assemblyscript/

The thing you are working on involves sorting large amounts of data, so you test a pure JS implementation first.

> To compare the speed, the test involves the initialization of an array with 100.000 random values. That will be copied 500 times and each time sorted. Each test will be repeated 5 times and the average will be taken.
>
> The tested browsers are Firefox (108.0b6), Edge (107.0.1418.56) and Chrome (107.0.5304.110) on an Intel Macbook Pro 2019.
>
> If curious, the test can be reproduced by using the following repository: [https://github.com/Ecostack/wasm-rust-go-asc](https://github.com/Ecostack/wasm-rust-go-asc)

> Originally, the Go version used an unstable sort as it is the default. This comparison was unfair, as Rust and AssemblyScript use a stable one by default. This has been changed, all variants use stable sorts now.

## [JavaScript](https://ecostack.dev/posts/wasm-tinygo-vs-rust-vs-assemblyscript/#javascript)

```js
function testSort() {
  const length = 100_000
  const arr = new Array(length)
  for (let i = 0; i < arr.length; i++) {
    arr[i] = Math.random()
  }
  const temp = new Array(length)
  for (let i = 0; i < 500; i++) {
    for (let j = 0; j < arr.length; j++) {
      temp[j] = arr[j]
    }
    temp.sort()
  }
}

function measureTime(times, func) {
  console.log("start measuring time")
  console.time("measureTime")
  for (let i = 0; i < times; i++) {
    func()
    console.timeLog("measureTime", i)
  }
  console.timeEnd("measureTime")
}

measureTime(5, () => testSort())
```

A test run with 5 repetition in Firefox shows, it takes around **19,273 milliseconds** on average with the JavaScript solution. The Chrome version takes all the way up to **68,720 ms (+256%)** In Edge, the test is not starting.

_You act surprised and think this took some time, so you get going on implementing it in the other languages._

## [AssemblyScript](https://ecostack.dev/posts/wasm-tinygo-vs-rust-vs-assemblyscript/#assemblyscript)

You start with **AssemblyScript**, as it is most similar to **TypeScript/JavaScript**. Setting up the project was a breeze, with following the guide at the [AssemblyScript website](https://www.assemblyscript.org/getting-started.html#setting-up-a-new-project) .

Now you got yourself the laid out project and type away the AssemblyScript version in the `assembly/index.ts`.

```js
export function testSort(): void {
  const length = 100_000
  const arr = new Array() < u32 > length
  for (let i = 0; i < arr.length; i++) {
    let value = i32((Math.random() * 2.0 - 1.0) * 100)
    arr[i] = value
  }
  const temp = new Array() < u32 > length
  for (let i = 0; i < 500; i++) {
    for (let j = 0; j < length; j++) {
      temp[j] = arr[j]
    }

    temp.sort()
  }
}
```

Finishing up the coding, you compile the whole thing to a wasm binary of 3.5 kb and a runtime of 1.2 kb, which totals to **4.7 kb**.

```bash
asc assembly/index.ts -Ospeed --target release
```

After compiling and running a similar test case with 5 runs inside Firefox, the AssemblyScript version reaches an average of **6,152 milliseconds**. The Chrome version runs on average with **6,405 ms (+4%)** and Edge is the slowest with **6,882 ms (+11%)**

_It gets faster, but you wonder if there is room for improvement, so you have a look at what the other languages are offering. Up next is Rust, [that seems to be quite popular these days?](https://survey.stackoverflow.co/2022/#section-most-loved-dreaded-and-wanted-programming-scripting-and-markup-languages)_

## [Rust](https://ecostack.dev/posts/wasm-tinygo-vs-rust-vs-assemblyscript/#rust)

Up next is Rust, which seems to be a bit more difficult to set up. You follow the [guide for wasm-pack](https://rustwasm.github.io/docs/wasm-pack/quickstart.html) and which will eventually leave you with the `src/lib.rs` where you can start implementing.

```rust
#[wasm_bindgen]
pub fn testSort() {
    const length: usize = 100_000;
    let mut arr: [u8; length] = [0; length];
    for i in 0..arr.len() {
        arr[i] = rand::random()
    }

    let mut temp: [u8; length] = [0; length];
    for i in 0..500 {
        temp = arr.clone();
        temp.sort()
    }
}
```

After fighting with the Rust compiler, you wrap up the implementation and finally compile a Wasm binary (44 kb). It comes with two bootstrap files (16 kb, 14 kb), which all in total are **74 kb**.

```bash
wasm-pack build --scope MYSCOPE
```

The same test case, with the Rust version in Chrome, runs on average with **2,982 ms**. The same thing runs in Firefox around **20% slower** with **3,582 ms** and in Edge around **10% slower** with **3,306 ms**.

_Not bad, down from 19 seconds to 3 seconds. Let’s have a look at Go._

## [Go (TinyGo)](https://ecostack.dev/posts/wasm-tinygo-vs-rust-vs-assemblyscript/#go-tinygo)

The last language in your test is Go, for which you chose the [TinyGo compiler](https://tinygo.org/) .

It produces a significant smaller binary compared to the normal Go compiler but does not support the full standard library, which does not bother you much, as you do not need the whole thing.

After following the [installation guide](https://tinygo.org/getting-started/install/) and the [project setup for TinyGo with Wasm](https://tinygo.org/docs/guides/webassembly/) you have working project where you can edit the `main.go`.

```go
type SortInt []int

func (c SortInt) Len() int           { return len(c) }
func (c SortInt) Swap(i, j int)      { c[i], c[j] = c[j], c[i] }
func (c SortInt) Less(i, j int) bool { return c[i] < c[j] }

//export testSort
func testSort() {
	arr := make(SortInt, 100_000)
	for _i := range arr {
		arr[_i] = rand.Intn(100)
	}
	temp := make(SortInt, len(arr))
	for _i := 0; _i < 500; _i++ {
        copy(temp, arr)
        sort.Stable(temp)
	}
}
```

The compilation step is leaving you with a Wasm binary (20 kb) and the necessary runtime (17 kb), which in total are **37 kb**.

```bash
tinygo build -o wasm.wasm -opt=2 -no-debug -target wasm ./main.go
```

You follow along with your test and discover, that the Go version runs on average **9,546 ms** in Edge, **10,668 ms (+12%)** in Firefox and **9,717 ms (+2%)** in Chrome.

## [Conclusion](https://ecostack.dev/posts/wasm-tinygo-vs-rust-vs-assemblyscript/#conclusion)

With all the tests done, it looks like Rust is leading the pack, closely followed by the AssemblyScript version and then the Go version. The pure JavaScript implementation is far in the back.

The below values were obtained via the Chrome browser.

| Language       | File-size (kb) | Runtime (ms) | Memory (mb) |
| -------------- | -------------- | ------------ | ----------- |
| JavaScript     | **1.3**        | 68,720       | 55.7        |
| AssemblyScript | 4.7            | 6,405        | 31.0        |
| Rust           | 74.0           | **2,982**    | **23.0**    |
| Go             | 37.0           | 9,717        | 24.2        |

Based on your observations, it seems like **Rust** is the safest bet for the fastest execution speed among all tested languages. If file-size is a major factor, one might consider choosing **AssemblyScript**, but it is around two times slower than Rust.

In terms of runtimes, depending on your choice of language, **Chrome** might have the best execution speed among all Wasm runtimes.

| Browser / Runtime | Go (ms)   | Rust (ms) | AssemblyScript (ms) | JS (ms)    |
| ----------------- | --------- | --------- | ------------------- | ---------- |
| Firefox           | 10,668    | 3,582     | **6,152**           | **19,273** |
| Edge              | **9,546** | 3,306     | 6,882               | -          |
| Chrome            | 9,717     | **2,982** | 6,405               | 68,720     |

---

> https://news.ycombinator.com/item?id=33763568

The Rust vs. Go comparison has two key differences:

- The Rust example uses 8 bit unsigned ints vs. Go example uses 32 bit signed ints
- Rust's sort is stable by default whereas Go's is not.

If you tweak the Rust benchmark to use `i32` instead of `u8` and `sort_unstable` instead of `sort`, you should see ~3-4x faster performance.

> https://news.ycombinator.com/item?id=33763859

Made a PR with the fixes, Rust is now 3 times faster than tinygo, and the wasm is almost 3 times smaller (wasm+js is twice as small) as expected.
https://github.com/Ecostack/wasm-rust-go-asc/pull/1

My first foray into wasm, so I probably missed some optimizations like wasm-opt.
