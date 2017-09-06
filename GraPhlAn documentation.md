# GraPhlAn Demo

Paper link [Compact graphical representation of phylogenetic data and metadata with GraPhlAn](https://peerj.com/articles/1029/)

**Overview pipeline**

* Download raw data 
* Install *export2graphlan* and *LEfSe*
* Prepare input data for *export2graphlan* by running LEfSe
* Prepare input data for GraPhlAn by runnning export2graphlan
* Annotate tree by running ``graphlan_annotate.py``
* Draw tree using annotated tree by running ``graphlan.py``


### Download raw data

From the left side item - Download- [Website for downloading raw data](https://bitbucket.org/CibioCM/export2graphlan/src/c168a100f37e?at=default)

### Installation of export2graphlan

1) Download python
2) Install Biom-format from anaconda cloud
3) Install panda from anaconda cloud
4) Install Scipy from Anaconda
After installation into my directory, run the below command to put this subfolder into the **system path**, so that you can use above softwares from anywhere in your system:

```
export PATH=/lustre/medusa/fliu21/anaconda2/bin:$PATH

```

### Installation of LEfSe using Anaconda

* First need to install anaconda 
    1) Download anaconda for linux from this [link](https://repo.continuum.io/archive/Anaconda3-4.4.0-MacOSX-x86_64.pkg)
    2) Install anaconda by running ``bash ~/Anaconda3-4.4.0-Linux-x86_64.sh``
* Then need to set up channel following this [link](https://bioconda.github.io/recipes/lefse/README.html)
* Using  ``conda install lefse`` to finish installation of LEfSE

### RUN LEfSE

**Input data format**

```
oxygen_availability     High_O2 Mid_O2  Low_O2  Mid_O2  Low_O2  Low_O2  High_O2$
body_site	ear            oral    gut     oral    gut     gut     nasal   vagina $
subject_id	          158721788	158721788	159146620	159005010      $
Archaea|Euryarchaeota|Methanobacteria|Methanobacteriales|Methanobacteriaceae|Me$
Bacteria        0.999994        0.99999 0.99999 0.999984        0.999988       $
Bacteria|Acidobacteria  5.0412e-05	8.65194e-05     8.39666e-05     0.00013$
Bacteria|Acidobacteria|Acidobacteria_Gp10|Gp10  2.96541e-06     5.08937e-06    $
Bacteria|Acidobacteria|Acidobacteria_Gp11|Gp11  2.96541e-06     5.08937e-06    $
Bacteria|Acidobacteria|Acidobacteria_Gp16|Gp16  2.96541e-06     5.08937e-06    $
Bacteria|Acidobacteria|Acidobacteria_Gp17|Gp17  2.96541e-06     5.08937e-06    $
Bacteria|Acidobacteria|Acidobacteria_Gp1|Gp1    2.96541e-06     5.08937e-06    $
Bacteria|Acidobacteria|Acidobacteria_Gp22|Gp22  2.96541e-06     5.08937e-06    $
Bacteria|Acidobacteria|Acidobacteria_Gp3|Gp3    2.96541e-06     5.08937e-06    $
Bacteria|Acidobacteria|Acidobacteria_Gp4|Gp4    2.96541e-06     5.08937e-06    $
Bacteria|Acidobacteria|Acidobacteria_Gp5|Gp5    2.96541e-06     5.08937e-06    $

```
Format above file to LEfSe recognized style

```
cd /lustre/medusa/fliu21/LEfSe-explore/lefse_depository/nsegata-lefse-54694b4b0d9e
lefse-format_input.py hmp_aerobiosis_small.txt hmp_aerobiosis_small.in -c 1 -s 2 -u 3 -o 1000000
```
RUN LEfSE analysis

```
python run_lefse.py hmp_aerobiosis_small.in hmp_aerobiosis_small.res
```
Now **LEfSe input data** - ``hmp_aerobiosis_small.txt``
**LEfSe input data** - ``hmp_aerobiosis_small.txt``
are ready for antomatic annotation using **export2graphlan**

### 





