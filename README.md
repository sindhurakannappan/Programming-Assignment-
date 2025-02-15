> makeCacheMatrix <- function(x = matrix()) {
+     inv <- NULL
+     
+     # Function to set the matrix
+     set <- function(y) {
+         x <<- y
+         inv <<- NULL  # Reset the inverse when the matrix is set
+     }
+     
+     # Function to get the matrix
+     get <- function() x
+     
+     # Function to set the inverse of the matrix
+     setInverse <- function(inverse) inv <<- inverse
+     
+     # Function to get the inverse of the matrix
+     getInverse <- function() inv
+     
+     # Return a list of the functions
+     list(set = set, get = get, setInverse = setInverse, getInverse = getInverse)
+ }
> 
> cacheSolve <- function(x, ...) {
+     # Get the cached inverse if it exists
+     inv <- x$getInverse()
+     
+     # If the inverse is already cached, return it
+     if (!is.null(inv)) {
+         message("getting cached data")
+         return(inv)
+     }
+     
+     # Otherwise, calculate the inverse
+     mat <- x$get()
+     inv <- solve(mat, ...)  # Compute the inverse
+     x$setInverse(inv)       # Cache the inverse
+     
+     inv  # Return the inverse
+ }
> 
> # Create a special matrix object
> specialMatrix <- makeCacheMatrix(matrix(c(1, 2, 3, 4), 2, 2))
> 
> # Compute and cache the inverse
> inverseMatrix <- cacheSolve(specialMatrix)
> 
> # Retrieve the cached inverse (no recomputation)
> cachedInverse <- cacheSolve(specialMatrix)
getting cached data
> 
