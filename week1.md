## 第一周

#### 1、Algorithm

**Problem**：[Reverse Integer](https://leetcode.com/problems/reverse-integer/)

**分析**：重复地pop x最后的一个数字push到rev变量中

```java
// pop操作
pop = x % 10
x = x / 10;
// push操作
temp = rev * 10 + pop;
rev = temp;
```

此题目的坑在于，temp = rev * 10 + pop 可能会造成溢出（上溢或下溢）。假设x是正的，则

- 如果temp = rev * 10 + pop 会溢出，即大于INTMAX，则rev >= INTAMX / 10；
- 如果rev > INTAMX / 10，则temp = rev * 10 + pop 肯定溢出；
- 如果 rev == INTMAX/10，那么当pop>7的时候，temp = rev * 10 + pop会溢出。（找出temp溢出的边界条件）

```java
class Solution {
    public int reverse(int x) {
        int rev = 0;
        while(x != 0){
            int pop = x % 10;
            x = x / 10;
            if (rev > Integer.MAX_VALUE/10 || (rev == Integer.MAX_VALUE / 10 && pop > 7)) return 0;
            if (rev < Integer.MIN_VALUE/10 || (rev == Integer.MIN_VALUE / 10 && pop < -8)) return 0;
            rev = rev * 10 + pop;
        }
        return rev;
    }
}
```

why condition is  pop >7 and pop < -8 ？

because it is dependent on the value of INTMAX and INTMIN. a 32-bit signed integer , INTMAX is 2<sup>31</sup> -1，it’s **2147483647** ; INTMIN is -2<sup>31</sup>,  it’s -**2147483648**.



#### 2、Review