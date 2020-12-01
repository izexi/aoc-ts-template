## Usage

```
npm start --day=DAY --part=PART
```
- Where `0<DAY<26` and `0<PART<3`
- E.g: To run day 7, part 2 that would be `npm start --day=7 --part=2`


## Util

> The `parseInput` function is already imported and called at the top of each file.

By default, the function will return the `input.txt` (for the according day which is determined by the flag mentioned above) splitted by `'\n'` as the delimiter and it will also be mapped into numbers by default.

This behaviour can be modified by overriding these options via the [`SplitOptions`](https://github.com/izexi/aoc-ts-template/blob/master/src/util/index.ts#L3-L11) param, here are some examples to illustrate that:

Let's say the `input.txt` looks like
```
1
2
3
```
In most cases, `[1, 2, 3]` is what we want, which is exactly what `parseInput()` would do (`parseInput({ split: { delim: '\n', mapper: (e) => Number(e) } }))` would also do the exact same).

---
Now, let's say the input looked like

```
A
B
C
```

Obviously, we don't want the `SplitOptions.mapper` to be `Number` (which is the default), so we can override this like so: `parseInput({ split: { mapper: false } })`. This would split the input by the default `'\n'` and since we passed `false` it would not map the splitted string.

---

There may also be inputs where the delimiter new lines like so

```
1 2 3
```

As shown above the delimiter here is infact `' '` which we can pass as the `SplitOptions.delimiter` and since we probably want to map that into numbers we don't need to worry about setting the `mapper` property since that is what it does by default: `parseInput({ split: { delimiter: ' ' } })`

---

Lastly, there may be an input that we don't want to modify at all and just handle the raw input such as

```
ABC
```
We can get that by doing: `parseInput({ split: false })`

---

There may a scenrio where we need to map each item in the input, for example let's say that we wanted to double each number:

```
1
2
3
```
We can do that like so: `parseInput({ split: { mapper: (n) => Number(n) * 2 } })`, the parameters of the function is identical to how it would be with [`Array#map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map#Syntax) (and it will be passed into map in the same way) which is `(e: string, i: number, a: string[])`.

---

The [`setupDay`](https://github.com/izexi/aoc-ts-template/blob/master/src/util/index.ts#L51-L57) function was used to generate boilerplates for all the days, if you don't wish to have directories pre-setup for future days you can simply delete them and make use of this function when you want to setup a specific day.