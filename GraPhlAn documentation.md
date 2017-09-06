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

1) Download **python**
2) Install **Biom-format** from anaconda cloud
3) Install **panda** from anaconda cloud
4) Install **Scipy** from Anaconda
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
HERE is what the LEfSe output file looks like:

```
Bacteria.Actinobacteria.Actinobacteria.Actinomycetales.Micromonosporaceae.Actinocatenispora     0.932620780672                  -
Bacteria.Firmicutes.Bacilli.Bacillales.Planococcaceae.Paenisporosarcina 0.932620780672                  -
Bacteria.Actinobacteria.Actinobacteria.Coriobacteriales.Coriobacteriaceae	4.1742722203                    -
Bacteria.Firmicutes.Bacilli.Bacillales.Bacillaceae.Exiguobacterium	3.14961753202                   -
Bacteria.Firmicutes.Clostridia.Clostridiales.Eubacteriaceae     3.01763255894                   -
Bacteria.Firmicutes.Bacilli.Bacillales.Bacillaceae.Ureibacillus 0.932620780672                  -
Bacteria.Actinobacteria.Actinobacteria.Actinomycetales.Micromonosporaceae	1.93262078067                   -
Bacteria.Proteobacteria.Alphaproteobacteria.Rhizobiales.Brucellaceae.Ochrobactrum	0.932620780672                  -
Bacteria.Firmicutes.Bacilli.Lactobacillales.Lactobacillaceae.Paralactobacillus  0.932620780672                  -
Bacteria.Proteobacteria.Gammaproteobacteria.Cardiobacteriales.Cardiobacteriaceae.Suttonella     0.932620780672                  -
Bacteria.Proteobacteria.Betaproteobacteria.Burkholderiales.Comamonadaceae.Curvibacter   0.932620780672                  -
Bacteria.Firmicutes.Clostridia.Clostridiales.Lachnospiraceae.Anaerostipes	2.51843157654   Low_O2  4.27481432877   0.00160691102896
Bacteria.Actinobacteria.Actinobacteria.Actinomycetales.Micrococcaceae.Arthrobacter	2.10647315409                   -
Bacteria.Proteobacteria.Betaproteobacteria.Neisseriales.Neisseriaceae.Kingella  3.68124168207                   -
Bacteria.Bacteroidetes.Flavobacteria.Flavobacteriales.Flavobacteriaceae.Elizabethkingia 1.50755996482                   -
Bacteria.Bacteria_incertae_sedis.Ktedonobacteria.Ktedonobacterales.Ktedonobacteraceae   0.932620780672                  -

```

Now copy files from current directory to export2graphlan working directory (where I installed export2graphan)

```
cp hmp_aerobiosis_small.txt hmp_aerobiosis_small.res /lustre/medusa/fliu21/circular_phylogenetic_tree/export2graphan_demo/
```

### Run export2graphlan

```
cd /lustre/medusa/fliu21/circular_phylogenetic_tree/export2graphan_demo
```
You will see files two hmp file inside of the directory

```
python export2graphlan.py -i hmp_aerobiosis_small.txt -o hmp_aerobiosis_small.res -t hmp_tree.txt -a hmp_annot.txt --title "HMP Aerobiosis" --annotations 2,3 --external_annotations 4,5,6 --fname_row 0 --skip_rows 1,2 --ftop 200
```
Now the ``hmp_tree.txt`` and ``hmp_annot.txt`` are generated. AND these two files are ready for doing really GraPhlAn analysis

### Finally, Let's run GraPhlAn analysis

```
graphlan_annotate.py hmp_tree.txt  hmp_annot_tree.txt --annot hmp_annot.txt

```
The ``graphlan_annotate.py`` function will generate tree file with annotation information.

Now, let's plot the tree!!!

```
graphlan.py hmp_annot_tree.txt  hmp_tree.png --dpi 300 --size 14

```
WOW, feel so excited to look at the tree!!!

WELL, png image file need to be visualize on my local computer. Let me transfer it from Beacon server to my computer

```
scp -r -P 22 fliu21@duo.acf.tennessee.edu:/lustre/medusa/fliu21/circular_phylogenetic_tree/export2graphan_demo/hmp_tree.png /Users/fangliu/Desktop/

```







