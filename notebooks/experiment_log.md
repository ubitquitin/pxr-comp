# DAY 1

- Chagned random split to scaffold split. Didnt seem to make much of a diff but kept anyway.
- LightGBM, Random forest and Gaussian process regression (too slow DNF) on the RDKIT descriptors. LightGBM was best marginally.
- LightGBM on RDKIT descriptors AND appended Morgan Fingerprints (now a larger, sparser feature space) - seemed to do marginally better?

- weighted training based on standard error (LightGBM): no difference, slight worsening.
- Next I took the top features of the lightgbm feature importance, found analogues (molecules with high TanimotoSimilarity) that had distinct PEC50s and looked at the feature diffs (of the top 10 features from lightGBM). The BertzCT was the main driver, and looking at the molecular structure, it seems that losely, larger, bulkier molecules are driving increased affinity to PxR..?

- Lipicity (polarity bad) seems to be important too, and there doesnt seem to be a hard MolWt cutoff.

- Structure paper: https://pmc.ncbi.nlm.nih.gov/articles/PMC2789303/

# DAY 2

- Let's look at analogues with high Tanimoto Similarity and their feature differentiators but using the RKDIT Descriptors representation rather than the Morgan Fingerprints. Let's seee how much the representation affects the feature diferentiation and molecular pairs:
    - The molecules seem less similar. The same features dominate but I wonder if that's because i didnt normalize.

- Paper on binding to PxR: https://www.pnas.org/doi/10.1073/pnas.2217804120: ![alt text](image.png)

# Day 3

- Tried different feature combinations but in the end n-estimators=3000 worked best.

# Day 4

- Create an ensembele between two separately trained models (split by pEC450 = 4.5) into a high pEC450 and low pEC450 model(s) (shouldnt thsi be emax? Ig it's the same thing...)

- Used a weighted smooth sigmoid ensemble weighting. for maximal RAE.