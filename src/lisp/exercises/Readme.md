# Exercises from book SICP

## Navigation

* [Exercise 1](#Exercise_1)

### Exercise_1

```lisp
; Exercize 1.1
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

; Exercize 1.2
(/  (+  5 
        4 
        (-  2 
            (-  3 
                (+  6 
                    (/ 4 5))))) 
    (*  3
        (- 6 2)
        (- 2 7)))
; result -0.24666666666666667

; Exercize 1.3
(define (square x) (* x x))
(define (squareSum x y) (+ (square x) (square y)))
(define (lowIn3 x y z) (and (not (> x y)) (not (> x z))))
(define (triple a b c)
  (cond ((lowIn3 a b c) (squareSum b c))
        ((lowIn3 b a c) (squareSum a c))
        ((lowIn3 c a b) (squareSum a b))))
(triple 4 1 2)

;Exercize 1.4

```