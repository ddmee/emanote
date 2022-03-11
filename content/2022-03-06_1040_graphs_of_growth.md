# Graphs of the growths

The most common orders of growth we write down:

```
O(1) = constant time is independent of the input
O(log n) = logarithmic growth
O(n) = linear growth
O(n log n) = log-linear growth
O(n ** c) = polynominal (e.g. x cubed) (where c is some constant)
O(c ** n) = exponential to the size of the input
O(n!) = factorial time
```

Constant growth doesn't grow at all as the input grows. Logarithmic grows slowly compared to the input.

![[constant_v_logarithmic.png]]

Linear grows a lot quicker than logarithmic growth. See [[2022-03-06_1037_logarithms]]

![[logarithmic_v_linear.png]]

Linear grows slower than log-linear growth.

![[linear_v_log_linear.png]]

Log-linear growths a lot slower than quadratic. Log-linear is the fastest time bound we can currently achieve for [[sorting a list|2022-03-08_1816_sorting-a-list]] of elements, e.g. [[2022-03-08_2109_merge-sort]]. In practice it's often the case that quadratic complexity is too slow for use. Often quadratic is the bound when we have nested loops. For example see [[2022-03-08_1851_bubble-sort]]

![[log_linear_v_quadratic.png]]

Quadratic verus exponential, it's hard to even see the quadratic growth because exponential is growing so quickly. You would need to plot the graph on logarithmic (non-linear) scale.

![[quadratic_v_exponential.png]]

Exponential algorithims are just impractical. Far too large. However, there are problems that we care about that in principle can only be solved with exponential algorithims. (We need some tricks to tackle these.) [[2022-03-06_1434_np_hard|See NP Complete, NP Hard Problems]]

#complexity
#growth
#algorithms
#asymptotic
#bigO
#orderN
#omicron
#donaldknuth
#logarithmic

