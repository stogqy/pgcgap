---
sort: 998
---

# DOC for V1.0.32

![Platform](https://img.shields.io/badge/Platform-WSL%2FLinux%2FmacOS-green) [![License](https://img.shields.io/github/license/liaochenlanruo/pgcgap)](https://github.com/liaochenlanruo/pgcgap/blob/master/LICENSE) [![GitHubversion](https://anaconda.org/bioconda/pgcgap/badges/version.svg)](https://anaconda.org/bioconda/pgcgap) ![Downloads conda](https://img.shields.io/conda/dn/bioconda/pgcgap.svg?style=flat) [![install with bioconda](https://img.shields.io/badge/install%20with-bioconda-brightgreen.svg?style=flat)](http://bioconda.github.io/recipes/pgcgap/README.html) [![生信之巅](https://pub.idqqimg.com/wpa/images/group.png "945751012")](//shang.qq.com/wpa/qunwpa?idkey=fd4637eecd73bf0a5a8caa274843a07afdf1fbbc40a86630df5d4b029749cc7b)


<p><center>
<script type="text/javascript" src="//rf.revolvermaps.com/0/0/4.js?i=0ett3z77b0x&amp;m=0&amp;h=128&amp;c=ff0000&amp;r=0" async="async"></script>
&nbsp;&nbsp;&nbsp;&nbsp;
<script type="text/javascript" src="//rf.revolvermaps.com/0/0/0.js?i=0ett3z77b0x&amp;d=3&amp;p=1&amp;b=1&amp;w=293&amp;g=2&amp;f=arial&amp;fs=13&amp;r=0&amp;c0=ff8a00&amp;c1=0006ff&amp;c2=000000&amp;ic0=0&amp;ic1=0" async="async"></script>
</center></p>
-------------

[English Readme](https://liaochenlanruo.github.io/pgcgap) \| [中文说明](https://liaochenlanruo.github.io/post/848f.html)


          ____       ____      ____     ____       _        ____    
        U|  _"\ u U /"___|u U /"___| U /"___|u U  /"\  u  U|  _"\ u 
        \| |_) |/ \| |  _ / \| | u   \| |  _ /  \/ _ \/   \| |_) |/ 
         |  __/    | |_| |   | |/__   | |_| |   / ___ \    |  __/   
         |_|        \____|    \____|   \____|  /_/   \_\   |_|      
         ||>>_      _)(|_    _// \\    _)(|_    \\    >>   ||>>_    
        (__)__)    (__)__)  (__)(__)  (__)__)  (__)  (__) (__)__)   

-------------


## Introduction
<p>PGCGAP is a pipeline for prokaryotic comparative genomics analysis. It can take the pair-end reads, ONT reads or PacBio reads as input. In addition to genome assembly, gene prediction and annotation, it can also get common comparative genomics analysis results such as phylogenetic trees of single-core proteins and core SNPs, pan-genome, whole-genome Average Nucleotide Identity (ANI), orthogroups and orthologs, COG annotations, substitutions (SNPs) and insertions/deletions (indels), and antimicrobial and virulence genes mining with only one line of commands. <strong>To follow this document, please upgrade PGCGAP to version v1.0.31 or later.</strong></p>
## Installation
<p>The software was tested successfully on Windows WSL, Linux x64 platform, and macOS. <font color=red>Because this software relies on a large number of other software, so it is recommended to install with <strong><a href="https://bioconda.github.io/index.html">Bioconda</a></strong></font>.</p>
<p><strong>Step1: Install PGCGAP</strong></p>
<pre>
$conda create -n pgcgap python=3
$conda activate pgcgap
$conda install pgcgap
</pre>

<p><strong>Notice: What should we do when the installation is slow? </strong>As more and more software is contained in CONDA and the index files become larger, the search space for the software that satisfies all the software dependencies in the environment becomes larger and larger when installing a new software, making "Solving Environment" slower and slower. Sometimes we can't even install the software through CONDA. In fact, we can do something instead of just waiting.<br/></p>
<ul>
<li>
Method 1: use mamba to deal with the slow development of "solving environment" when using CONDA.
<pre>
$conda activate pgcgap
$conda install mamba -c conda-forge
$mamba install pgcgap
</pre>
</li>

<li>
Method 2: use "environment.yaml" we provided to deal with the slow development of "solving environment" when using CONDA. Run the following commands to download the <a href="https://github.com/liaochenlanruo/pgcgap/blob/master/conda/pgcgap_latest_env.yml">latest environmental file</a> and install PGCGAP:
<pre>
# download pgcgap_latest_env.yml
$wget https://github.com/liaochenlanruo/pgcgap/blob/master/conda/pgcgap_latest_env.yml

# create a conda environment named as pgcgap and install the latest version of PGCGAP
$conda env create -f pgcgap_latest_env.yml
</pre>
</li>
</ul>

<pre>
$conda activate pgcgap
$pgcgap --setup-COGdb
$conda deactivate
</pre>
<p>Users with <a href="https://hub.docker.com/">docker container</a> installed have another choice to install PGCGAP.</p>
<pre>
$docker pull quay.io/biocontainers/pgcgap:<tag>
</pre>
<p>(see <a href="https://quay.io/repository/biocontainers/pgcgap?tab=tags">pgcgap/tags</a> for valid values for &lt;tag&gt;)</p>
## Required dependencies
<ul>
<li><a href="https://github.com/tseemann/abricate">Abricate</a></li>
<li><a href="http://www.bcgsc.ca/platform/bioinfo/software/abyss/">ABySS</a></li>
<li><a href="http://canu.readthedocs.org/">Canu</a></li>
<li><a href="http://weizhongli-lab.org/cd-hit/">CD-HIT</a></li>
<li><a href="https://www.gnu.org/software/coreutils/">Coreutils</a></li>
<li><a href="https://github.com/bbuchfink/diamond">Diamond</a></li>
<li><a href="https://github.com/ParBLiSS/FastANI">FastANI</a></li>
<li><a href="http://www.atgc-montpellier.fr/fastme/binaries.php">Fastme</a></li>
<li><a href="https://github.com/OpenGene/fastp">Fastp</a></li>
<li><a href="http://www.microbesonline.org/fasttree">FastTree</a></li>
<li><a href="https://github.com/sanger-pathogens/gubbins">Gubbins</a> &gt;=2.3.4</li>
<li><a href="https://github.com/samtools/htslib">Htslib</a></li>
<li><a href="http://www.iqtree.org/">IQ-TREE</a></li>
<li><a href="https://mafft.cbrc.jp/alignment/software/">Mafft</a></li>
<li><a href="https://github.com/marbl/Mash">Mash</a></li>
<li><a href="https://github.com/soedinglab/mmseqs2">Mmseqs2</a></li>
<li><a href="https://www.ebi.ac.uk/Tools/msa/muscle/">Muscle</a></li>
<li><a href="https://blast.ncbi.nlm.nih.gov/Blast.cgi?CMD=Web&amp;PAGE_TYPE=BlastDocs&amp;DOC_TYPE=Download">NCBI-blast+</a></li>
<li><a href="https://github.com/davidemms/OrthoFinder">OrthoFinder</a></li>
<li><a href="https://openjdk.java.net/">OpenJDK8</a></li>
<li><a href="http://www.bork.embl.de/pal2nal/">PAL2NAL v14</a></li>
<li><a href="http://trimal.cgenomics.org/">trimAL</a></li>
<li>
<a href="http://www.perl.org/get.html">Perl</a> &amp; the modules
<ul>
<li><a href="http://metacpan.org/pod/BioPerl">perl-bioperl</a></li>
<li><a href="http://metacpan.org/pod/Data::Dumper">perl-data-dumper</a></li>
<li><a href="http://metacpan.org/pod/File::Tee">perl-file-tee</a></li>
<li><a href="http://metacpan.org/pod/Getopt::Long">perl-getopt-long</a></li>
<li><a href="http://search.cpan.org/~marekr/Pod-Usage-1.69/">perl-pod-usage</a></li>
<li><a href="https://metacpan.org/pod/release/DLUX/Parallel-ForkManager-0.7.5/ForkManager.pm">perl-parallel-forkmanager</a></li>
</ul>
</li>
<li><a href="https://github.com/tseemann/prokka">Prokka</a></li>
<li>
<a href="https://www.python.org/">Python</a> &amp; the modules
<ul>
<li><a href="https://biopython.org/">biopython</a></li>
<li><a href="https://matplotlib.org/">matplotlib</a></li>
<li><a href="http://www.numpy.org/">numpy</a></li>
<li><a href="http://pandas.pydata.org/">pandas</a></li>
<li><a href="http://seaborn.pydata.org/">seaborn</a></li>
</ul>
</li>
<li>
<a href="https://www.r-project.org/">R</a> &amp; the packages
<ul>
<li><a href="https://cran.r-project.org/web/packages/corrplot/index.html">corrplot</a></li>
<li><a href="https://cran.r-project.org/web/packages/ggplot2/">ggplot2</a></li>
<li><a href="https://cran.r-project.org/web/packages/gplots/">gplots</a></li>
<li><a href="https://cran.r-project.org/web/packages/pheatmap/index.html">pheatmap</a></li>
<li><a href="https://cran.r-project.org/web/packages/plotrix/">plotrix</a></li>
</ul>
</li>
<li><a href="https://sanger-pathogens.github.io/Roary/">Roary</a></li>
<li><a href="https://github.com/najoshi/sickle">Sickle-trim</a></li>
<li><a href="https://github.com/tseemann/snippy">Snippy</a></li>
<li><a href="https://github.com/sanger-pathogens/snp-sites">Snp-sites</a></li>
<li><a href="https://github.com/rrwick/Unicycler">unicycler</a></li>
<li><a href="https://www.gnu.org/software/wget/">wget</a></li>
</ul>
## Usage
<ul>
<li>
<p><strong>Print the help messages:</strong></p>
<pre>$pgcgap --help</pre>
</li>
<li>
<p><strong>Check for update:</strong></p>
<pre>$pgcgap --check-update</pre>
</li>
<li>
<p><strong>General usage:</strong></p>
<pre>$pgcgap [modules] [options]</pre>
</li>
<li>
<p><strong>Show parameters for each module:</strong></p>
<pre>$pgcgap [Assemble|Annotate|ANI|AntiRes|CoreTree|MASH|OrthoF|Pan|pCOG|VAR|STREE|ACC]</pre>
</li>
<li>
<p><strong>Show examples of each module:</strong></p>
<pre>$pgcgap Examples</pre>
</li>
</ul>
<p><br/></p>
<ul>
<li>
<p><strong>Setup COG database:</strong> (Users should execute this after the first installation of pgcgap)</p>
<pre>$pgcgap --setup-COGdb</pre>
<p><br/></p>
</li>
<li>
<p><strong>Modules:</strong></p>
<ul>
<li>
<p><strong>[--All]</strong>                          Perform Assemble, Annotate, CoreTree, Pan, OrthoF, ANI, MASH, AntiRes and pCOG functions with one command</p>
</li>
<li>
<p><strong>[--Assemble]</strong>                     Assemble reads (short, long or hybrid) into contigs</p>
</li>
<li>
<p><strong>[--Annotate]</strong>                     Genome annotation</p>
</li>
<li>
<p><strong>[--CoreTree]</strong>                     Construct single-core proteins tree and SNPs tree of single-copy core genes</p>
</li>
<li>
<p><strong>[--Pan]</strong>                          Run &quot;roary&quot; pan-genome pipeline with gff3 files, and construct a phylogenetic tree with the sing-copy core proteins called by roary</p>
</li>
<li>
<p><strong>[--OrthoF]</strong>                       Identify orthologous protein sequence
                                 families with &quot;OrthoFinder&quot;</p>
</li>
<li>
<p><strong>[--ANI]</strong>                          Compute whole-genome Average Nucleotide Identity ( ANI )</p>
</li>
<li>
<p><strong>[--MASH]</strong>                         Genome and metagenome similarity estimation using MinHash</p>
</li>
<li>
<p><strong>[--pCOG]</strong>                         Run COG annotation for each strain (*.faa),
		          and generate a table containing the relative
		          abundance of each flag for all strains</p>
</li>
<li>
<p><strong>[--VAR]</strong>                          Rapid haploid variant calling and core
                                 genome alignment with &quot;Snippy&quot;</p>
</li>
<li>
<p><strong>[--AntiRes]</strong>                      Screening of contigs for antimicrobial and virulence genes</p>
</li>
<li>
<p><strong>[--STREE]</strong>                        Construct a phylogenetic tree based on multiple sequences in one file</p>
</li>
<li>
<p><strong>[--ACC]</strong>                          Other useful gadgets (now includes 'Assess' for filtering short sequences in the genome and assessing the status of the genome only)</p>
</li>
</ul>
</li>
</ul>
<p><br/></p>
<ul>
<li>
<p><strong>Global Options:</strong></p>
<ul>
<li>
<p><strong>[--strain_num (INT)]</strong>             [Required by &quot;--All&quot;, &quot;--CoreTree&quot;, &quot;--Pan&quot;, &quot;--VAR&quot; and &quot;--pCOG&quot;]
                                 The total number of strains used for analysis, not including the reference genome</p>
</li>
<li>
<p><strong>[--ReadsPath (PATH)]</strong>             [Required by &quot;--All&quot;, &quot;--Assemble&quot; and &quot;--VAR&quot;]
                                 Reads of all strains as file paths ( Default ./Reads/Illumina )</p>
</li>
<li>
<p><strong>[--scafPath (PATH)]</strong>              [Required by &quot;--All&quot;, &quot;--Assess&quot;, &quot;--Annotate&quot;, &quot;--MASH&quot; and &quot;--AntiRes&quot;] Path for contigs/scaffolds (Default &quot;Results/Assembles/Scaf/Illumina&quot;)</p>
</li>
<li>
<p><strong>[--AAsPath (PATH)]</strong>               [Required by &quot;--All&quot;, &quot;--Pan&quot;, &quot;--OrthoF&quot; and &quot;--pCOG&quot;] Amino acids of all strains as fasta file paths,
                                 ( Default &quot;./Results/Annotations/AAs&quot; )</p>
</li>
<li>
<p><strong>[--reads1 (STRING)]</strong>              [Required by &quot;--All&quot;, &quot;--Assemble&quot; and
                                 &quot;--VAR&quot;] The suffix name of reads 1 ( for
                                 example: if the name of reads 1 is
                                 &quot;YBT-1520_L1_I050.R1.clean.fastq.gz&quot;,
                                 &quot;YBT-1520&quot; is the strain same, so the
                                 suffix name should be &quot;.R1.clean.fastq.gz&quot;)</p>
</li>
<li>
<p><strong>[--reads2 (STRING)]</strong>              [Required by &quot;--All&quot;, &quot;--Assemble&quot; and
                                 &quot;--VAR&quot;] The suffix name of reads 2( for
                                 example: if the name of reads 2 is
                                 &quot;YBT-1520_2.fq&quot;, the suffix name should be &quot;_2.fq&quot; )</p>
</li>
<li>
<p><strong>[--Scaf_suffix (STRING)]</strong>         [Required by &quot;--All&quot;, &quot;--Assess&quot;, &quot;--Annotate&quot; &quot;--MASH&quot;, &quot;--ANI&quot; and &quot;--AntiRes&quot;] The suffix of scaffolds or genome files. This is an important parameter that must be set (Default -8.fa)</p>
</li>
<li>
<p><strong>[--filter_length (INT)]</strong>          [Required by &quot;--All&quot;, &quot;--Assemble&quot; and &quot;--Assess&quot;]&gt; Sequences shorter than the 'filter_length' will be deleted from the assembled genomes. ( Default 200 )</p>
</li>
<li>
<p><strong>[--codon (INT)]</strong>                  [Required by &quot;--All&quot;, &quot;--Annotate&quot;, &quot;--CoreTree&quot; and &quot;--Pan&quot;] Translation table ( Default 11 )</p>
<ul>
<li>1                             Universal code</li>
<li>2                             Vertebrate mitochondrial code</li>
<li>3                             Yeast mitochondrial code</li>
<li>4                             Mold, Protozoan, and Coelenterate Mitochondrial code and Mycoplasma/Spiroplasma code</li>
<li>5                             Invertebrate mitochondrial</li>
<li>6                             Ciliate, Dasycladacean and Hexamita nuclear code</li>
<li>9                             Echinoderm and Flatworm mitochondrial code</li>
<li>10                            Euplotid nuclear code</li>
<li>11                            Bacterial, archaeal and plant plastid code ( Default )</li>
<li>12                            Alternative yeast nuclear code</li>
<li>13                            Ascidian mitochondrial code</li>
<li>14                            Alternative flatworm mitochondrial code</li>
<li>15                            Blepharisma nuclear code</li>
<li>16                            Chlorophycean mitochondrial code</li>
<li>21                            Trematode mitochondrial code</li>
<li>22                            Scenedesmus obliquus mitochondrial code</li>
<li>23                            Thraustochytrium mitochondrial code</li>
</ul>
</li>
<li>
<p><strong>[--suffix_len (INT)]</strong>             [Required by &quot;--All&quot;, &quot;--Assemble&quot; and
                                 &quot;--VAR&quot;] <strong>(Strongly recommended)</strong> The suffix length of the reads,
                                 that is the length of your reads name
                                 minus the length of your strain name. For
                                 example the --suffix_len of
                                 &quot;YBT-1520_L1_I050.R1.clean.fastq.gz&quot; is 26
                                 ( &quot;YBT-1520&quot; is the strain name ) ( Default 0 )</p>
</li>

<li><p><strong>[--fasttree]</strong>             [Can be used with "CoreTree", "Pan" and "OrthoF"] Use FastTree to construct phylogenetic tree quickly instead of IQ-TREE</p></li>
<li>
<p><strong>[--bsnum (INT)]</strong>             [Required by "CoreTree", "Pan", "OrthoF", "STREE", and "VAR"] Replicates for bootstrap of IQ-TREE ( Default 500 )</p>
</li>

<li>
<p><strong>[--fastboot (INT)]</strong>             [Required by "CoreTree", "Pan", "OrthoF", "STREE", and "VAR"] Replicates for ultrafast bootstrap of IQ-TREE. ( must >= 1000, Default 1000 )</p>
</li>

<li>
<p><strong>[--logs (STRING)]</strong>                Name of the log file ( Default Logs.txt )</p>
</li>
<li>
<p><strong>[--threads (INT)]</strong>                Number of threads to be used ( Default 4 )
<br/></p>
</li>
</ul>
</li>
<li>
<p><strong>Local Options:</strong></p>
<ul>
<li>
<p><strong>--Assemble</strong></p>
<ul>
<li>
<p><strong>[--platform (STRING)]</strong>         [Required] Sequencing Platform, &quot;illumina&quot;, &quot;pacbio&quot;, &quot;oxford&quot; and &quot;hybrid&quot; available ( Default illumina )</p>
</li>
<li>
<p><strong>[--assembler (STRING)]</strong>        [Required] Software used for illumina reads assembly, &quot;abyss&quot; and &quot;spades&quot; available ( Default abyss )</p>
</li>
<li>
<p><strong>[--kmmer (INT)]</strong>               [Required] k-mer size for genome assembly of Illumina data ( Default 81 )</p>
</li>
<li>
<p><strong>[--genomeSize (STRING)]</strong>       [Required] An estimate of the size of the genome. Common suffixes are allowed, for example, 3.7m or 2.8g. Needed by PacBio data and Oxford data ( Default Unset )</p>
</li>
<li>
<p><strong>[--short1 (STRING)]</strong>           [Required] FASTQ file of first short reads in each pair. Needed by hybrid assembly ( Default Unset )</p>
</li>
<li>
<p><strong>[--short2 (STRING)]</strong>           [Required] FASTQ file of second short reads in each pair. Needed by hybrid assembly ( Default Unset )</p>
</li>
<li>
<p><strong>[--long (STRING)]</strong>             [Required] FASTQ or FASTA file of long reads. Needed by hybrid assembly ( Default Unset )</p>
</li>
<li>
<p><strong>[--hout (STRING)]</strong>             [Required] Output directory for hybrid assembly ( Default ../../Results/Assembles/Hybrid )</p>
</li>
</ul>
</li>
<li>
<p><strong>--Annotate</strong></p>
<ul>
<li>
<p><strong>[--genus (STRING)]</strong>           Genus name of your strain ( Default &quot;NA&quot; )</p>
</li>
<li>
<p><strong>[--species (STRING)]</strong>         Species name of your strain ( Default &quot;NA&quot;)
<br/></p>
</li>
</ul>
</li>
<li>
<p><strong>--CoreTree</strong></p>
<ul>
<li>
<p><strong>[--CDsPath (PATH)]</strong>           [Required] CDs of all strains as fasta file
                             paths ( Default &quot;./Results/Annotations/CDs&quot; ),
		 if set to &quot;NO&quot;, the SNPs of single-copy core
		 genes will not be called</p>
</li>
<li>
<p><strong>[-c (FLOAT)]</strong>                 Sequence identity threshold, ( Default 0.5)</p>
</li>
<li>
<p><strong>[-n (INT)]</strong>                   Word_length,  -n 2 for thresholds 0.4-0.5,
                             -n 3 for thresholds 0.5-0.6, -n 4 for thresholds 0.6-0.7,
                             -n 5 for thresholds 0.7-1.0 ( Default 2 )</p>
</li>
<li>
<p><strong>[-G (INT)]</strong>                   Use global (set to 1) or local (set to 0)
                             sequence identity, ( Default 0 )</p>
</li>
<li>
<p><strong>[-t (INT)]</strong>                   Tolerance for redundance ( Default 0 )</p>
</li>
<li>
<p><strong>[-aL (FLOAT)]</strong>                Alignment coverage for the longer
                             sequence. If set to 0.9, the alignment
                             must cover 90% of the sequence ( Default 0.5 )</p>
</li>
<li>
<p><strong>[-aS (FLOAT)]</strong>                Alignment coverage for the shorter sequence.
                             If set to 0.9, the alignment must covers
                             90% of the sequence ( Default 0.7 )</p>
</li>
<li>
<p><strong>[-g (INT)]</strong>                   If set to 0, a sequence is clustered to
                             the first cluster that meets the threshold
                             (fast cluster). If set to 1, the program
                             will cluster it into the most similar
                             cluster that meets the threshold (accurate
                             but slow mode, Default 1)</p>
</li>
<li>
<p><strong>[-d (INT)]</strong>                   length of description in .clstr file. if
                             set to 0, it takes the fasta defline and
                             stops at first space ( Default 0 )
<br/></p>
</li>
</ul>
</li>
<li>
<p><strong>--Pan</strong></p>
<ul>
<li>
<strong>[--GffPath (PATH)]</strong>           [Required] Gff files of all strains as paths
                             ( Default &quot;./Results/Annotations/GFF&quot; )
<br/>
</li>

<li>
<strong>[--PanTree]</strong>                  Construct a phylogenetic tree of single-copy core proteins called by roary
<br/>
</li>

<li>
<strong>[--identi (INT)]</strong>            Minimum percentage identity for blastp ( Default 95 )
<br/>
</li>

</ul>
</li>
<li>
<p><strong>--OrthoF</strong></p>
<ul>
<li>
<p><strong>[--Sprogram (STRING)]</strong>        Sequence search program, Options: blast,
                             mmseqs, blast_gz, diamond ( Default blast)</p>
</li>
<li>
<p><strong>[--PanTree]</strong>                  Construct a phylogenetic tree of single-copy core proteins called by roary
<br/></p>
</li>
</ul>
</li>
<li>
<p><strong>--ANI</strong></p>
<ul>
<li>
<p><strong>[--queryL (FILE)]</strong>            [Required] The file containing paths to query
                             genomes, one per line ( Default scaf.list )</p>
</li>
<li>
<p><strong>[--refL (FILE)]</strong>              [Required] The file containing paths to reference genomes,
                             one per line. ( Default scaf.list )</p>
</li>
</ul>
</li>
<li>
<p><strong>--VAR</strong></p>
<ul>
<li>
<p><strong>[--refgbk (FILE)]</strong>            [Required] The full path and name of
                             reference genome in GENBANK format (
                             recommended ), fasta format is also OK.
                             For example: &quot;/mnt/g/test/ref.gbk&quot;</p>
</li>
<li>
<p><strong>[--qualtype (STRING)]</strong>        [Required] Type of quality values (solexa
                             (CASAVA &lt; 1.3), illumina (CASAVA 1.3 to 1.7),
	         sanger (which is CASAVA &gt;= 1.8)). ( Default sanger )</p>
</li>
<li>
<p><strong>[--qual (INT)]</strong>               Threshold for trimming based on average
                             quality in a window. ( Default 20 )</p>
</li>
<li>
<p><strong>[--length (INT)]</strong>             Threshold to keep a read based on length
                             after trimming. ( Default 20 )</p>
</li>
<li>
<p><strong>[--mincov (INT)]</strong>             The minimum number of reads covering a
                             site to be considered ( Default 10 )</p>
</li>
<li>
<p><strong>[--minfrac (FLOAT)]</strong>          The minimum proportion of those reads
                             which must differ from the reference ( Default 0.9 )</p>
</li>
<li>
<p><strong>[--minqual (INT)]</strong>            The minimum VCF variant call &quot;quality&quot; ( Default 100 )</p>
</li>
<li>
<p><strong>[--ram (INT)]</strong>                Try and keep RAM under this many GB ( Default 8 )</p>
</li>
<li>
<p><strong>[--tree_builder (STRING)]</strong>    Application to use for tree building
                             [raxml|fasttree|hybrid] ( Default fasttree)</p>
</li>
<li>
<p><strong>[--iterations (INT)]</strong>         Maximum No. of iterations for gubbins ( Default 5 )
<br/></p>
</li>
</ul>
</li>
<li>
<p><strong>--AntiRes</strong></p>
<ul>
<li>
<p><strong>[--db (STRING)]</strong>              [Required] The database to use, options: all, <a href="https://www.ncbi.nlm.nih.gov/pubmed/24145532">argannot</a>, 
                         <a href="https://www.ncbi.nlm.nih.gov/pubmed/27789705">card</a>, <a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5343136/">ecoh</a>, <a href="https://github.com/phac-nml/ecoli_vf">ecoli_vf</a>, <a href="https://megares.meglab.org/">megares</a>, <a href="https://www.biorxiv.org/content/10.1101/550707v1">ncbi</a>, <a href="https://www.ncbi.nlm.nih.gov/pubmed/24777092">plasmidfinder</a>, <a href="https://www.ncbi.nlm.nih.gov/pubmed/22782487">resfinder</a> and <a href="https://www.ncbi.nlm.nih.gov/pubmed/26578559">vfdb</a>. ( Default all )</p>
</li>
<li>
<p><strong>[--identity (INT)]</strong>           [Required] Minimum %identity to keep the result, 
                         should be a number between 1 to 100. ( Default 75 )</p>
</li>
<li>
<p><strong>[--coverage (INT)]</strong>           [Required] Minimum %coverage to keep the result, 
                         should be a number between 0 to 100. ( Default 50 )</p>
</li>
</ul>
</li>
<li>
<p><strong>--STREE</strong></p>
<ul>
<li>
<p><strong>[--seqfile (STRING)]</strong>        [Required] Path of the sequence file for analysis.</p>
</li>
<li>
<p><strong>[--seqtype (INT)]</strong>           [Required] Type Of Sequence (p, d, c for Protein, DNA, Codons, respectively). ( Default p )</p>
</li>
</ul>
</li>
<li>
<p><strong>--ACC</strong></p>
<ul>
<li><strong>[--Assess (STRING)]</strong>           Filter short sequences in the genome and assess the status of the genome</li>
</ul>
</li>
</ul>
</li>
<li>
<p><strong>Paths of external programs</strong></p>
<p>Not needed if they were in the environment variables path. Users can check with the &quot;--check-external-programs&quot; option for the essential programs.
<br/></p>
<ul>
<li>
<p><strong>[--abricate-bin (PATH)]</strong>          Path to abyss binary file. Default tries if abyss is in PATH;</p>
</li>
<li>
<p><strong>[--abyss-bin (PATH)]</strong>             Path to abyss binary file. Default tries if abyss is in PATH;</p>
</li>
<li>
<p><strong>[--canu-bin (PATH)]</strong>              Path to canu binary file. Default tries if canu is in PATH;</p>
</li>
<li>
<p><strong>[--cd-hit-bin (PATH)]</strong>            Path to cd-hit binary file. Default tries if cd-hit is in PATH;</p>
</li>
<li>
<p><strong>[--fastANI-bin (PATH)]</strong>           Path to the fastANI binary file. Default tries if fastANI is in PATH;</p>
</li>
<li>
<p><strong>[--gubbins-bin (PATH)]</strong>           Path to the run_gubbins.py binary file. Default tries if run_gubbins.py is in PATH;</p>
</li>
<li>
<p><strong>[--iqtree-bin (PATH)]</strong>            Path to the iqtree binary file. Default tries if iqtree is in PATH;</p>
</li>
<li>
<p><strong>[--mafft-bin (PATH)]</strong>             Path to mafft binary file. Default tries if mafft is in PATH;</p>
</li>
<li>
<p><strong>[--mash-bin (PATH)]</strong>              Path to the mash binary file. Default tries if mash is in PATH.</p>
</li>
<li>
<p><strong>[--muscle-bin (PATH)]</strong>            Path to the muscle binary file. Default tries if muscle is in PATH.</p>
</li>
<li>
<p><strong>[--orthofinder-bin (PATH)]</strong>       Path to the orthofinder binary file. Default tries if orthofinder is in PATH;</p>
</li>
<li>
<p><strong>[--pal2nal-bin (PATH)]</strong>           Path to the pal2nal.pl binary file. Default tries if pal2nal.pl is in PATH;</p>
</li>
<li>
<p><strong>[--prodigal-bin (PATH)]</strong>          Path to prodigal binary file. Default tries if prodigal is in PATH;</p>
</li>
<li>
<p><strong>[--prokka-bin (PATH)]</strong>            Path to prokka binary file. Default tries if prokka is in PATH;</p>
</li>
<li>
<p><strong>[--roary-bin (PATH)]</strong>             Path to the roary binary file. Default tries if roary is in PATH;</p>
</li>
<li>
<p><strong>[--sickle-bin (PATH)]</strong>            Path to the sickle-trim binary file. Default tries if sickle is in PATH.</p>
</li>
<li>
<p><strong>[--snippy-bin (PATH)]</strong>            Path to the snippy binary file. Default tries if snippy is in PATH;</p>
</li>
<li>
<p><strong>[--snp-sites-bin (PATH)]</strong>         Path to the snp-sites binary file. Default tries if snp-sites is in PATH;</p>
</li>
<li>
<p><strong>[--trimAL-bin (PATH)]</strong>           Path to the trimAL binary file. Default tries if trimAL is in PATH;</p>
</li>
<li>
<p><strong>[--unicycler-bin (PATH)]</strong>         Path to the unicycler binary file. Default tries if unicycler is in PATH;</p>
</li>
</ul>
</li>
</ul>
<p><br/></p>
<ul>
<li>
<p><strong>Setup COG database</strong></p>
<ul>
<li><strong>[--setup-COGdb]</strong>                  Users should execute this after first installation of pgcgap.
<br/></li>
</ul>
</li>
<li>
<p>Check the required external programs (<strong>It is strongly recommended that this step be performed after the installation of PGCGAP</strong>):</p>
<pre>$pgcgap --check-external-programs</pre>
</li>
</ul>
<p><br/></p>
## Examples

<strong><p>Example dataset can be download <a href="http://bcam.hzau.edu.cn/PGCGAP/PGCGAP_Examples.tar.gz">here</a>.</p></strong>
<ul>
<li>
<p><strong>Example 1:</strong> Perform all functions, take the <em>Escherichia coli</em> as an example, total 6 strains for analysis.<br/></p>
<p><strong>Notice</strong>: For the sake of flexibility, The &quot;VAR&quot; function needs to be added additionally.<br/></p>
<pre>
$pgcgap --All --platform illumina --filter_length 200 --ReadsPath Reads/Illumina --reads1 _1.fastq.gz --reads2 _2.fastq.gz --suffix_len 11 --kmmer 81 --genus Escherichia --species “Escherichia coli” --codon 11 --strain_num 6 --threads 4 --VAR --refgbk /mnt/h/PGCGAP_Examples/Reads/MG1655.gbff --qualtype sanger
</pre>
</li>
<li>
<p><strong>Example 2:</strong> Genome assembly.</p>
<ul>
<li>
<p>Illumina reads assembly</p>
<p>In this dataset, the naming format of the genome is “strain_1.fastq.gz” and “strain_2.fastq.gz”. The string after the strain name is “_1.fastq.gz”, and its length is 11, so &quot;--suffix_len&quot; was set to 11.</p>
<pre>
$pgcgap --Assemble --platform illumina --assembler abyss --filter_length 200 --ReadsPath Reads/Illumina --reads1 _1.fastq.gz --reads2 _2.fastq.gz --kmmer 81 --threads 4 --suffix_len 11
$pgcgap --Assemble --platform illumina --assembler spades --filter_length 200 --ReadsPath Reads/Illumina --reads1 _1.fastq.gz --reads2 _2.fastq.gz --threads 4 --suffix_len 11
$pgcgap --Assemble --platform illumina --assembler auto --filter_length 200 --ReadsPath Reads/Illumina --reads1 _1.fastq.gz --reads2 _2.fastq.gz --kmmer 81 --threads 4 --suffix_len 11</pre>
</li>
<li>
<p>Oxford reads assembly</p>
<p>Oxford nanopore only produces one reads file, so only the parameter of &quot;--reads1&quot; needs to be set, where the value is &quot;.fasta&quot;. “--genomeSize” is the estimated genome size, and users can check the genome size of similar strains in the NCBI database for reference. The parameter was set to &quot;4.8m&quot; here. The suffix of the reads file here is &quot;.fasta&quot; and its length is 6, so &quot;--suffix_len&quot; was set to 6.</p>
<pre>$pgcgap --Assemble --platform oxford --filter_length 200 --ReadsPath Reads/Oxford --reads1 .fasta --genomeSize 4.8m --threads 4 --suffix_len 6</pre>
</li>
<li>
<p>PacBio reads assembly</p>
<p>PacBio also produces only one reads file &quot;pacbio.fastq&quot;, the parameter settings are similar to Oxford. The strain name is &quot;pacbio&quot; with the suffix &quot;.fastq&quot; and the suffix length is 6, so &quot;--suffix_len&quot; was set to 6.</p>
<pre>$pgcgap --Assemble --platform pacbio --filter_length 200 --ReadsPath Reads/PacBio --reads1 .fastq --genomeSize 4.8m --threads 4 --suffix_len 6</pre>
</li>
<li>
<p>Hybrid assembly of short reads and long reads</p>
<p>Paired-end short reads and long reads in the directory “Reads/Hybrid/” were used as inputs. Illumina reads and long reads must be from the same isolates.</p>
<pre>$pgcgap --Assemble --platform hybrid --ReadsPath Reads/Hybrid --short1 short_reads_1.fastq.gz --short2 short_reads_2.fastq.gz --long long_reads_high_depth.fastq.gz --threads 4</pre>
</li>
</ul>
</li>
<li>
<p><strong>Example 3</strong>: Gene prediction and annotation</p>
<pre>$pgcgap --Annotate --scafPath Results/Assembles/Scaf/Illumina --Scaf_suffix -8.fa --genus Escherichia --species “Escherichia coli” --codon 11 --threads 4</pre>
</li>
<li>
<p><strong>Example 4</strong>: Constructing single-copy core protein tree and core SNPs tree</p>
<pre># Construct phylogenetic tree with FastTree (Quick without best fit model testing)<br/>$pgcgap --CoreTree --CDsPath Results/Annotations/CDs --AAsPath Results/Annotations/AAs --codon 11 --strain_num 6 --threads 4 --fasttree<br/><br/># Construct phylogenetic tree with IQ-TREE (Very slow with best fit model testing, traditional bootstrap)<br/>$pgcgap --CoreTree --CDsPath Results/Annotations/CDs --AAsPath Results/Annotations/AAs --codon 11 --strain_num 6 --threads 4 --bsnum 500<br/><br/># Construct phylogenetic tree with IQ-TREE (Slow with best fit model testing, ultrafast bootstrap)<br/>$pgcgap --CoreTree --CDsPath Results/Annotations/CDs --AAsPath Results/Annotations/AAs --codon 11 --strain_num 6 --threads 4 --fastboot 1000</pre>
</li>
<li>
<p><strong>Example 5:</strong> Constructing single-copy core protein tree only.</p>
<pre># Construct phylogenetic tree with FastTree (Quick without best fit model testing)<br/>$pgcgap --CoreTree --CDsPath NO --AAsPath Results/Annotations/AAs --codon 11 --strain_num 6 --threads 4 --fasttree<br/><br/># Construct phylogenetic tree with IQ-TREE (Very slow with best fit model testing, traditional bootstrap)<br/>$pgcgap --CoreTree --CDsPath NO --AAsPath Results/Annotations/AAs --codon 11 --strain_num 6 --threads 4 --bsnum 500<br/><br/># Construct phylogenetic tree with IQ-TREE (Slow with best fit model testing, ultrafast bootstrap)<br/>$pgcgap --CoreTree --CDsPath NO --AAsPath Results/Annotations/AAs --codon 11 --strain_num 6 --threads 4 --fastboot 1000</pre>
</li>
<li>
<p><strong>Example 6:</strong> Conduct pan-genome analysis and construct a phylogenetic tree of single-copy core proteins called by roary. <strong>Applicable to v1.0.27 and later</strong>.</p>
<pre># Construct phylogenetic tree with FastTree (Quick without best fit model testing)<br/>$pgcgap --Pan --codon 11 --identi 95 --strain_num 6 --threads 4 --GffPath Results/Annotations/GFF --PanTree --fasttree<br/><br/># Construct phylogenetic tree with IQ-TREE (Very slow with best fit model testing, traditional bootstrap)<br/>$pgcgap --Pan --codon 11 --identi 95 --strain_num 6 --threads 4 --GffPath Results/Annotations/GFF --PanTree --bsnum 500<br/><br/># Construct phylogenetic tree with IQ-TREE (Slow with best fit model testing, ultrafast bootstrap)<br/>$pgcgap --Pan --codon 11 --identi 95 --strain_num 6 --threads 4 --GffPath Results/Annotations/GFF --PanTree --fastboot 1000</pre>
</li>
<li>
<p><strong>Example 7:</strong> Inference of orthologous gene groups and construct a phylogenetic tree of single-copy Orthologue proteins. <strong>Applicable to v1.0.29 and later</strong>.</p>
<pre># Construct phylogenetic tree with FastTree (Quick without best fit model testing)<br/>$pgcgap --OrthoF --threads 4 --AAsPath Results/Annotations/AAs --fasttree<br/><br/># Construct phylogenetic tree with IQ-TREE (Very slow with best fit model testing, traditional bootstrap)<br/>$pgcgap --OrthoF --threads 4 --AAsPath Results/Annotations/AAs --bsnum 500<br/><br/># Construct phylogenetic tree with IQ-TREE (Slow with best fit model testing, ultrafast bootstrap)<br/>$pgcgap --OrthoF --threads 4 --AAsPath Results/Annotations/AAs --fastboot 1000</pre>
</li>
<li>
<p><strong>Example 8:</strong> Compute whole-genome Average Nucleotide Identity (ANI).</p>
<pre>$pgcgap --ANI --threads 4 --queryL scaf.list --refL scaf.list --Scaf_suffix .fa</pre>
</li>
<li>
<p><strong>Example 9:</strong> Genome and metagenome similarity estimation using MinHash</p>
<pre>$pgcgap --MASH --scafPath <PATH> --Scaf_suffix <STRING></pre>
</li>
<li>
<p><strong>Example 10:</strong> Run COG annotation for each strain.</p>
<pre>$pgcgap --pCOG --threads 4 --strain_num 6 --AAsPath Results/Annotations/AAs</pre>
</li>
<li>
<p><strong>Example 11:</strong> Variants calling and phylogenetic tree construction based on the reference genome.</p>
<pre># Construct phylogenetic tree with IQ-TREE (Very slow with best fit model testing, traditional bootstrap)<br/>$pgcgap --VAR --threads 4 --refgbk /mnt/h/PGCGAP_Examples/Reads/MG1655.gbff --ReadsPath Reads/Illumina --reads1 _1.fastq.gz --reads2 _2.fastq.gz --suffix_len 11 --strain_num 6 --qualtype sanger --bsnum 500<br/><br/># Construct phylogenetic tree with IQ-TREE (Slow with best fit model testing, ultrafast bootstrap)<br/>$pgcgap --VAR --threads 4 --refgbk /mnt/h/PGCGAP_Examples/Reads/MG1655.gbff --ReadsPath Reads/Illumina --reads1 _1.fastq.gz --reads2 _2.fastq.gz --suffix_len 11 --strain_num 6 --qualtype sanger --fastboot 1000</pre>
</li>
<li>
<p><strong>Example 12:</strong> Screening of contigs for antimicrobial and virulence genes</p>
<pre>$pgcgap --AntiRes --scafPath Results/Assembles/Scaf/Illumina --Scaf_suffix -8.fa --threads 6 --db all --identity 75 --coverage 50</pre>
</li>
<li>
<p><strong>Example 13:</strong> Filter short sequences in the genome and assess the status of the genome</p>
<pre>$pgcgap --ACC --Assess --scafPath Results/Assembles/Scaf/Illumina --Scaf_suffix -8.fa --filter_length 200</pre>
</li>
<li>
<p><strong>Example 14:</strong> Construct a phylogenetic tree based on multiple sequences in one file</p>
<pre># Construct phylogenetic tree with IQ-TREE (Very slow with best fit model testing, traditional bootstrap)<br/>$pgcgap --STREE --seqfile proteins.fas --seqtype p --bsnum 500 --threads 4<br/><br/># Construct phylogenetic tree with IQ-TREE (Slow with best fit model testing, ultrafast bootstrap)<br/>$pgcgap --STREE --seqfile proteins.fas --seqtype p --fastboot 1000 --threads 4</pre>
</li>
</ul>
## Generating Input files
<h3>Working directory</h3>
<p>The directory where the PGCGAP software runs.</p>
<h3>Assemble</h3>
<p>Pair-end reads of all strains in a directory or PacBio reads or Oxford nanopore reads (Default: ./Reads/Illumina/ under the working directory).</p>
<h3>Annotate</h3>
<p>Genomes files (complete or draft) in a directory (Default: Results/Assembles/Scaf/Illumina under the working directory).</p>
<h3>ANI</h3>
<p>QUERY_LIST and REFERENCE_LIST files containing full paths to genomes, one per line (default: scaf.list under the working directory). If the “--Assemble” function was run first, the list file will be generated automatically.</p>
<h3>MASH</h3>
<p>Genomes files (complete or draft) in a directory (Default: Results/Assembles/Scaf/Illumina under the working directory).</p>
<h3>CoreTree</h3>
<p>Amino acids file (With “.faa” as the suffix) and nucleotide (With “.ffn” as the suffix) file of each strain placed into two directories (default: “./Results/Annotations/AAs/” and “./Results/Annotations/CDs/”). The “.faa” and “.ffn” files of the same strain should have the same prefix name. The name of protein IDs and gene IDs should be started with the strain name. The “Prokka” software was suggested to generate the input files. If the “--Annotate” function was run first, the files will be generated automatically. If the “--CDsPath” was set to “NO”, the nucleotide files will not be needed.</p>
<h3>OrthoF</h3>
<p>A set of protein sequence files (one per species) in FASTA format under a directory (default: “./Results/Annotations/AAs/”). If the “--Annotate” function was run first, the files will be generated automatically.</p>
<h3>Pan</h3>
<p>GFF3 files (With “.gff” as the suffix) of each strain placed into a directory. They must contain the nucleotide sequence at the end of the file. All GFF3 files created by Prokka are valid (default: ./Results/Annotations/GFF/). If the “--Annotate” function was run first, the files will be generated automatically.</p>
<h3>pCOG</h3>
<p>Amino acids file (With “.faa” as the suffix) of each strain placed into a directory (default: ./Results/Annotations/AAs/). If the “--Annotate” function was run first, the files will be generated automatically.</p>
<h3>VAR</h3>
<ul>
<li>
<p>Pair-end reads of all strains in a directory (default: ./Reads/Over/ under the working directory).
<br/></p>
</li>
<li>
<p>The full path of reference genome in fasta format or GenBank format (<strong>must be provided</strong>).</p>
</li>
</ul>
<h3>AntiRes</h3>
<p>Genomes files (complete or draft) in a directory (Default: Results/Assembles/Scaf/Illumina under the working directory).</p>
<h3>STREE</h3>
<p>Multiple-FASTA sequences in a file, can be Protein, DNA and Codons.</p>
## Output Files
<h3>Assemble</h3>
<ul>
<li>
<p><strong>Results/Assembles/Illumina/</strong><br/>
Directories contain Illumina assembly files and information of each strain.
<br/></p>
</li>
<li>
<p><strong>Results/Assembles/PacBio/</strong><br/>
Directories contain PacBio assembly files and information of each strain.
<br/></p>
</li>
<li>
<p><strong>Results/Assembles/Oxford/</strong><br/>
Directories contain ONT assembly files and information of each strain.
<br/></p>
</li>
<li>
<p><strong>Results/Assembles/Hybrid/</strong><br/>
Directory contains hybrid assembly files of the short reads and long reads of the same strain.
<br/></p>
</li>
<li>
<p><strong>Results/Assembles/Scaf/Illumina</strong><br/>
Directory contains Illumina contigs/scaffolds of all strains. &quot;*.filtered.fas&quot; is the genome after excluding short sequences. &quot;*.prefilter.stats&quot; describes the stats of the genome before filtering, and &quot;*.filtered.stats&quot; describes the stats of the genome after filtering.
<br/></p>
</li>
<li>
<p><strong>Results/Assembles/Scaf/Oxford</strong><br/>
Directory contains Oxford nanopore contigs/scaffolds of all strains.
<br/></p>
</li>
<li>
<p><strong>Results/Assembles/Scaf/PacBio</strong><br/>
Directory contains PacBio contigs/scaffolds of all strains.
<br/></p>
</li>
</ul>
<h3>Annotate</h3>
<ul>
<li>
<p><strong>Results/Annotations/*_annotation</strong><br/>
directories contain <a href="https://github.com/tseemann/prokka?_blank">annotation files</a> of each strain.
<br/></p>
</li>
<li>
<p><strong>Results/Annotations/AAs</strong><br/>
Directory contain amino acids sequences of all strains.
<br/></p>
</li>
<li>
<p><strong>Results/Annotations/CDs</strong><br/>
Directory contain nucleotide sequences of all strains.
<br/></p>
</li>
<li>
<p><strong>Results/Annotations/GFF</strong><br/>
Directory contain the master annotation of all strains in GFF3 format.</p>
</li>
</ul>
<h3>ANI</h3>
<ul>
<li>
<p><strong>Results/ANI/ANIs</strong><br/>
The file contains comparation information of genome pairs. The document is composed of five columns, each of which represents query genome, reference genome, ANI value, count of bidirectional fragment mappings, total query fragments.
<br/></p>
</li>
<li>
<p><strong>Results/ANI/ANIs.matrix</strong><br/>
file with identity values arranged in a <a href="https://www.mothur.org/wiki/Phylip-formatted_distance_matrix?_blank">phylip-formatted lower triangular matrix</a>.
<br/></p>
</li>
<li>
<p><strong>Results/ANI/ANIs.heatmap</strong><br/>
An ANI matrix of all strains.
<br/></p>
</li>
<li>
<p><strong>Results/ANI/ANI_matrix.pdf</strong><br/>
The heatmap plot of &quot;ANIs.heatmap&quot;.</p>
</li>
</ul>
<h3>MASH</h3>
<ul>
<li>
<p><strong>Results/MASH/MASH</strong><br/>
The pairwise distance between pair genomes, each column represents Reference-ID, Query-ID, Mash-distance, P-value, and Matching-hashes, respectively.</p>
</li>
<li>
<p><strong>Results/MASH/MASH2</strong><br/>
The pairwise similarity between pair genomes, each column represents Reference-ID, Query-ID, similarity, P-value, and Matching-hashes, respectively.</p>
</li>
<li>
<p><strong>Results/MASH/MASH.heatmap</strong><br/>
A similarity matrix of all genomes.</p>
</li>
<li>
<p><strong>Results/MASH/MASH_matrix.pdf</strong><br/>
A heat map plot of &quot;MASH.heatmap&quot;.</p>
</li>
</ul>
<h3>CoreTree</h3>
<ul>
<li>
<p><strong>Results/CoreTrees/ALL.core.protein.fasta</strong><br/>
Concatenated and aligned sequences file of single-copy core proteins.
<br/></p>
</li>
<li>
<p><strong>Results/CoreTrees/ALL.core.protein.nwk</strong><br/>
The phylogenetic tree file of single-copy core proteins for all strains constructed by FastTree.
<br/></p>
</li>
<li>
<p><strong>Results/CoreTrees/ALL.core.protein.fasta.gb.treefile</strong><br/>
The phylogenetic tree file of single-copy core proteins for all strains constructed by IQ-TREE.
<br/></p>
</li>
<li>
<p><strong>Results/CoreTrees/faa2ffn/ALL.core.nucl.fasta</strong><br/>
Concatenated and aligned sequences file of single-copy core genes.
<br/></p>
</li>
<li>
<p><strong>Results/CoreTrees/ALL.core.snp.fasta</strong><br/>
Core SNPs of single-copy core genes in fasta format.
<br/></p>
</li>
<li>
<p><strong>Results/CoreTrees/ALL.core.snp.nwk</strong><br/>
The phylogenetic tree file of SNPs of single-copy core genes for all strains constructed by FastTree.
<br/></p>
</li>
<li>
<p><strong>Results/CoreTrees/ALL.core.snp.fasta.gb.treefile</strong><br/>
The phylogenetic tree file of SNPs of single-copy core genes for all strains constructed by IQ-TREE.
<br/></p>
</li>
<li>
<p><strong>Results/CoreTrees/&quot;Other_files&quot;</strong><br/>
Intermediate directories and files.
<br/></p>
</li>
</ul>
<h3>OrthoF</h3>
<ul>
<li><strong>Results/OrthoFinder/Results_orthoF</strong><br/>
Same as <a href="https://github.com/davidemms/OrthoFinder?_blank">OrthoFinder</a> outputs.
<br/></li>
<li><strong>Results/OrthoFinder/Results_orthoF/Single_Copy_Orthologue_Tree/</strong><br/>Directory contains Phylogenetic tree files based on Single Copy Orthologue sequences.<br/></li>
<li><strong>Results/OrthoFinder/Results_orthoF/Single_Copy_Orthologue_Tree/Single.Copy.Orthologue.nwk</strong><br/>Phylogenetic tree constructed by FastTree.<br/></li>
<li><strong>Results/OrthoFinder/Results_orthoF/Single_Copy_Orthologue_Tree/Single.Copy.Orthologue.fasta.gb.treefile</strong><br/>Phylogenetic tree constructed by IQ-TREE.<br/></li>
</ul>
<h3>Pan</h3>
<ul>
<li>
<p><strong>Results/PanGenome/Pangenome_Pie.pdf</strong><br/>
A 3D pie chart and a fan chart of the breakdown of genes and the number of isolates they are present in.
<br/></p>
</li>
<li>
<p><strong>Results/PanGenome/pangenome_frequency.pdf</strong><br/>
A graph with the frequency of genes versus the number of genomes.
<br/></p>
</li>
<li>
<p><strong>Results/PanGenome/Pangenome_matrix.pdf</strong><br/>
A figure showing the tree compared to a matrix with the presence and absence of core and accessory genes.
<br/></p>
</li>
<li>
<p><strong>Results/PanGenome/Core/Roary.core.protein.fasta</strong><br/>
Alignments of single-copy core proteins called by roary software.
<br/></p>
</li>
<li>
<p><strong>Results/PanGenome/Core/Roary.core.protein.nwk</strong><br/>
A phylogenetic tree of Roary.core.protein.fasta constructed by FastTree.
<br/></p>
</li>
<li>
<p><strong>Results/PanGenome/Core/Roary.core.protein.fasta.gb.treefile</strong><br/>
A phylogenetic tree of Roary.core.protein.fasta constructed by IQ-TREE.
<br/></p>
</li>
<li>
<p><strong>Results/PanGenome/Other_files</strong><br/>
see <a href="https://sanger-pathogens.github.io/Roary/?_blank">roary</a> outputs.
<br/></p>
</li>
</ul>
<h3>pCOG</h3>
<ul>
<li>
<p><strong>*.COG.xml, *.2gi.table, *.2id.table, *.2Sid.table</strong><br/>
Intermediate files.
<br/></p>
</li>
<li>
<p><strong>*.2Scog.table</strong><br/>
The super COG table of each strain.
<br/></p>
</li>
<li>
<p><strong>*.2Scog.table.pdf</strong><br/>
A plot of super COG table in pdf format.
<br/></p>
</li>
<li>
<p><strong>All_flags_relative_abundances.table</strong>
A table containing the relative abundance of each flag for all strains.</p>
</li>
</ul>
<h3>VAR</h3>
<ul>
<li>
<p><strong>Results/Variants/directory-named-in-strains</strong><br/>
directories containing substitutions (snps) and insertions/deletions (indels) of each strain. See <a href="https://github.com/tseemann/snippy?_blank">Snippy</a> outputs for detail.</p>
</li>
<li>
<p><strong>Results/Variants/Core</strong><br/>
  The directory containing SNP phylogeny files.</p>
<ul>
<li><strong>core.aln</strong> : A core SNP alignment includes only SNP sites.</li>
<li><strong>core.full.aln</strong> : A whole genome SNP alignment (includes invariant sites).</li>
<li><strong>core.*.treefile</strong> : Phylogenetic tree of the core SNP alignment based on the best-fit model of evolution selected using IQ-TREE (ignoring possible recombination).</li>
<li><strong>gubbins.core.full.node_labelled.final_tree.tre</strong> : Phylogenetic tree of the whole genome SNP alignment constructed with <strong>gubbins</strong> (get rid of recombination).</li>
</ul>
</li>
</ul>
<h3>AntiRes</h3>
<ul>
<li><strong>Results/AntiRes/*.tab</strong> : Screening results of each strain.</li>
<li><strong>Results/AntiRes/summary.txt</strong> : A matrix of gene presence/absence for all strains.</li>
</ul>
<h3>STREE</h3>
<ul>
<li><strong>Results/STREE/*.aln</strong> : Aligned sequences.</li>
<li><strong>Results/STREE/*.aln.gb</strong> : Conserved blocks of the aligned sequences.</li>
<li><strong>Results/STREE/*.aln.gb.treefile</strong> : The final phylogenetic tree.</li>
<li><strong>Results/STREE/*.aln.gb.iqtree</strong> : Log of IQ-TREE.</li>
</ul>
## License
<p>PGCGAP is free software, licensed under GPLv3.</p>
## Feedback and Issues
<p>Please report any issues to the <a href="https://github.com/liaochenlanruo/pgcgap/issues?_blank">issues page</a> or email us at <a href="&#109;&#x61;&#x69;&#108;&#116;&#111;&#58;&#x6c;&#x69;&#97;&#111;c&#104;&#101;&#x6e;&#108;&#97;&#x6e;&#114;&#x75;&#111;&#64;&#119;&#101;&#x62;m&#x61;&#105;&#x6c;&#46;&#x68;&#x7a;&#x61;&#117;&#46;&#x65;&#100;&#x75;&#46;&#99;n">&#108;&#x69;&#97;&#111;&#x63;&#104;&#101;&#x6e;&#x6c;&#97;&#x6e;&#114;&#x75;&#x6f;&#64;&#119;&#101;&#x62;m&#97;&#x69;&#108;&#46;&#104;&#122;&#97;&#117;&#x2e;&#101;du&#46;&#x63;&#110;</a>.</p>
## Citation
<ul>
<li>
<p>If you use this software please cite: Liu H, Xin B, Zheng J, Zhong H, Yu Y, Peng D, Sun M. Build a bioinformatics analysis platform and apply it to routine analysis of microbial genomics and comparative genomics. <em>Protocol exchange</em>, 2020. DOI: <a href="https://doi.org/10.21203/rs.2.21224/v5">10.21203/rs.2.21224/v5</a></p>
</li>
<li>
<p>If you use &quot;--Assemble&quot;, please also cite one or two of <a href="https://github.com/OpenGene/fastp">Fastp</a>, <a href="https://doi.org/10.1101/gr.214346.116">ABySS</a>, <a href="http://link.springer.com/chapter/10.1007%2F978-3-642-37195-0_13">SPAdes</a>, <a href="https://doi.org/10.1101/gr.215087.116">Canu</a>, or <a href="https://doi.org/10.1371/journal.pcbi.1005595">Unicycler</a>.</p>
</li>
<li>
<p>If you use &quot;--Annotate&quot;, please also cite <a href="https://doi.org/10.1093/bioinformatics/btu153">Prokka</a>.</p>
</li>
<li>
<p>If you use &quot;--CoreTree&quot;, please also cite <a href="https://doi.org/10.1093/bioinformatics/btl158">CD-HIT</a>, <a href="https://doi.org/10.1093/nar/gkf436">MAFFT</a>, <a href="https://doi.org/10.1093/nar/gkl315">PAL2NAL</a>, <a href="https://doi.org/10.1093/bioinformatics/btp348">trimAL</a>, <a href="https://doi.org/10.1093/molbev/msaa015">IQ-TREE</a> or <a href="https://doi.org/10.1371/journal.pone.0009490">FastTree</a>, and <a href="https://dx.doi.org/10.1099%2Fmgen.0.000056">SNP-sites</a>.</p>
</li>
<li>
<p>If you use &quot;--Pan&quot;, please also cite <a href="https://dx.doi.org/10.1093%2Fbioinformatics%2Fbtv421">Roary</a>, <a href="https://doi.org/10.1093/nar/gkf436">MAFFT</a>, <a href="https://doi.org/10.1093/bioinformatics/btp348">trimAL</a>, <a href="https://doi.org/10.1093/molbev/msaa015">IQ-TREE</a> or <a href="https://doi.org/10.1371/journal.pone.0009490">FastTree</a>.</p>
</li>
<li>
<p>If you use &quot;--OrthoF&quot;, please also cite <a href="https://dx.doi.org/10.1186%2Fs13059-019-1832-y">OrthoFinder</a>, <a href="https://doi.org/10.1093/nar/gkf436">MAFFT</a>, <a href="https://doi.org/10.1093/bioinformatics/btp348">trimAL</a>, <a href="https://doi.org/10.1093/molbev/msaa015">IQ-TREE</a> or <a href="https://doi.org/10.1371/journal.pone.0009490">FastTree</a>.</p>
</li>
<li>
<p>If you use &quot;--ANI&quot;, please also cite <a href="https://dx.doi.org/10.1038%2Fs41467-018-07641-9">fastANI</a>.</p>
</li>
<li>
<p>If you use &quot;--MASH&quot;, please also cite <a href="https://dx.doi.org/10.1186%2Fs13059-016-0997-x">Mash</a>.</p>
</li>
<li>
<p>If you use &quot;--VAR&quot;, please also cite <a href="https://github.com/najoshi/sickle">Sickle</a>, <a href="https://github.com/tseemann/snippy">Snippy</a>, <a href="https://dx.doi.org/10.1093%2Fnar%2Fgku1196">Gubbins</a>, <a href="https://doi.org/10.1093/molbev/msaa015">IQ-TREE</a>, and <a href="https://dx.doi.org/10.4161%2Ffly.19695">SnpEff</a>.</p>
</li>
<li>
<p>If you use &quot;--AntiRes&quot;, please also cite <a href="https://github.com/tseemann/abricate">Abricate</a> and the corresponding database you used: <a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6811410">NCBI AMRFinderPlus</a>, <a href="https://www.ncbi.nlm.nih.gov/pubmed/27789705">CARD</a>, <a href="https://www.ncbi.nlm.nih.gov/pubmed/22782487">Resfinder</a>, <a href="https://www.ncbi.nlm.nih.gov/pubmed/24145532">ARG-ANNOT</a>, <a href="https://www.ncbi.nlm.nih.gov/pubmed/26578559">VFDB</a>, <a href="https://www.ncbi.nlm.nih.gov/pubmed/24777092">PlasmidFinder</a>, <a href="https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5343136/">EcOH</a>, or <a href="https://academic.oup.com/nar/article/48/D1/D561/5624973">MEGARES 2.00</a>.</p>
</li>
<li>
<p>If you use &quot;--STREE&quot;, please also cite <a href="http://europepmc.org/abstract/MED/30976793">Muscle</a>, <a href="https://doi.org/10.1093/bioinformatics/btp348">trimAL</a>, and <a href="https://doi.org/10.1093/molbev/msaa015">IQ-TREE</a>.</p>
</li>
</ul>
## FAQ
<h3>Q1 VAR function ran failed to get annotated VCFs and Core results</h3>
<p>Check the log file named in &quot;strain_name.log&quot; under Results/Variants/&lt;strain_name&gt;/ directory. If you find a sentence like &quot;WARNING: All frames are zero! This seems rather odd, please check that 'frame' information in your 'genes' file is accurate.&quot; This is a snpEff error. Users can install JDK8 to solve this problem.</p>
<pre>$conda install java-jdk=8.0.112</pre>
<p>Click <a href="https://github.com/tseemann/snippy/issues/259?_blank">here</a> for more solutions.</p>
<h3>Q2 Could not determine version of minced please install version 2 or higher</h3>
<p>When running the Annotate function, this error could happen, the error message shows as following:</p>
<pre>
Error: A JNI error has occurred, please check your installation and try again
Exception in thread "main" java.lang.UnsupportedClassVersionError: minced has been compiled by a more recent version of the Java Runtime (class file version 55.0), this version of the Java Runtime only recognizes class file versions up to 52.0
	at java.lang.ClassLoader.defineClass1(Native Method)
	at java.lang.ClassLoader.defineClass(ClassLoader.java:763)
	at java.security.SecureClassLoader.defineClass(SecureClassLoader.java:142)
	at java.net.URLClassLoader.defineClass(URLClassLoader.java:468)
	at java.net.URLClassLoader.access$100(URLClassLoader.java:74)
	at java.net.URLClassLoader$1.run(URLClassLoader.java:369)
	at java.net.URLClassLoader$1.run(URLClassLoader.java:363)
	at java.security.AccessController.doPrivileged(Native Method)
	at java.net.URLClassLoader.findClass(URLClassLoader.java:362)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
	at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:349)
	at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
	at sun.launcher.LauncherHelper.checkAndLoadMain(LauncherHelper.java:495)
[01:09:40] Could not determine version of minced - please install version 2.0 or higher
</pre>
<p>Users can downgrade the minced to version 0.3 to solve this problem.</p>
<pre>$conda install minced=0.3</pre>
<p>Click <a href="https://github.com/bioconda/bioconda-recipes/pull/15407?_blank">here</a> for detail informations.</p>
<h3>Q3 dyld: Library not loaded: @rpath/libcrypto.1.0.0.dylib</h3>
<p>This error may happen when running function &quot;VAR&quot; on macOS. It is an error of openssl. Users can solve this problem as the following:</p>
<pre>
#Firstly, install brew if have not installed before
$ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

#Install openssl with brew
$brew install openssl

#Create the soft link for libraries
$ln -s /usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib /usr/local/lib/

$ln -s /usr/local/opt/openssl/lib/libssl.1.0.0.dylib /usr/local/lib/
</pre>
<p>Click <a href="https://gist.github.com/aklap/e885721ef15c8668ed0a1dd64d2ea1a7">here</a> for more informations</p>
<h3>Q4 Use of uninitialized value in require at Encode.pm line 61</h3>
<p>This warning may happen when running function &quot;Pan&quot;. It is a warning of Roary software.
The content of line 61 is &quot;require Encode::ConfigLocal;&quot;. Users can ignore the warning.
Click <a href="https://github.com/sanger-pathogens/Roary/issues/323">here</a> for details.</p>
## Updates
<ul>
<li>
<p>V1.0.3</p>
<ul>
<li>Updated ANI function.</li>
</ul>
</li>
<li>
<p>V1.0.4</p>
<ul>
<li>Add parallel for function &quot;pCOG&quot;.</li>
<li>Optimized drawing of ANI heat map.</li>
</ul>
</li>
<li>
<p>V1.0.5</p>
<ul>
<li>Bug repair for the input of gubbins.</li>
</ul>
</li>
<li>
<p>V1.0.6</p>
<ul>
<li>Modified CoreTree to split protein and SNPs tree constructing.</li>
</ul>
</li>
<li>
<p>V1.0.7</p>
<ul>
<li>Split Assemble and Annotate into two functions.</li>
<li>Added third-generation genome assembly function.</li>
<li>Changed the default parameters of the CoreTree function (aS 0.8 to 0.7 and aL 0.8 to 0.5).</li>
<li>Changed the name of function &quot;COG&quot; to &quot;pCOG&quot;.</li>
<li>Fixed the sorting bug for ANI heat map.</li>
</ul>
</li>
<li>
<p>V1.0.8</p>
<ul>
<li>Add the &quot;MASH&quot; function to compute genome distance and similarity using MinHash.</li>
</ul>
</li>
<li>
<p>V1.0.9</p>
<ul>
<li>The function of constructing a single-copy core protein phylogenetic tree was added to &quot;Pan&quot;.</li>
<li>Fixed a bug of plot_3Dpie.R, Optimized image display, and a fan chart has been added.</li>
<li>Fixed a bug for plotting the ANI matrix.</li>
</ul>
</li>
<li>
<p>V1.0.10</p>
<ul>
<li>Add the &quot;AntiRes&quot; function to screening of contigs for antimicrobial and virulence genes.</li>
</ul>
</li>
<li>
<p>V1.0.11</p>
<ul>
<li>Users now can choose &quot;abyss&quot; or &quot;spades&quot; for illumina reads aseembly.</li>
<li>New support for hybrid assembly of paired-end short reads and long reads.</li>
<li>Add the selecting of best-fit model of evolution for DNA and protein alignments before constructing a phylogenetic tree.</li>
<li>Optimized display of help information. Users can check parameters for each modulewith command &quot;pgcgap [Assemble|Annotate|ANI|AntiRes|CoreTree|MASH|OrthoF|Pan|pCOG|VAR]&quot;, and can look up the examples of each module with command &quot;pgcgap Examples&quot;.</li>
</ul>
</li>
<li>
<p>V1.0.12</p>
<ul>
<li>Added automatic mode for illumina genome assembly. First, PGCGAP calls &quot;ABySS&quot; for genome assembly. When the assembled N50 is less than 50,000, it automatically calls &quot;SPAdes&quot; to try multiple parameters for assembly.</li>
<li>Added ability to filter short sequences of assembled genomes.</li>
<li>Added function of genome assembly status assessment.</li>
<li>Modified the drawing script of ANI and MASH modules so that it can automatically adjust the font size according to the number of samples.</li>
</ul>
</li>
<li>
<p>V1.0.13</p>
<ul>
<li>Fixed the &quot;running error&quot; bug of function &quot;Assess&quot; in module &quot;ACC&quot;.</li>
<li>Added module &quot;STREE&quot; for constructing a phylogenetic tree based on multiple sequences in one file.</li>
</ul>
</li>
<li>
<p>V1.0.14</p>
<ul>
<li>The relative_abundances of flags among strains will not be called while the strain number is less than two.</li>
<li>Fixed the error of function &quot;Assess&quot; in module &quot;ACC&quot;.</li>
</ul>
</li>
<li>
<p>V1.0.15</p>
<ul>
<li>When the number of threads set by the user exceeds the number of threads owned by the system, PGCGAP will automatically adjust the number of threads to avoid program crash.</li>
<li>Add FASTQ preprocessor before Illunima genome assembly: adapter trimming, polyG tail trimming of Illumina NextSeq/NovaSeq reads, quality filtering (Q value filtering, N base filtering, sliding window filtering), length filtering.</li>
</ul>
</li>
<li>
<p>V1.0.16</p>
<ul>
<li>Reduced the number of Racon polishing rounds for better speed performance when peforming genome assembly.</li>
<li>Force overwriting existing output folder when running &quot;Annotate&quot; analysis to avoid program crash.</li>
</ul>
</li>
<li>
<p>V1.0.17</p>
<ul>
<li>Fixed a bug that the program can not go back to the working directory after genome annotation.</li>
<li>Added scripts to check if there were single-copy core proteins found while running module &quot;CoreTree&quot;.</li>
<li>Modified the help message.</li>
</ul>
</li>
<li>
<p>V1.0.18</p>
<ul>
<li>Updated the downloading link of COG database.</li>
<li>Users can choose the number of threads used for running module "STREE".</li>
</ul>
</li>

<li>
<p>V1.0.19</p>
<ul>
<li>Can resume from break-point when downloading the COG database.</li>
<li>Fixed a bug that failed to create multi-level directories.</li>
</ul>
</li>

<li>
<p>V1.0.20</p>
<ul>
<li>Fixed a little bug (path error) of module "VAR".</li>
<li>Fixed a little bug of module "CoreTree" to avoid the interference of special characters in sequence ID to the program.</li>
</ul>
</li>

<li>
<p>V1.0.21</p>
<ul>
<li>Change the default search program "blast" to "diamond" of module "OrthoF".</li>
<li>Fixed a bug of module "pCOG" to output the right figure.</li>
</ul>
</li>

<li>
<p>V1.0.22</p>
<ul>
<li>The drawing function of module "ANI" and module "MASH" has been enhanced, including automatic adjustment of font size and legend according to the size of the picture.</li>
<li>Fixed a bug of module "ANI", that is no heatmap will be drawn when there is "NA" in the ANI matrix in the previous versions.</li>
<li>When the ANI value or genome similarity is greater than 95%, an asterisk (*) will be drawn in the corresponding cell of the heatmap.</li>
</ul>
</li>

<li>
<p>V1.0.23</p>
<ul>
<li>The "--Assess" function of module "ACC" was enhanced to (1) generate a summary file containing the status of all genomes (before and after the short sequence filtering), (2) auto move the low-quality genomes (that is genomes with N50 length less than 50 k) to a directory, and others to another directory.</li>
</ul>
</li>

<li>
<p>V1.0.24</p>
<ul>
<li>Fixed a little bug of module "Pan" to avoid the interference of special characters (>) in sequence ID to the program.</li>
</ul>
</li>

<li>
<p>V1.0.25</p>
<ul>
<li>Gblocks was used to eliminate poorly aligned positions and divergent regions of an alignment of DNA or protein sequences in module "CoreTree" and "Pan".</li>
<li>The parameter "--identi" was added into module "Pan" to allow users to set the minimum percentage identity for blastp.</li>
</ul>
</li>

<li>
<p>V1.0.26</p>
<ul>
<li>Adjusted the font size with the variation of genome number and the string length of the genome name when plotting the heat map of module "ANI" and "MASH".</li>
<li>Two heat map are provided, one of which with a star (means the similarity of the two genomes is larger than 95%) and another without a star, when performing the "ANI" and "MASH" analysis.</li>
</ul>
</li>

<li>
<p>V1.0.27</p>
<ul>
<li>The Amino Acid files are no longer needed when performing the Pan-genome analysis with module Pan.</li>
</ul>
</li>

<li>
<p>V1.0.28</p>
<ul>
<li>Users can check and install the latest version of PGCGAP by the command "pgcgap --check-update".</li>
<li>Update module Assemble to allow polish after the assembly of PacBio and ONT data.</li>
<li>Update module pCOG to adjust the latest database of <a href="https://ftp.ncbi.nih.gov/pub/COG/COG2020/data/" target="_blank">COG 2020</a>.</li>
<li>Optimized the drawing and color scheme of the module pCOG.</li>
<li>Fixed the parameter "CoreTree" in the module Pan to avoid program termination caused by the ">" in non-sequence lines.</li>
</ul>
</li>

<li>
<p>V1.0.29</p>
<ul>
<li>Function added to module OrthoF: Phylogenetic tree can be constructed automatically with the Single Copy Orthologue Sequences called by module OrthoF.</li>
<li>Fixed the "permission denied" error when moving directories on the WSL platform.</li>
</ul>
</li>

<li>
<p>V1.0.30</p>
<ul>
<li>Replace Gblocks with trimAL to trim MSA (module CoreTree, Pan, STREE, and OrthoF).</li>
<li>Replaced Modeltest-ng and Raxml-ng with IQ-TREE (module CoreTree, Pan OrthoF, and VAR).</li>
<li>Added the option of using fasttree to build phylogenetic tree (module CoreTree, Pan, and OrthoF).</li>
</ul>
</li>

<li>
<p>V1.0.31</p>
<ul>
<li>The default replicates for bootstrap testing of IQ-TREE was set to 500.</li>
<li>Add the method for phylogenetic tree constructing with ultrafast bootstrap of IQ-TREE.</li>
<li>Prevent the log from being written to the tree file generated by FastTree.</li>
</ul>
</li>

<li>
<p>V1.0.32</p>
<ul>
<li>A more colorful version, try "pgcgap Examples" to have a look.</li>
<li>Updated module AntiRes: the parameter --db had been modified to add choices of "all" and "megares".</li>
<li>A little optimization of module VAR.</li>
<li>Replaced conda with mamba to update PGCGAP more quickly.</li>
</ul>
</li>

</ul>
<hr />
<p><center><strong>
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
<span id="busuanzi_container_site_pv">Total visits: <span id="busuanzi_value_site_pv"></span> times</span>
<span class="post-meta-divider">|</span>
<span id="busuanzi_container_site_uv">Visitors: <span id="busuanzi_value_site_uv"></span> people</span>
</strong></center></p>
