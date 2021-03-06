METRICS FOR EVALUATING GEC OUTPUT

This package contains a scoring program for evaluating system output of the CoNLL 2014
Shared Task test set [1], and is released to accompany the following paper:

Courtney Napoles, Keisuke Sakaguchi, and Joel Tetreault
There's No Comparison: Reference-less Evaluation Metrics in Grammatical Error Correction
EMNLP 2016

Please include the following citation if you use this toolkit.

@InProceedings{napoles-sakaguchi-tetreault:2016:EMNLP2016,
  author    = {Napoles, Courtney  and  Sakaguchi, Keisuke  and  Tetreault, Joel},
  title     = {There's No Comparison: Reference-less Evaluation Metrics in Grammatical Error Correction},
  booktitle = {Proceedings of the 2016 Conference on Empirical Methods in Natural Language Processing},
  month     = {November},
  year      = {2016},
  address   = {Austin, Texas},
  publisher = {Association for Computational Linguistics},
  pages     = {2109--2115},
  url       = {https://aclweb.org/anthology/D16-1228}
}

The code for executing this evaluation program is also available from our git repository: [https://github.com/cnap/grammaticality-metrics].

==

Usage:

  python evaluate.py input-dir output-dir [-d] [--im] [--ref NUCLE|ALL|EXPFLUENCY|EXPMIN|TURKFLUENCY|TURKMIN|BN]

This scoring program was created following the Codalab competition guidelines.
System output should be included in the file input-dir/res/answer.txt and the metrics are
written to output-dir/scores.txt.

In total, it calculates 10 metrics over 7 different reference sets. More details can be
found in our paper. The default behavior on CodaLab is to return GLEU, M2, and GLEU inerpolated
with LT, using all available references.

Metrics:
  - Reference-based metrics (RBMs)
	  * GLEU [2]
  	  * I-measure [3]
	  * M2 [4]
  - Grammaticality-based metrics (GBM)
	  * LT
  - Interpolated metrics
	  * LT interpolated with each RBM

Reference sets:
  - NUCLE references [1]
  - non-expert fluency edits [5]
  - non-expert minimal edits [5]
  - expert fluency edits [5]
  - expert minimal edits [5]
  - 10 references provided by Bryant and Ng, 2015 [6]

==

Contents:

├── LanguageTool-3.1/   from [https://languagetool.org/]
├── evaluate.py         evaluation script
├── gleu.py             adapted from https://github.com/cnap/gec-ranking]
├── imeasure/           adapted from [https://github.com/mfelice/imeasure]
├── m2scorer/           adapted from [http://www.comp.nus.edu.sg/~nlp/conll14st.html]
├── metadata
├── sentence_scores.py  print sentence-level scores for metrics. cannot be run within CodaLab
└── readme.txt

The scripts for calculating GLEU, I-measure, and M2 were modified to return sentence-level
scores and so that they can be called by an external program.
At this date, Codalab does not support Java 8, so we are using the most recent version of
LanguageTool that supports Java 7 (3.1).
I-measure takes several minutes to run and therefore we have disabled it from the online CodaLab
site so that it doesn't time out, but you can run it from the original repository
[https://github.com/mfelice/imeasure] or from the git repository for this scoring suite
[https://github.com/cnap/grammaticality-metrics].

==

Requirements:

 - python 2.7
 - numpy
 - scipy
 - Java 7+

==

References

1. Ng et al. (2014) The CoNLL-2014 Shared Task on grammatical error correction
2. Napoles et al. (2015) Ground truth for grammatical error correction metrics
3. Felice and Briscoe (2015) Towards a standard evaluation method for grammatical error
   detection and correction
4. Dahlmeier and Ng (2012) Better evaluation for grammatical error correction
5. Sakaguchi et al. (2015) Reassessing the goals of grammatical error correction: Fluency
   instead of grammaticality
6. Bryant and Ng (2015) How Far are We from Fully Automatic High Quality Grammatical Error
   Correction?

==

Contact: Courtney Napoles <napoles@cs.jhu.edu>
2016-11-17
