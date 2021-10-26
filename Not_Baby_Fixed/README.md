# Challenge Info:

### Challenge Name: Not_Baby_Fixed

### Challenge Author: QuickMaffs

### Challenge Description: Hmm.... What is this? (Note: Not_Baby has a different solution than intended)

### Files Provided: out.txt | nums.txt | script.py

## Solution: 

#### So after looking through the files we have provided we can see that script.py reads in flag.txt and nums.txt and then generates out.txt. Out.txt prints out an n value, e value, and ct value so we know this is RSA. A lot of other solutions that I found for this challenge used factor calculators for a long time or factorDB now that someone uploaded the factors into it. However that's cringe and we like to do the intended solution around here 😎. (Note: I did talk to the challenge author and this method is the intended sol. 

#### So first we have to somehow factor n into prime factors so that then we can do the regular RSA decryption on this. However, n is supposed to be too large to factor so we must use other methods. We do know however from script.py that the way n is generated makes: n = a^3 + b^3 - 34c^3 and we know all the values of a b and c from nums.txt. Btw the reason this challenge had to be "fixed" is that the original Not_Baby accidentally didn't provide nums.txt so it was "supposedly" impossible but people like running factor calculators for 2 hours 🤦‍♂️. Anyways, knowing a, b, and c we can try to break up this equation/polynomial or whatever you want to call it to make factoring n more realistic. So we can use any big factorization calculator like alpertron or factorDB to start factoring a, b, and c (I used factorDB). Eventually you'll find that a and c have a large, prime common factor and that b and c also have a large, prime common factor. We can then rewrite a, b, and c using these two large factors we found, lets call them x and y. a = 15x^2, b = 7y^2, c = 3xy where x = 321329349024937022728435772726127082487 and y = 302518462040600437690188095770599287567. Knowing that n = a^3 + b^3 - 34c^3, we can know plug-in the values we have calculated and make a new two-variable equation which looks like: 3375x^6 + 343y^6 - 918x^3y^3. Now we have a two-vairable equation/polynomial so we can try to factor it out now. You can use something like sage for this but I was lazy and found this website that factored it for me: https://quickmath.com/webMathematica3/quickmath/algebra/factor/basic.jsp. The two resulting factors we get are: (15x^2 + 3xy + 7y^2)(225x^4 - 45x^3y - 96x^2y^2 - 21xy^3 + 49y^4). Now we have successfully split n into two smaller factors, yay. Rather than mutliplying out those polynomials by hand we can begin to write a script.

``` 
x = 321329349024937022728435772726127082487
y = 302518462040600437690188095770599287567

f = 15*x**2 + 3*x*y + 7*y**2
g = 225*x**4 - 45*x**3*y - 96*x**2*y**2 - 21*x*y**3 + 49*y**4

print(f)
print(g)
```

#### Now that we have two smaller numbers that we know are the products of n we can begin to prime factorize them, which will be much faster and more efficient than an incredibly large n value. Using factorDB I was able to get a long list of only prime factors that all multiply to get n. Time to write our script and decrypt this RSA now that the hard part is over. I will post my full script in this folder but I will give a brief explanation of it here. After calculating f and g I create an array of all the prime factors and call it nums. I then calculate phi by multiplying all of the factors - 1 by each other. (Note: Will explain why this won't always work). Then I just calculate d value with standard RSA, so e^-1 mod phi. I think this can also be achieved with the pycrypto inverse function with inverse (e, phi). Then find the message, again with standard RSA protocol, so our cyphertext^d mod n. Then I just run the long_to_bytes function to convert the message from numbers to readable text and voila, we have our flag. Quickly to explain my previous note the phi function isn't calculated simply by getting the product of every prime factor - 1 it is actually calculated wtih phi(p^e) = p^(e-1) * (p-1) p being the prime and e being the exponent. Sometimes though you won't get any primes with an exponent larger than 1 so the beginning part of the phi function which is p^(e-1) will just end up equalling 1, so all you have to really solve for is (p-1). In this problem there was a prime factor of 2^4, but I was too lazy to write an actually good script so when I solved the phi function by hand with 2^4 I found that it would end up multiplying phi by 8, so in my nums array I just lazily added a factor of 9 so that when phi was multiplied by (num - 1) the 9 would multiply phi by 8. If you want a much better way of doing this I'd recommend checking out https://hackmd.io/Dy_A6F9fQTikEtHMEKcZ1Q?view this persons write-up has a much better and more dynamic way to calculate phi that will work with multiple factors with exponents > 1. Also funny enough this was the only write-up I could find that solved the challenge with the intended solutionso kudos to them. However, as a beginner reading that write-up I thought it could use a little more explanationto help people trying to learn which I tried to achieve in this write-up. Anyways I'm done blabbering now here's the flag that is printed when I run my solve.py script.

### Flag: flag{plz_n0_guess_sum_of_a_b_c_d1vides_n}
