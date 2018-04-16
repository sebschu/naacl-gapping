# Code and Data for Schuster et al. (2018)

This repository contains the data, models and system output for replicating the results from the following NAACL paper.

> Sebastian Schuster, Joakim Nivre, and Christopher D. Manning. 2018. _Sentences with Gapping: Parsing and Reconstructing Elided Predicates_. In _Proceedings of the 16th Annual Conference of the North American Chapter of the Association for Computational Linguistics: Human Language Technologies (NAACL 2018)_.


## Data

The repository contains the manually annotated gapping constructions (corresponding to section 4.1 and 4.4), the parser outputs (corresponding to sections 4.2 and 4.4), and the post-processed dependency graphs (corresponding to section 4.3).

Note that this directory only contains the additional data (what we refer to as the GAPPING dataset in the paper) from the WSJ, the Brown Corpus, the GENIA treebank, and the linguistic literature. The latest version of the EWT can be downloaded from 

  https://github.com/UniversalDependencies/UD_English

The directory structure is as follows.

- `data`: manually annotated data
	- `enhanced`: gold standard enhanced graphs
	- `orphan-basic`: gold standard dependency trees annotated according to UD v2 guidelines
	- `composite-basic`: gold standard dependency trees annotated with composite relations
	- `constituency`: Constituency trees annotated according to PTB guidelines
- `parser-output`: outputs of dependency and constituency parser
	- `orphan-basic`: predicted dependency trees annotated with UD v2 relations
  - `composite-basic`: predicted dependency trees annotated with composite-relations
  - `kummerfeld-klein`: predicted constituency trees as output by the parser of Kummerfeld and Klein (2017).

- `enhanced-graphs`: post-processed dependency graphs
	- `oracle`: dependency graphs obtained from gold standard dependency trees
		- `orphan`: graphs obtained by applying the orphan procedure (section 3.2)
		- `composite`: graphs obtained by applying the composite procedure (section 3.1)
	- `end-to-end`: dependency graphs obtained from predicted dependency trees
		- `orphan`: graphs obtained by applying the orphan procedure (section 3.2)
		- `composite`: graphs obtained by applying the composite procedure (section 3.1)

## Models

The `models` directory contains the models for the Dozat and Manning (2016) parser and the Dozat et al. (2017) tagger. We used the following version of the parser for training and parsing:

  https://github.com/tdozat/Parser-v2/commit/d5159a1c03c4ce92eb3bdb77ac1723d0bdbc052c

The parser and tagger requires the pre-trained embeddings from the [CoNLL 2017 Shared task](http://universaldependencies.org/conll17/), which can be downloaded at

  https://lindat.mff.cuni.cz/repository/xmlui/handle/11234/1-1989
  
  
## Enhancement code

The enhancement code is built on top of Stanford CoreNLP. It uses some unreleased extensions that allow one to work with UD v2 code. If you want to use the enhancer, download the following two jar files:

  * [Special version of Stanford CoreNLP](https://nlp.stanford.edu/~sebschu/files/javanlp-core-src.jar)
  * [EJML 0.23](https://sourceforge.net/projects/ejml/files/v0.23/ejml-0.23.jar/download)
  
  Use the following command to run the enhancer:
  
      java -cp javanlp-core-src.jar:ejml-0.23.jar edu.stanford.nlp.trees.ud.EnglishUDGappingEnhancer INPUT_FILE.conllu GOLD_STANDARD.conllu -embeddings embeddings.txt > OUTPUT_FILE.conllu
      
This will add the enhancements to a treebank annotated with `orphan` relations and output the graphs to `OUTPUT_FILE.conllu`. It will also compute the labeled and unlabeled precision and recall metrics by comparing the ouput to the graphs in `GOLD_STANDARD.conllu`.
  
