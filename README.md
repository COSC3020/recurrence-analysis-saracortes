# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```



Recurrence relation:
T(n) = 1, n ≤ 1 
$$ 3T(n/3) + n^5 $$

This recurrence relation can be solved thanks to the following:
$$ T(n) = 3T(n/3) + n^5 $$
$$ T(n) = 3(3T(n/9) + (n/3)^5) + n^5 $$
$$ T(n) = 9T(n/9) + 3(n/3)^5 + n^5 $$
$$ T(n) = 9(3T(n/27) + (n/9)^5) + 3(n/3)^5 + n^5 $$
$$ T(n) = 27T(n/27) + 9(n/9)^5 + 3(n/3)^5 + n^5 $$
which can be generalized to:
$$ T(n) = 3^k T(n/3^k) + \sum_{i=0}^{k-1} 3^i (n/3^i)^5 $$
$$ T(n) = 3^k T(n/3^k) + n^5 \sum_{i=0}^{k-1} \frac{3^i}{3^{5i}} $$
$$ T(n) = 3^k T(n/3^k) + n^5 \sum_{i=0}^{k-1} 3^{i(1-5)} $$
$$ T(n) = 3^k T(n/3^k) + n^5 \sum_{i=0}^{k-1} 3^{-4i} $$
$$ S = \sum_{i=0}^{k-1} 3^{-4i} $$
$$ S = \frac{1 - (3^{-4})^k}{1 - 3^{-4}} $$
$$ S = \frac{1 - 3^{-4k}}{1 - 3^{-4}} $$
$$ T(n) = 3^k T(n/3^k) + n^5 \cdot \frac{1 - 3^{-4k}}{1 - 3^{-4}} $$
with an asymptotic analysis we can say that:
# $$ T(n) = \mathcal{O}(n^5) $$


Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.
