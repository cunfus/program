# 过程与它们所产生的计算

### 示例


```scheme
; 线性递归过程
(define (factorial n)
  (if (= n 1)
    1
    (* n factorial (- n 1))))
```


```scheme
; 迭代计算过程，
(define (fact-iter product counter max-count)
  (if (> counter max-count)
      product
      (fact-iter (* counter product)
                 (+ counter 1)
                 max-count)))

(define (factorial n)
  (fact-iter 1 1 n))
```


```scheme
(define (fib n)
  (if (< n 2)
     n
     (+ (fib (- n 1)) (fib (- n 2)))))
```

这一节，它推演了线性递归过程（计算过程中没有任何的增长和收缩，计算的中间结果会保存在轨迹里），将这种线性递归称为迭代计算过程（线性迭代过程）。





令俺印象深刻的是，它说，在常量空间中执行迭代型计算过程，即使它是递归过程描述的，具备这种特性的递归称为尾递归。我们利用这种常规的过程调用机制表达迭代，那些各种复杂的专用迭代结构变成不过是一些语法糖衣了。






## 练习

### 1.9

```scheme


(if (= a 0)
    b
    (inc (+ (dec a) b)))


(if (= a 0)
    b
    (+ (dec a) (inc b)))

```
从语法形式上来说，这两个过程都是递归的。从计算过程上来说，前者是递归的，后者是迭代的。

### 1.10

```scheme
(define (A x y)
  (cond ((= y 0) 0)
        ((= x 0) (* 2 y))
        ((= y 1) 2)
        (else (A (- x 1)
                 (A x (- y 1))))))

(define (f n) (A 0 n)) ; 2 的 n 的 0 次方
(define (g n) (A 1 n)) ; 2 的 n 的 1 次方
(define (h n) (A 2 n)) ; 2 的 n 的 2 次方
```