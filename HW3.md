### Prob. 1
#### (a)
Type, length, attributes.
#### (b)
Four common types: Integer, Numeric, Logical, Complex
Three attributes: `names`, `dim`, `class`
#### (c)
A list could contain data of different types (recurrsive), while an atomic vector could only contain data of one type.
A matrix could only contain data of one type, while a data frame could contain data of different types in each column (frame). However, data type in a single frame should be the same.
#### (d)
Yes, by assigning 2 dimensions for the list, like below:
```R
c <- list(1L, 2, TRUE, "name")
dim(c) <- c(2,2)
```

### Prob. 2
By the code below, I extracted the residual DoF and R squared of the model:
```R
mod <- lm(mpg ~ wt, data = mtcars)

mod_summary <- summary(mod)

rs <- mod_summary$r.squared

print(paste("R-squared:", rs))

df_res <- mod_summary$df[2]

print(paste("Degrees of freedom for residuals:", df_res))
```
The output is presented below:
```R
r$> source("/Users/lyumakaze/R_works/CS_HW3/Prob2.R", encoding = "UTF-8")
[1] "R-squared: 0.752832793658264"
[1] "Degrees of freedom for residuals: 30"
```

### Prob. 3
Choosing problem (1).
Working code are shown below:
```R
tot <- 1:1000

mask <- (tot %% 3 == 0) & (tot %% 5 == 0)

sum_35 <- sum(tot[mask])

cat("The result is", sum_35, "\n")
```
The result is:
```R
r$> source("/Users/lyumakaze/R_works/CS_HW3/Prob.3.R", encoding = "UTF-8")
The result is 33165 
```

### Prob. 4
#### (a)
```R
a <- 1:25

A <- matrix(a, nrow = 5, ncol = 5)

A <- t(A)

print(A)
```
The result is:
```R
r$> source("/Users/lyumakaze/R_works/CS_HW3/Prob.4a.R", encoding = "UTF-8")
     [,1] [,2] [,3] [,4] [,5]
[1,]    1    2    3    4    5
[2,]    6    7    8    9   10
[3,]   11   12   13   14   15
[4,]   16   17   18   19   20
[5,]   21   22   23   24   25
```
#### (b)
Computing code:
```R
a <- 1:25
A <- matrix(a, nrow = 5, ncol = 5)
A <- t(A)
print(A)
trA <- sum(diag(A))
rankA <- qr(A)$rank
detA <- det(A)
sumrowA <- rowSums(A)
meancolA <- colMeans(A)
AAT <- A %*% t(A)
ATA <- t(A) %*% A
iden <- AAT == ATA # whether they are identical
```
Results:
```R
r$> trA
[1] 65

r$> rankA
[1] 2

r$> detA
[1] 0

r$> sumrowA
[1]  15  40  65  90 115

r$> meancolA
[1] 11 12 13 14 15

r$> AAT
     [,1] [,2] [,3] [,4] [,5]
[1,]   55  130  205  280  355
[2,]  130  330  530  730  930
[3,]  205  530  855 1180 1505
[4,]  280  730 1180 1630 2080
[5,]  355  930 1505 2080 2655

r$> ATA
     [,1] [,2] [,3] [,4] [,5]
[1,]  855  910  965 1020 1075
[2,]  910  970 1030 1090 1150
[3,]  965 1030 1095 1160 1225
[4,] 1020 1090 1160 1230 1300
[5,] 1075 1150 1225 1300 1375

r$> iden
      [,1]  [,2]  [,3]  [,4]  [,5]
[1,] FALSE FALSE FALSE FALSE FALSE
[2,] FALSE FALSE FALSE FALSE FALSE
[3,] FALSE FALSE FALSE FALSE FALSE
[4,] FALSE FALSE FALSE FALSE FALSE
[5,] FALSE FALSE FALSE FALSE FALSE
```
For the computation time:
```R
time_per <- system.time({
AAT_per <- matrix(0, nrow = 5, ncol = 5)
AAT_per <- A %*% t(A)
})

time_loop <- system.time({
	AAT_loop <- matrix(0, nrow = 5, ncol = 5)
	for (i in 1:5) {
		for (j in 1:5) {
			AAT_loop[i, j] <- sum(A[i, ] * AT[, j])
		}
	}
})
```
The result
```R
r$> time_per
   user  system elapsed 
      0       0       0 

r$> time_loop
   user  system elapsed 
  0.002   0.000   0.001 
```

### Prob. 5
#### (a)
```R
x <- c(a = 10, b = 20, c = 30, d = 40)
x2 <- x[2]
print(x2)
x2 <- x["b"]
print(x2)
x12 <- x[c(1, 2)]
print(x12)
str(x12)

L <- list(A = 1:3, B = c("x", "y"), C = matrix(1:4, 2))
column1C <- L[["C"]][, 1]
print(column1C)
```
Results:
```R
r$> source("/Users/lyumakaze/R_works/CS_HW3/Prob.5a.R", encoding = "UTF-8")
 b 
20 # by position
 b 
20 # by name
 a  b 
10 20 # as vector
 Named num [1:2] 10 20
 - attr(*, "names")= chr [1:2] "a" "b"# structure
[1] 1 2# 1st column of C
```
#### (b)
```R
set.seed(941)
M <- runif(16, min = 10, max = 50)
M <- matrix(M, nrow = 4, ncol = 4)
print(M)
M2row <- M[2, ]
print(M2row)
M3col <- M[, 3]
print(M3col)
M22 <- M[1:2, 1:2]
print(M22)
M1row <- matrix(M[1, ], nrow = 1)
print(M1row)
```
The result
```R
r$> source("/Users/lyumakaze/R_works/CS_HW3/Prob.5b.R", encoding = "UTF-8")
         [,1]     [,2]     [,3]     [,4]
[1,] 37.53718 26.72963 22.43047 16.23326
[2,] 34.07116 38.28096 11.11204 41.10529
[3,] 48.11755 20.86962 46.75381 35.41442
[4,] 20.50064 15.62749 47.54822 19.03909# Matrix M
[1] 34.07116 38.28096 11.11204 41.10529# 2nd row
[1] 22.43047 11.11204 46.75381 47.54822# 3rd column
         [,1]     [,2]
[1,] 37.53718 26.72963
[2,] 34.07116 38.28096# LT submatrix
         [,1]     [,2]     [,3]     [,4]
[1,] 37.53718 26.72963 22.43047 16.23326# 1st row, 1*4 matrix
```
#### (c)
```R
dat <- mtcars
dat5row <- dat[1:5, ]
print(dat5row)
cat("\n")

mpg <- dat["mpg"]
print(mpg)
cat("\n")

cyl <- dat$cyl
print(cyl)
cat("\n")

mask_mpg <- mpg > 20
dat_mpg20 <- dat[mask_mpg, ]
am <- dat$am
mask_cyl_am <- (cyl == 6) & (am == 1)
dat_keep <- dat[mask_cyl_am, c("mpg", "hp", "wt")]
print(dat_keep)
```
The results:
```R
r$> source("/Users/lyumakaze/R_works/CS_HW3/Prob.5c.R", encoding = "UTF-8")
# First 5 rows
                   mpg cyl disp  hp drat    wt  qsec vs am gear carb
Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2

# Column of mpg by []
                     mpg
Mazda RX4           21.0
Mazda RX4 Wag       21.0
Datsun 710          22.8
Hornet 4 Drive      21.4
Hornet Sportabout   18.7
Valiant             18.1
Duster 360          14.3
Merc 240D           24.4
Merc 230            22.8
Merc 280            19.2
Merc 280C           17.8
Merc 450SE          16.4
Merc 450SL          17.3
Merc 450SLC         15.2
Cadillac Fleetwood  10.4
Lincoln Continental 10.4
Chrysler Imperial   14.7
Fiat 128            32.4
Honda Civic         30.4
Toyota Corolla      33.9
Toyota Corona       21.5
Dodge Challenger    15.5
AMC Javelin         15.2
Camaro Z28          13.3
Pontiac Firebird    19.2
Fiat X1-9           27.3
Porsche 914-2       26.0
Lotus Europa        30.4
Ford Pantera L      15.8
Ferrari Dino        19.7
Maserati Bora       15.0
Volvo 142E          21.4

# Column of cyl by $
 [1] 6 6 4 6 8 6 8 4 4 6 6 8 8 8 8 8 8 4 4 4 4 8 8 8 8 4 4 4 8 6 8 4

# cyl == 6 and am == 1, 3 columns
               mpg  hp    wt
Mazda RX4     21.0 110 2.620
Mazda RX4 Wag 21.0 110 2.875
Ferrari Dino  19.7 175 2.770
```