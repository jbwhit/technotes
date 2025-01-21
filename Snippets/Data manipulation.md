Matrix Creation

import numpy as np

# Create matrices
A = np.array([[1, 2], [3, 4]])    # 2x2 matrix
B = np.ones((2, 2))               # Matrix of ones
C = np.zeros((3, 3))              # Matrix of zeros
D = np.eye(3)                     # Identity matrix
E = np.random.rand(2, 2)          # Random matrix

Matrix Properties

# Matrix shape and size
shape = A.shape                   # (rows, columns)
size = A.size                     # Total number of elements

# Matrix transpose
A_T = A.T                         # Transpose of A

# Determinant
det = np.linalg.det(A)

# Rank
rank = np.linalg.matrix_rank(A)

# Trace
trace = np.trace(A)               # Sum of diagonal elements

# Inverse
A_inv = np.linalg.inv(A)          # Only if A is square and invertible

Matrix Operations

# Element-wise operations
C = A + B                         # Addition
D = A - B                         # Subtraction
E = A * B                         # Element-wise multiplication
F = A / B                         # Element-wise division

# Matrix multiplication
G = np.dot(A, B)                  # Dot product
H = A @ B                         # Preferred syntax for matrix multiplication

# Matrix power
P = np.linalg.matrix_power(A, 3)  # A^3

# Broadcasting
scaled = 2 * A                    # Scalar multiplication

Solving Equations

# Solve Ax = b
x = np.linalg.solve(A, np.array([1, 2]))  # A must be square and invertible

Special Operations

# Eigenvalues and eigenvectors
eigenvalues, eigenvectors = np.linalg.eig(A)

# Singular Value Decomposition (SVD)
U, S, V = np.linalg.svd(A)

# QR decomposition
Q, R = np.linalg.qr(A)

# Cholesky decomposition
L = np.linalg.cholesky(A)          # A must be symmetric and positive definite

Reshaping and Stacking

# Reshape matrix
A_reshaped = A.reshape((4, 1))

# Concatenate matrices
horizontal_stack = np.hstack([A, B])
vertical_stack = np.vstack([A, B])

Useful Utilities

# Sum over rows/columns
row_sum = A.sum(axis=1)            # Sum of each row
col_sum = A.sum(axis=0)            # Sum of each column

# Maximum/Minimum
row_max = A.max(axis=1)
col_min = A.min(axis=0)
