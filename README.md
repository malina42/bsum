# bsum
bsum utility to run the 4 blake2 variations and blake3 (default) faster than current solutions.

note is inside the tarball. This is for linux only. and is a demo version. it has limitations, but if/as people use it,
I can take the time to sort it out.

Mali

Addendum:

to test speeds vs. b2sum (coreutils?) or b3sum (blake3), testing traversal vs. single large files:

examples: (adjust according to available memory)

truncate -s 2G /dev/shm/2G 
or for a non sparse file:
dd if=/dev/urandom bs=2M count=1024 of=/dev/shm/2G.rnd

time ./bsum /dev/shm/2G
time ./bsum /dev/shm/2G.rnd
vs. time b2sum b3sum...

time b{,2,3}sum /usr/bin/**/*(D.) (zsh)
/usr/bin/* should be fine too. 

for smaller files like /usr/share/man can also be useful

NOTE. I did not put setting threads yet , ignore the help. This means 
it will NOT do well on HDD, i.e. spinning media. neither will b3sum, 
*unless* one sets --num-threads=1 or --rayon-threads=1 or whatever they use.

Once/if I get feedback on that, (or I bother), I can add it. it's rather trivial.

finally. I just added some code from C/asm to test speedup on single, large files (i.e. b3.MT in the C path),

and the function probably requires caller to free, so there is some leaks. This should absoutely have been done before
I uploaded. so despite this not a timed demo, it should have been. don't use for extended/practical use then.

Again, if feedback suggests needs, I will find time to polish it to a RC.
