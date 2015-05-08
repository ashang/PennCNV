The joint CNV calling algorithm in the PennCNV package is designed for calling CNVs from parents-offspring trios and has improved performance over the trio calling algorithm described in previous Trio Calling tutorial section. Please see the Wang et al paper in NAR for details on the joint calling algorithm. (The current joint-calling algorithm has been re-written and been directly incorporated into the main `detect_cnv.pl` program.) Unlike the trio calling algorithm, which use posterior validation on individual-based CNV calls, the joint-calling algorithm generates CNV calls in one single step for three individuals in a family.

The joint-calling algorithm has better performance than the current family-based CNV calls, especially in resolving the correct CNV boundaries and for reducing false negative rates on very small (\<10 SNPs) CNV calls. However, it is extremely slow and may take several hours for a single trio genotyped at 550K markers. To use this new algorithm, the user can specify `--joint` argument, rather than `--trio` argument in the command line. For example:
 
```
[kaiwang@cc penncnv]$ detect_cnv.pl -joint -hmm lib/hh550.hmm -pfb lib/hh550.hg18.pfb sample1.txt sample2.txt sample3.txt -out sampleall.jointcnv
NOTICE: Reading marker coordinates and population frequency of B allele (PFB) from lib/hh550.hg18.pfb ... Done with 566108 records (178 records in chr M,XY were discarded)
NOTICE: Reading LRR and BAF values for from sample1.txt ... Done with 561288 records in 24 chromosomes (178 records are discarded due to lack of PFB information for the markers)
NOTICE: Data from chromosome X,Y will not be used in analysis
NOTICE: Median-adjusting LRR values for all markers by -0.0184
NOTICE: Reading LRR and BAF values for from sample2.txt ... Done with 561288 records in 24 chromosomes (178 records are discarded due to lack of PFB information for the markers)
NOTICE: Data from chromosome X,Y will not be used in analysis
NOTICE: Median-adjusting LRR values for all markers by 0.0233
NOTICE: Reading LRR and BAF values for from sample3.txt ... Done with 561288 records in 24 chromosomes (178 records are discarded due to lack of PFB information for the markers)
NOTICE: Data from chromosome X,Y will not be used in analysis
NOTICE: Median-adjusting LRR values for all markers by -0.0084
NOTICE: Calling CNVs in chromosome 1 with 42075 markers
NOTICE: Finished recursion cycle 1000 in Viterbi algorithm
NOTICE: Finished recursion cycle 2000 in Viterbi algorithm
NOTICE: Finished recursion cycle 3000 in Viterbi algorithm
NOTICE: Finished recursion cycle 4000 in Viterbi algorithm
NOTICE: Finished recursion cycle 5000 in Viterbi algorithm
NOTICE: Finished recursion cycle 6000 in Viterbi algorithm
```

As we can see from the command line above, unlike the `-trio` argument, the joint-calling algorithm does not require a CNV file generated by individual-based calling algorithm as input files.

The joint-calling algorithm only supports trios. For complex nuclear families, it is better to be processed with the `-trio` and `-quartet` operations described in Trio Calling section in the tutorial.