# GraPhlAn Demo

Paper link [Compact graphical representation of phylogenetic data and metadata with GraPhlAn](https://peerj.com/articles/1029/)

**Overview pipeline**

* Download raw data 
* Install *export2graphlan* and *LEfSe*
* Prepare input data for *export2graphlan* by running LEfSe
* Prepare input data for GraPhlAn by runnning export2graphlan
* Annotate tree by running ``graphlan_annotate.py``
* Draw tree using annotated tree by running ``graphlan.py``
