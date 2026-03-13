# Class06: R Functions
Joli DeLucia (A17320476)

- [Background](#background)
- [A first function](#a-first-function)
- [A second function](#a-second-function)
- [A new cool function](#a-new-cool-function)

## Background

Functions are at the heart of using R. Everything we do involves calling
and using functions (from data, input, analysis to results output).

All functions in R have at least 3 things:

1.  A **name** the thing we use to call the function.
2.  One or more input **arguments** that are comma separated
3.  The **body**, lines of code between curly brackets { } that does the
    work of the function

## A first function

Let’s write a silly function that adds some numbers:

``` r
add <- function(x) {
  x + 1
}
```

Let’s try it out

``` r
add(100)
```

    [1] 101

Will this work

``` r
add( c(100,200, 300) )
```

    [1] 101 201 301

Modify to be more useful and add more than just 1

``` r
add <- function(x, y = 1) {
  x + y
}
```

Let’s try it

``` r
add(100, 10)
```

    [1] 110

Will this work?

``` r
add(100)
```

    [1] 101

``` r
log(10, base = 10)
```

    [1] 1

> **N.B** Input arguments can be either **required** or **optional**.
> The later have a fall-back default that is specified in the function
> code with the equals sign =.

``` r
#add(100, 200, 300)
```

## A second function

All functions in R look like this

    name <- function(arg) {
      body
    }

The `sample()` function in R …

``` r
sample(1:10, 4)
```

    [1] 10  7  9  8

> Q. Return 12 numbers picked randomly from the input 1:10

``` r
sample(1:10, 12, replace = TRUE)
```

     [1] 3 3 7 3 2 5 8 3 8 2 6 2

> Q. Write the code that generates a random 12 nucleotide long DNA
> sequence?

``` r
sample( c("A", "T", "G", "C"), 12, replace = TRUE)
```

     [1] "T" "T" "C" "G" "G" "G" "G" "A" "T" "T" "A" "T"

> Q. Write a first version function called `generate_dna()` that
> generates a user specified length `n` random DNA sequence?

``` r
generate_dna <- function(n = 6) {
  sample( c("A", "T", "G", "C"), size = n, replace = TRUE)
}
```

``` r
generate_dna(15)
```

     [1] "A" "A" "G" "C" "G" "G" "T" "C" "T" "C" "C" "A" "A" "C" "T"

> Q. Modify your function to return a FASTA like sequence so rather than
> \[1\] “G” “A” “C” “G” we want “GACG”

``` r
generate_dna <- function(n = 6) {
  paste(sample( c("A", "T", "G", "C"), size = n, replace = TRUE), collapse = "")
}
```

``` r
generate_dna(15)
```

    [1] "ACTGTGGGCCGCCGC"

> Q. Give the user the option to return the FASTA format output or the
> standard multi-element vector format?

``` r
generate_dna <- function(n = 6, fasta = TRUE) {
  ans <- sample( c("A", "T", "G", "C"), size = n, replace = TRUE)
  
  if(fasta) {
    ans <- paste(ans, collapse = "")
  }
  
  return(ans)
}
```

``` r
generate_dna(15, fasta = F)
```

     [1] "C" "T" "G" "C" "C" "G" "G" "A" "G" "C" "C" "A" "T" "T" "C"

``` r
generate_dna(15, fasta = T)
```

    [1] "GCCGGTCCAGAGCCT"

``` r
generate_dna(15)
```

    [1] "AGCAGAATCTAGACA"

## A new cool function

> Q. Write a function called `generate_protein()` that generates a user
> specified length protein sequence in FASTA like format?

``` r
aa20 <- c("A","R","N","D","C","Q","E","G","H","I",
          "L","K","M","F","P","S","T","W","Y","V")
generate_protein <- function(n =6) {
  paste(sample(aa20, size = n, replace = T), collapse = "")
}
```

``` r
generate_protein()
```

    [1] "AVWLIS"

> Q. Use your new `generate_protein()` function to generate all
> sequences between length 6 and 12 amino acids in length and check if
> any of these are unique in nature (i.e found in the NR database at
> NCBI)?

``` r
generate_protein(6)
```

    [1] "FAFSDK"

``` r
generate_protein(7)
```

    [1] "TAMSYEY"

``` r
generate_protein(8)
```

    [1] "EVIENMPY"

``` r
generate_protein(9)
```

    [1] "KLTSTWNGT"

``` r
generate_protein(10)
```

    [1] "IHRAERVEDH"

``` r
generate_protein(11)
```

    [1] "MAAWKHPIQDH"

``` r
generate_protein(12)
```

    [1] "DSDAGGGNIQFV"

Or we could do a `for()` loop:

``` r
for(i in 6:12) {
  cat(">", i, "\n", sep = "")
  cat ( generate_protein(i), "\n" )
}
```

    >6
    EACQPP 
    >7
    VNFFQGG 
    >8
    QPWFDYLK 
    >9
    WGEEMLDFD 
    >10
    IYCCATQVPP 
    >11
    CDLHKRLMWWL 
    >12
    RLQTMCKNHHHQ 
