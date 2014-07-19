libcperm - Create secure permutations from cryptologic ciphers.

Description
===========
libcperm is a library for creating permutations from cryptologic block ciphers. A block cipher is
by definition a permutation over the set of possible inputs. Most block ciphers have limited number
of block sizes, which are typically powers of two. Often times, permutations with much smaller ranges
are needed, limiting the effictivness of the using a block cipher directly.

libcperm creates a pseudo-random permutation over an arbitrary finite domain.
Permutations are created using either the Perfix Cipher or the Cycle-walking Cipher algorithms described
in the paper "Ciphers with Arbitrary Finite Domains" by John Black and Phillip Rogaway. As shown in the
paper, the permutations generated by libcperm are no less secure as the cipher used to generate them.

Advantages of libcperm
----------------------
- Permutations are as secure as the cipher used to generate them (RC4).
- Simple, easy to use API.
- Can handle any size domain up to 2^32.
- Each value will only be seen once unlike a random number generator which may generate the same value twice.
- Small, compact, pure-C library that will compile anywhere.
- Permutations can be seeded, allowing repeated generation of the same permutation.

Example
=======
Below is a simple C program that creates a permutation with 100 objects and prints out the each of the
objects in the permuted order.

#include <stdio.h>
#include "perm.h"

#define SIZE 100

int main() {
struct perm_t* perm = perm_create(SIZE, PERM_MODE_PREFIX, PERM_CIPHER_RC5, key, 32);
uint32_t value, count = 0;

while(PERM_END != perm_next(perm, &value)) {
printf("perm[%u] = %u\n", count, value);
count++;
}

perm_destroy(perm);

return 0;
}
