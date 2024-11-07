# 程序设计的基本元素


## 经典实例

### 1.1.7 采用牛顿法求平方根

牛顿的方法：如果 x 的平方根的值有了一个猜测 y，只要求出 y 和 x/y 的平均值（它更接近实际的平方根值）。
可以用这种方法求 2 的平方根，假定初始值是 1。


```scheme
(define (sqrt-iter guess x)
    (if (good-enough? guess x)
        guess
        (sqrt-iter (improve guess x) x)))

(define (improve guess x)
    (average guess (/ x guess))) ; 牛顿法

(define (average x y)
    (/ (+ x y) 2))
```

怎么算足够好？
可以让，猜测值的平方与 x 小于某个误差值。
```scheme
(define (square x)
    (* x x))

(define (good-enough? guess x)
    (< (abs (- (square guess) x)) 0.001))
```

最后需要一种方式启动整个工作。

```scheme
(define (sqrt x)
    (sqrt-iter 1 x)) ; initiate
```

## 练习

### 1.1

```scheme
10
(+ 5 3 4)
(- 9 1)
(/ 6 2)
(+ (* 2 4) (- 4 6))
(define a 3)
(define b (+ a 1))
(+ a b (* a b))
(= a b)
(if (and (> b a) (< b (* a b)))
    b
    a)

(cond ((= a 4) 6)
      ((= b 4) (+ 6 7 a))
      (else 25))
    
(+ 2 (if (> b a) b a))

(* (cond ((> a b) a)
         ((< a b) b)
         (else -1))
   (+ a 1))
```

### 1.2

```scheme
(/ (+ 5 4
      (- 2 
         (- 3 
            (+ 6 (/ 4 5))))) 
   (* 3 (- 6 2) (- 2 7)))
```

### 1.3

```scheme
(define (min-value a b c)
    (cond ((and (< a b) (< a c)) a)
          ((and (< b a) (< b c)) b)
          ((and (< c a) (< c b)) c))
)

(define (two-bigger-sum a b c)
    (+ a b c 
        (- 0 (min-value a b c))
    )
)

(two-bigger-sum -1 8 -2)
```

### 1.4

```scheme
(define (a-plus-abs-b a b)
    ((if (> b 0) + -) a b)
)

(a-plus-abs-b 3 -9)
```

### 1.5

如果是正则序求值（即先完全展开，而后规约），那么会因为展开而死循环；如果是应用序求值，会是 0。我使用的scheme 实现是正则序，于是死循环了。

```scheme
(define (p)
    (p))

(define (test x)
    (if (= x 0) 0 (p)))

(test 0)
(define y 0)
(the y (and (>= y 0)))
```

`the` 在 Scheme 的方言 Racket 里不是标识符...

### 1.6

```scheme
(define (new-if predicate then-clause else-clause)
    (cond (predicate then-clause)
          (else else-clause)))
```

`new-if` 会对 `then-clause` `else-clause` 求值，不论该走哪个分支。显然，死循环了。

### 1.7

```scheme
;(< (/ (abs (- (improve guess x) guess)) guess) 0.001))
```

试了，效果不太理想。

### 1.8

```scheme
(define (cbrt x)
  (define (cube x)
    (* x x x))
  (define (improve guess x)
    (/ (+ (/ x (* guess guess)) (* 2 guess)) 3))
  (define (good-enough? guess x)
    (< (abs (- (cube guess) x)) 0.001))
  (define (cbrt-iter guess x)
    (if (good-enough? guess x)
        guess
        (cbrt-iter (improve guess x) x)))
  (cbrt-iter 1 x))

; (display (exact->inexact (cbrt (* 5 5 5))))
```

就是效率不太行，每加一个值，时间呈指数上升。

