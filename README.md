# Genetic_rescue_simulations
Code for simulations of genetic rescue under various conditions, for a future paper. The steps for these simulations are as follows:

1) Generate initial burn-in of non-neutral mutations only, and output the resultant tree-sequence recording. Models are based on four different mammalian genomes ("Species" = Canine, Human, Mouse and Wallaby); three different (ancestral) population sizes ("AncestralSize" = 2000; 5000; 10000); and two different sets of non-neutral mutations ("MutModel" = deleterious only: "NoAdap", and deleterious + adaptive: "Shared"). These are output as:
  "{Species}_K{AncestralSize}_{MutModel}_burnin.trees"
2) Import each of these tree-sequence recordings into pyslim/msprime, and use recapitation to fill out the coalescent tree (see Kelleher et al. 20XX) and distribute neutral mutations according to a defined mutation rate and recombination map per species. This is repeated for each of the tree-sequence recordings. These are output as:
  "{Species}_K{AncestralSize}_{MutModel}_recapped.trees"
3) Each of these recapitated and filled tree-sequence recordings is used as the input for further SLiMulations, starting from generation 1000 (when the initial burn-in trees were exported). From this starting point, the ancestral population is divided into two populations (a "source" and "target" for genetic rescue) and allowed to diverge for a period of time (until the specific Fst threshold is hit). At this stage, a single migration event from the target to the source is enacted (as a one-off translocation) and then the simulation continues for ~20 generations, with relevant statistics of the target population calculated and exported. These are saved as:
  "{Species}_K{AncestralSize}_{MutModel}.csv"
4) Statistical inferences of these outputs are then evaluated using R. 
