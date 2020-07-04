# AIPR2019

STEP1: Building binaries

<pre>
# ./build-traverse.sh multi
# ./build-gpu.sh km-thrust
# ./build.sh aipr
</pre>

STEP2: Generating data

<pre>
# ./aipr 10000
# wc -l random_data.txt
10000 random_data.txt
</pre>

STEP3: Preparing data

<pre>
# split -l 1000 random_data.txt
# ls x*
xaa  xab  xac  xad  xae  xaf  xag  xah  xai  xaj
</pre>

<pre>
# mkdir tmp-box
# mv x* tmp-box
# ls tmp-box
xaa  xab  xac  xad  xae  xaf  xag  xah  xai  xaj
</pre>

STEP4: Reduction

<pre>
# time ./multi tmp-box/

real    0m5.679s
user    0m0.739s
sys     0m4.860s

# head -n 3 tmp-1
2019-07-02 00:00:00.027,841
2019-07-02 00:00:00.198,784
2019-07-02 00:00:00.354,912
# head -n 3 tmp-2
2019-07-02 00:00:00.027,25846
2019-07-02 00:00:00.198,52326
2019-07-02 00:00:00.354,12947

# wc -l tmp-1
9972 tmp-1
# wc -l tmp-2
9972 tmp-2
</pre>

STEP5: Clustering

<pre>
# time ./km-thrust tmp-1 tmp-2 9972

real    0m4.855s
user    0m0.253s
sys     0m4.378s

# head -n 3 clustered
2019-07-02 00:00:00.027,493,27944, cluster4,(0.0961693%)
2019-07-02 00:00:00.198,574,23719, cluster0,(0.0976735%)
2019-07-02 00:00:00.354,311,48552, cluster2,(0.0999799%)
</pre>
