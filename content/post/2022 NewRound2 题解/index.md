+++
slug = "2022-newround2-solution"
title = '2022 NewRound2 题解'
date = 2024-09-09T23:49:57+08:00
weight=6

categories = [
    "题解"
]


+++

- [C++](#c)
- [Rust](#rust)
  - [A](#a)
  - [B](#b)
  - [C](#c-1)
  - [F](#f)
  - [G](#g)
  - [H](#h)
  - [I](#i)
  - [L](#l)
  - [M](#m)
  - [N](#n)
  - [R](#r)

## C++

pending

## Rust

### A

```rust
fn main()
{
    loop {
        let mut s = String::new();
        std::io::stdin().read_line(&mut s);

        let mut two = s.split_whitespace().map(|s| s.parse::<i32>());
        match (two.next(), two.next()) {
            (Some(Ok(n)), Some(Ok(m))) => {
                if 2 * n > m || 4 * n < m || m % 2 != 0 {
                    println!("False!");
                } else {
                    let y = (m - 2 * n) / 2;
                    let x = n - y;
                    println!("{} {}", x, y);
                }
            },
            _ => {
                break;
            },
        }
    }
}
```

### B

```rust
fn main() {
    let mut ts = String::new();
    std::io::stdin().read_line(&mut ts);
    if let Ok(t) = ts.trim().parse::<i32>() {
        for _ in 0..t {
            let mut ns = String::new();
            std::io::stdin().read_line(&mut ns);
            if let Ok(a) = ns.trim().parse::<i32>() {
                if a == 0 || a == 1 {
                    println!("No");
                    continue;
                }
                let mut is_prime = true;
                for factor in 2..a/2+1 {
                    if a % factor == 0 {
                        is_prime = false;
                        break;
                    }
                }
                println!("{}", if is_prime { "Yes" } else { "No" });
            }
        }
    }
}
```

### C

```rust
fn dfs(v: &[i32], m: i32, sum: i32, cnt: i32) -> bool {
    if cnt == 4 {
        if sum == m {
            return true;
        } else {
            return false;
        }
    }
    let mut ret = false;
    for a in v {
        if sum + a <= m {
            ret |= dfs(v, m, sum + a, cnt + 1);
        }
        if ret {
            break;
        }
    }
    return ret;
}

fn main() {
    let mut s1 = String::new();
    std::io::stdin().read_line(&mut s1);
    let n = s1.trim().parse::<i32>().unwrap();

    let mut s2 = String::new();
    std::io::stdin().read_line(&mut s2);
    let m = s2.trim().parse::<i32>().unwrap();

    let mut s3 = String::new();
    std::io::stdin().read_line(&mut s3);
    let v: Vec<i32> = s3.trim().split_whitespace().map(|s| s.parse::<i32>().unwrap()).collect();

    if dfs(&v, m, 0, 0) {
        println!("Yes");
    } else {
        println!("No");
    }
}
```

### F

```rust
fn main() {
    let mut ts = String::new();
    std::io::stdin().read_line(&mut ts);

    let mut arr_s = String::new();
    std::io::stdin().read_line(&mut arr_s);
    let mut arr = arr_s.trim().split_whitespace().map(|s| s.parse::<i32>());
    let mut vec = Vec::new();
    while let Some(Ok(a)) = arr.next() {
        vec.push(a);
    }
    &vec.sort();

    for i in 0..vec.len() {
        if i != 0 {
            print!(" ");
        }
        print!("{}", vec[i]);
    }
    println!();
}
```

### G

```rust
fn main() {
    let mut s = String::new();
    std::io::stdin().read_line(&mut s);
    let mut si = s.trim().split_whitespace().map(|s| s.parse::<i32>().unwrap());
    let n = si.next().unwrap();
    let m = si.next().unwrap();
    let mut intervals: Vec<(i32, i32)> = Vec::new();
    for _ in 0..m {
        let mut s = String::new();
        std::io::stdin().read_line(&mut s);
        let mut si = s.trim().split_whitespace().map(|s| s.parse::<i32>().unwrap());
        intervals.push((si.next().unwrap(), si.next().unwrap()));
    }

    let mut s = String::new();
    std::io::stdin().read_line(&mut s);
    let f = s.trim().parse::<i32>().unwrap();

    let mut r = false;
    for v in intervals {
        if v.0 <= f && f <= v.1 {
            r = true;
            break;
        }
    }
    println!("{}", if r { "Yes" } else { "No" });
}
```

### H

```rust
fn gcd(a: u64, b: u64) -> u64 {
    if b == 0 {
        a
    } else {
        gcd(b, a % b)
    }
}

fn main() {
    let mut s = String::new();
    std::io::stdin().read_line(&mut s);
    let w: Vec<u64> = s.trim().split_whitespace().map(|s| s.parse::<u64>().unwrap()).collect();
    println!("{}", w[0] / gcd(w[0], w[1]) * w[1]);
}
```

### I

```rust
fn main() {
    let mut t = String::new();
    std::io::stdin().read_line(&mut t);
    let mut cnt = [0; 11];

    loop {
        let mut ns = String::new();
        let res = std::io::stdin().read_line(&mut ns);
        let mut itr = ns.trim().split_whitespace().map(|s| s.parse::<i32>().unwrap());
        let mut at_least = 0;
        while let Some(a) = itr.next() {
            cnt[a as usize] += 1;
            at_least += 1;
        }
        if at_least == 0 {
            break;
        }
    }

    for i in 1usize..11usize {
        println!("{}", cnt[i]);
    }
}
```

### L

```rust
fn main() {
    let mut s = String::new();
    std::io::stdin().read_line(&mut s);
    let mut w = s.trim().split_whitespace().map(|s| s.parse::<i32>().unwrap()).collect::<Vec<i32>>();

    let mut a: Vec<Vec<i32>> = Vec::new();
    for _ in 0..w[0] {
        let mut line = String::new();
        std::io::stdin().read_line(&mut line);
        a.push(line.trim().split_whitespace().map(|s| s.parse::<i32>().unwrap()).collect::<Vec<i32>>());
    }

    for i in 0usize..w[0] as usize {
        let mut line = String::new();
        std::io::stdin().read_line(&mut line);
        let mut it = line.trim().split_whitespace().map(|s| s.parse::<i32>().unwrap());
        if w[0] == w[2] && w[1] == w[3] {
            for j in 0usize..w[1] as usize {
                if j != 0 {
                    print!(" ");
                }
                print!("{}", a[i][j] + it.next().unwrap());
            }
            println!();
        }
    }

    if w[0] != w[2] || w[1] != w[3] {
        println!("False!");
        return;
    }
}
```

### M

```rust
fn main() {
    let mut s = String::new();
    std::io::stdin().read_line(&mut s);
    let n = s.trim().parse::<i32>().unwrap();
    let mut v = Vec::new();

    let mut avg = 0f64;
    let mut s = String::new();
    std::io::stdin().read_line(&mut s);
    let mut it = s.trim().split_whitespace().map(|s| s.parse::<i32>().unwrap());
    while let Some(a) = it.next() {
        avg += a as f64;
        v.push(a);
    }

    avg /= n as f64;
    println!("{:.2}", avg);

    let mut first_one = true;
    for a in v {
        if a as f64 >= avg {
            if first_one {
                first_one = false;
            } else {
                print!(" ");
            }
            print!("{}", a);
        }
    }
}
```

### N

```rust
fn main() {
    let mut s = String::new();
    std::io::stdin().read_line(&mut s);
    let mut s = String::new();
    std::io::stdin().read_line(&mut s);
    let mut it = s.trim().split_whitespace().map(|s| s.parse::<i32>().unwrap());
    let mut v: Vec<i32> = Vec::new();

    let mut first = true;
    while let Some(a) = it.next() {
        if first {
            first = false;
        } else {
            print!(" ");
        }
        let mut cnt: i32 = 0;
        for k in &v {
            if k < &a {
                cnt += 1;
            }
        }
        print!("{}", cnt);
        v.push(a);
    }
}
```

### R

```rust
fn main() {
    let mut s = String::new();
    std::io::stdin().read_line(&mut s);
    let mut a = s.trim().parse::<i32>().unwrap();
    if a == 0 {
        println!("0");
        return;
    }

    let mut first_in = true;
    while a != 0 {
        if first_in {
            first_in = false;
        } else {
            print!(" ");
        }

        print!("{}", a % 10);
        a /= 10;
    }
}
```
