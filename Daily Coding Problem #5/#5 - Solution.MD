
**Solution**

This is a really cool example of using [closures](https://en.wikipedia.org/wiki/Closure_(computer_programming)) to store data. We must look at the signature type of cons to retrieve its first and last elements. cons takes in a and b, and returns a new anonymous function, which itself takes in f, and calls f with a and b. So the input to car and cdr is that anonymous function, which is `pair`. To get a and b back, we must feed it yet another function, one that takes in two parameters and returns the first (if car) or last (if cdr) one.

    def car(pair):
        return pair(lambda a, b: a)
    
    def cdr(pair):
        return pair(lambda a, b: b)
    

Fun fact: cdr is pronounced "cudder"!