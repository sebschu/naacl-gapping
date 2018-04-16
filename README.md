# Code and Data for Schuster et al. (2018)

This repository contains the data, models and system output for replicating the results from the following NAACL paper.

> Sebastian Schuster, Joakim Nivre, and Christopher D. Manning. 2018. _Sentences with Gapping: Parsing and Reconstructing Elided Predicates_. In _Proceedings of the 16th Annual Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies (NAACL 2018)_.


## Data

The repository contains the manually annotated gapping constructions (corresponding to section 4.1 and 4.4), the parser outputs (corresponding to sections 4.2 and 4.4), and the post-processed dependency graphs (corresponding to section 4.3).

Note that this directory only contains the additional data (what we refer to as the GAPPING dataset in the paper) from the WSJ, the Brown Corpus, the GENIA treebank, and the linguistic literature. The latest version of the EWT can be downloaded from 

  https://github.com/UniversalDependencies/UD_English

The directory structure is as follows.

- data: manually annotated data
	- enhanced: gold standard enhanced graphs
	- orphan-basic: gold standard dependency trees annotated according to UD v2 guidelines
	- composite-basic: gold standard dependency trees annotated with composite relations
	- constituency: Constituency trees annotated according to PTB guidelines
- parser-output: outputs of dependency and constituency parser
	- orphan-basic: predicted dependency trees annotated with UD v2 relations
  - composite-basic: predicted dependency trees annotated with composite-relations
  - kummerfeld-klein: predicted constituency trees as output by the parser of Kummerfeld and Klein (2017).

- enhanced-graphs: post-processed dependency graphs
	- oracle: dependency graphs obtained from gold standard dependency trees
		- orphan: graphs obtained by applying the orphan procedure (section 3.2)
		- composite: graphs obtained by applying the composite procedure (section 3.1)
	- end-to-end: dependency graphs obtained from predicted dependency trees
		- orphan: graphs obtained by applying the orphan procedure (section 3.2)
		- composite: graphs obtained by applying the composite procedure (section 3.1)
