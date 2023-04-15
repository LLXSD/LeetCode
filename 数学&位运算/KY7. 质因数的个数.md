## 题目描述
求正整数N(N>1)的质因数的个数。 相同的质因数需要重复计算。如120=2*2*2*3*5，共有5个质因数。



## 代码
```python

prime = [True] * int(1000000000 ** 0.5 +1)  
# 取sqrt是因为其中只可能有一个质因数大于其平方根，两个的话乘积会大于N
prime[0], prime[1] = False, False
for i in range(2, len(prime)):
    if prime[i]:
        j = 2
        while (i * j) < len(prime):
            prime[int(i * j)] = False
            j += 1
p = []
for i in range(len(prime)):
    if prime[i]:
        p.append(i)
# 用每个素数除n，若可以除尽，则返回len(r)，若不可以除尽，则说明有一个质因数大于平方根，此时需要len(r)+1
def primedivision(n):
    r = []
    index = 0
    while n != 1:
        if n % p[index] == 0:
            r.append(p[index])
            n = n / p[index]
        else:
            index += 1
            if index == len(p):
                return len(r) + 1
    return len(r)

while 1:
    try:
        N = int(input().strip())
        print(primedivision(N))
    except:
        break

```
