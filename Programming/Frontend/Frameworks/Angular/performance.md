# Performance Optimizations For Angular
- Combined notes on research done to enhance performance in all potential areas of an angular application.

- For any applications **performance** is a cause by a multitude of factors. To name a few:
  - **output bundle composition**
  - **network parameters/available resources**

# Build Optimizations

## Compression and Bundle Output Size
- After the application code is optimized and minified by the Angular compiler. The optimal code can further be reduced in size by compressing the output files. 

  ### Compression Algorithms
  - Gzip & Brotli are the two popular & widely supported compression algorithms which we can employ to achieve better output size.
  - 