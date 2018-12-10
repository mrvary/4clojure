# Solutions for 4clojure problems

I liked how [SegFaultAX listed his answers](https://gist.github.com/SegFaultAX/3607101) to the 4clojure
exercises, so I used it as a template, swapped his solutins for mine and added problem descriptions where I saw fit.
There are cases where his answers seem more idiosyncratic and concise (which comes down to a better knowledge of the
standard library and less loop/recur extravaganza), so I kept them as points of comparison.

[Problem 1: Nothing but the Truth [Elementary]](http://www.4clojure.com/problem/1)

```clojure
true
```

[Problem 2: Simple Math [Elementary]](http://www.4clojure.com/problem/2)

```clojure
4
```

[Problem 3: Intro to Strings [Elementary]](http://www.4clojure.com/problem/3)

```clojure
"HELLO WORLD"
```

[Problem 4: Intro to Lists [Elementary]](http://www.4clojure.com/problem/4)

```clojure
:a :b :c
```

[Problem 5: Lists: conj [Elementary]](http://www.4clojure.com/problem/5)

```clojure
'(1 2 3 4)
```

[Problem 6: Intro to Vectors [Elementary]](http://www.4clojure.com/problem/6)

```clojure
:a :b :c
```

[Problem 7: Vectors: conj [Elementary]](http://www.4clojure.com/problem/7)

```clojure
[1 2 3 4]
```

[Problem 8: Intro to Sets [Elementary]](http://www.4clojure.com/problem/8)

```clojure
#{:a :b :c :d}
```

[Problem 9: Sets: conj [Elementary]](http://www.4clojure.com/problem/9)

```clojure
2
```

[Problem 10: Intro to Maps [Elementary]](http://www.4clojure.com/problem/10)

```clojure
20
```

[Problem 11: Maps: conj [Elementary]](http://www.4clojure.com/problem/11)

```clojure
[:b 2]
```

[Problem 12: Intro to Sequences [Elementary]](http://www.4clojure.com/problem/12)

```clojure
3
```

[Problem 13: Sequences: rest [Elementary]](http://www.4clojure.com/problem/13)

```clojure
[20 30 40]
```

[Problem 14: Intro to Functions [Elementary]](http://www.4clojure.com/problem/14)

```clojure
8
```

[Problem 15: Double Down [Elementary]](http://www.4clojure.com/problem/15)
Write a function which doubles a number.

```clojure
(fn [x] (* x 2))
```

[Problem 16: Hello World [Elementary]](http://www.4clojure.com/problem/16)
Write a function which returns a personalized greeting.

```clojure
(fn [name] (str "Hello, " name "!"))
```

[Problem 17: Sequences: map [Elementary]](http://www.4clojure.com/problem/17)

```clojure
'(6 7 8)
```

[Problem 18: Sequences: filter [Elementary]](http://www.4clojure.com/problem/18)

```clojure
'(6 7)
```

[Problem 19: Last Element [Easy]](http://www.4clojure.com/problem/19)

Write a function which returns the last element in a sequence.

```clojure
(fn _last [x]
  (if (empty? (rest x))
    (first x)
    (_last (rest x))))

;; SegFaultAX:
#(nth % (dec (count %)))
```

[Problem 20: Penultimate Element [Easy]](http://www.4clojure.com/problem/20)

Write a function which returns the second to last element from a sequence.

```clojure
(fn second-to-last [x]
  (if (= 1 (count (rest x)))
    (first x)
    (second-to-last (rest x))))

;; SegFaultAX: 
(comp second reverse)
```

[Problem 21: Nth Element [Easy]](http://www.4clojure.com/problem/21)

Write a function which returns the Nth element from a sequence.

```clojure
(fn number-at-index [coll index]
  (if (= index 0)
    (first coll)
    (number-at-index (rest coll) (- index 1))))

;; SegFaultAX:
(fn [coll n] (first (drop n coll)))
```

[Problem 22: Count a Sequence [Easy]](http://www.4clojure.com/problem/22)

Write a function which returns the total number of elements in a sequence.

```clojure
(fn count-elements [coll]
  (if (empty? (rest coll))
    1
    (+ 1 (count-elements (rest coll)))))

;; SegFaultAX:
#(reduce + (map (constantly 1) %))
```

[Problem 23: Reverse a Sequence [Easy]](http://www.4clojure.com/problem/23)

Write a function which reverses a sequence.

```clojure
(fn my-reverse [coll]
  (loop [x coll
         result '()]
    (if (empty? x)
      result
      (recur (rest x) (cons (first x) result)))))

;; SegFaultAX
#(reduce conj () %)
```

[Problem 24: Sum It All Up [Easy]](http://www.4clojure.com/problem/24)

Write a function which returns the sum of a sequence of numbers.

```clojure
(fn [coll] (reduce + coll))
```

[Problem 25: Find the odd numbers [Easy]](http://www.4clojure.com/problem/25)

Write a function which returns only the odd numbers from a sequence.

```clojure
(fn [coll] (filter odd? coll))
```

[Problem 26: Fibonacci Sequence [Easy]](http://www.4clojure.com/problem/26)

Write a function which returns the first X fibonacci numbers.

```clojure
(fn fibo-recur [length]
  (loop [result [1 1]]
    (if (= (count result) length)
      result
      (recur (conj result (+ (last (pop result)) (last result)))))))

;; SefFaultAX:
#(take % (map first (iterate (fn [[a b]] [b (+ a b)]) [1 1])))
```

[Problem 27: Palindrome Detector [Easy]](http://www.4clojure.com/problem/27)

Write a function which returns true if the given sequence is a palindrome.

```clojure
(fn [coll]
  (= (seq coll) (reverse coll)))
```

[Problem 29: Get the Caps [Easy]](http://www.4clojure.com/problem/29)

Write a function which takes a string and returns a new string containing only the capital letters.

```clojure
(fn [s] 
  (apply str (filter (set "ABCDEFGHIJKLMNOPQRSTUVWXYZ") s)))

;; SegFaultAX:
#(apply str (re-seq #"[A-Z]+" %))
```

[Problem 30: Compress a Sequence [Easy]](http://www.4clojure.com/problem/30)

Write a function which removes consecutive duplicates from a sequence.

```clojure
(fn [coll]
  (->> coll
      (partition-by identity)
      (map first)))

;; SegFaultAX
#(map first (partition-by identity %))
```

[Problem 31: Pack a Sequence [Easy]](http://www.4clojure.com/problem/31)

Write a function which packs consecutive duplicates into sub-lists.

```clojure
(partial partition-by identity)
```

[Problem 32: Duplicate a Sequence [Easy]](http://www.4clojure.com/problem/32)

Write a function which duplicates each element of a sequence.

```clojure
(fn [x] 
  (loop [items x
         result []]
    (if (empty? items)
      result
      (recur (rest items)
             (conj result (first items) (first items))))))

;; SegFaultAX
mapcat #(list % %)
```

[Problem 33: Replicate a Sequence [Easy]](http://www.4clojure.com/problem/33)

Write a function which replicates each element of a sequence a variable number of times.

```clojure
(fn [coll n]
  (loop [remaining coll
         result []]
    (if (empty? remaining)
      result
      (recur (rest remaining)
             (into result (repeat n (first remaining)))))))

;; SefFaultAX
(fn [s n] (mapcat #(repeat n %) s))
```

[Problem 34: Implement range [Easy]](http://www.4clojure.com/problem/34)

Write a function which creates a list of all integers in a given range.

```clojure
(fn [start end]
  (take-while #(< % end) (iterate inc start)))
```

[Problem 35: Local bindings [Elementary]](http://www.4clojure.com/problem/35)

```clojure
7
```

[Problem 36: Let it Be [Elementary]](http://www.4clojure.com/problem/36)

```clojure
[x 7
 y 3
 z 1]
```

[Problem 37: Regular Expressions [Elementary]](http://www.4clojure.com/problem/37)

```clojure
"ABC"
```

[Problem 38: Maximum value [Easy]](http://www.4clojure.com/problem/38)

Write a function which takes a variable number of parameters and returns the maximum value.

```clojure
(fn [& args] (last (sort args)))
```

[Problem 41: Drop Every Nth Item [Easy]](http://www.4clojure.com/problem/41)

Write a function which drops every Nth item from a sequence.

```clojure
(fn [realColl realN]
  (loop [[fst & snd :as coll] realColl
       	 n realN
       	 result []]
    (cond
      (empty? coll) result
      (= 1 n) (recur snd realN result)
      :else (recur snd
                   (dec n)
                   (conj result fst)))))

;; SegFaultAX
#(apply concat (partition-all (dec %2) %2 %))
```

[Problem 42: Factorial Fun [Easy]](http://www.4clojure.com/problem/42)

Write a function which calculates factorials.

```clojure
(fn [n]
  (loop [number n
         result 1]
    (if (<= number 1)
      result
      (recur (dec number) (* result number)))))

;; SegFaultAX
#(apply * (range 1 (inc %)))
```

[Problem 45: Intro to Iterate [Easy]](http://www.4clojure.com/problem/45)

```clojure
[1 4 7 10 13]
```

[Problem 47: Contain Yourself [Easy]](http://www.4clojure.com/problem/47)

```clojure
4
```

[Problem 48: Intro to some [Easy]](http://www.4clojure.com/problem/48)

```clojure
6
```

[Problem 51: Advanced Destructuring [Easy]](http://www.4clojure.com/problem/51)

```clojure
[1 2 3 4 5]
```

[Problem 52: Intro to Destructuring [Easy]](http://www.4clojure.com/problem/52)

```clojure
(vector c e)
```

[Problem 57: Simple Recursion [Elementary]](http://www.4clojure.com/problem/57)

```clojure
[5 4 3 2 1]
```

[Problem 64: Intro to Reduce [Elementary]](http://www.4clojure.com/problem/64)

```clojure
+
```

[Problem 66: Greatest Common Divisor [Easy]](http://www.4clojure.com/problem/66)

Given two integers, write a function which returns the greatest common divisor.

```clojure
(fn [x y]
  (loop [a x
         b y]
  	(if (= b 0)
    	a
    	(recur b (mod a b)))))

(fn gcd [a b] (if (zero? b) a (recur b (mod a b))))
```

[Problem 68: Recurring Theme [Elementary]](http://www.4clojure.com/problem/68)

```clojure
[7 6 5 4 3]
```

[Problem 71: Rearranging Code: -> [Elementary]](http://www.4clojure.com/problem/71)

```clojure
last
```

[Problem 72: Rearranging Code: ->> [Elementary]](http://www.4clojure.com/problem/72)

```clojure
reduce +
```

[Problem 76: Intro to Trampoline [Medium]](http://www.4clojure.com/problem/76)

```clojure
[1 3 5 7 9 11]

;; SegFaultAX
(range 1 12 2)
```

[Problem 81: Set Intersection [Easy]](http://www.4clojure.com/problem/81)

Write a function which returns the intersection of two sets. The intersection is the sub-set of items that each set has in common.

```clojure
(fn [a b]
  (let* [all-items (clojure.set/union a b)
         only-in-a (clojure.set/difference all-items b)
         only-in-b (clojure.set/difference all-items a)]
    (clojure.set/difference all-items only-in-a only-in-b)))

;; SegFaultAX
(fn [a b] (set (filter #(contains? b %) a)))
```

[Problem 83: A Half-Truth [Easy]](http://www.4clojure.com/problem/83)

Write a function which takes a variable number of booleans. Your function should return true if some of the parameters are true, but not all of the parameters are true. Otherwise your function should return false.

```clojure
not=
```

[Problem 88: Symmetric Difference [Easy]](http://www.4clojure.com/problem/88)

Write a function which returns the symmetric difference of two sets. The symmetric difference is the set of items belonging to one but not both of the two sets.

```clojure
(fn [setA setB]
  (let [only-in-a (clojure.set/difference setA setB)
         only-in-b (clojure.set/difference setB setA)]
  	(clojure.set/union only-in-a only-in-b)))

```

[Problem 90: Cartesian Product [Easy]](http://www.4clojure.com/problem/90)

Write a function which calculates the Cartesian product of two sets.

```clojure
(fn [setA setB]
  (set (for [a setA
        	 b setB]
    		[a b])))

;; SegFaultAX
#(set (for [a (vec %1) b (vec %2)] [a b]))
```

[Problem 100: Least Common Multiple [Easy]](http://www.4clojure.com/problem/100)

Write a function which calculates the least common multiple. Your function should accept a variable number of positive integers or ratios. 

```clojure
(fn [& args] 
  (let [gcd (fn [a b] (if (zero? b) a (recur b (mod a b))))]
    (/ (reduce * args) (reduce gcd args))))
```

[Problem 107: Simple closures [Easy]](http://www.4clojure.com/problem/107)

```clojure
(fn [n]
  (fn [x]
    (reduce * (repeat n x))))
```

[Problem 120: Sum of square of digits [Easy]](http://www.4clojure.com/problem/120)

Write a function which takes a collection of integers as an argument. Return the count of how many elements are smaller than the sum of their squared component digits. For example: 10 is larger than 1 squared plus 0 squared; whereas 15 is smaller than 1 squared plus 5 squared.

```clojure
(fn [coll]
  (letfn [(num-to-digits [n]
            (loop [num n
                   res []]
              (if (= num 0)
                (reverse res)
                (recur (quot num 10) (conj res (rem num 10))))))
          (smaller-than-squared-digits? [n]
            (let [coll (num-to-digits n)]
              (< n (reduce #(+ (* %2 %2) %1) 0 coll))))]
    (count (filter smaller-than-squared-digits? coll))))

;; SegFaultAX
(fn sum-square [coll]
  (let [digits (fn [n] (map #(- (int %) 48) (str n)))
        square #(* % %)
        sum-digits (fn [n] (reduce + (map square (digits n))))]
    (count (filter #(< % (sum-digits %)) coll))))
```

[Problem 134: A nil key [Elementary]](http://www.4clojure.com/problem/134)

Write a function which, given a key and map, returns true iff the map contains an entry with that key and its value is nil.

```clojure
(fn [k m]
  (and (contains? m k) 
       (nil? (get m k))))
```

[Problem 145: For the win [Elementary]](http://www.4clojure.com/problem/145)

```clojure
(range 1 40 4)
```

[Problem 156: Map Defaults [Elementary]](http://www.4clojure.com/problem/156)

Write a function which takes a default value and a sequence of keys and constructs a map.

```clojure
(fn [default coll] (into {} (for [i coll] [i default])))

;; SegFaultAX
#(apply hash-map (interleave %2 (repeat %1)))
```

[Problem 161: Subset and Superset [Elementary]](http://www.4clojure.com/problem/161)

```clojure
#{1 2}
```

[Problem 162: Logical falsity and truth [Elementary]](http://www.4clojure.com/problem/162)

```clojure
1
```

[Problem 173: Intro to Destructuring 2 [Easy]](http://www.4clojure.com/problem/173)

```clojure
f xs
```