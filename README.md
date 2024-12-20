![GraphVisulization](images/graph_construction.png)  
# Introduction
The repository contains the code for the winning project of the 2023 [BioHack NYC](https://www.biohacknyc.com/) hackathon. Our goal was to use graph neural networks to predict to predict the identity of amino acids within ligand binding pockets.
##Inspiration
One of the major goals in the field of protein design is creating a protein that can bind any arbitraty small molecule. We were particularly struck by the work of [McCann et al.](https://www.science.org/doi/full/10.1126/sciadv.abh3421?rfr_dat=cr_pub++0pubmed&url_ver=Z39.88-2003&rfr_id=ori%3Arid%3Acrossref.org). They were able to design a protein that selectily binds VX nerve agent. The protein was designed using an algorithm called protEvolver, a physics-based genetic algorithim that optimizes protein-ligand interfaces. Methods like these are slow and computationally expensive. The success of [proteinMPNN](https://www.science.org/doi/10.1126/science.add2187?url_ver=Z39.88-2003&rfr_id=ori:rid:crossref.org&rfr_dat=cr_pub%20%200pubmed) inspired us to try to create a smiliar machine learning model that could incorporate small molecule information in the sequence prediction task. Such a model copuld be used to greatly speed up the design process.  
**n.b. Since our work on this project, the developers of proteinMPNN have released LigandMPNN**
## Data
To run this repository on your own the first thing you need to do is download the [PDBind](http://www.pdbbind.org.cn/) refined set and extract the download into this repository.  
This dataset contains high resolution protein ligand complexes with well characterized binding information. You can read more about the dataset on the website.  
## Environment
Use the yml file to install all required dependencies  
```
conda env create -f environment.yml
```
# Results
Our model achieved 78% sequence revocery across the entire validation set.
![fullrecovery](images/fullrecovery.png)  
There appears to be a slight bias towards over represeneted amino acids and away from under represented amino acids.  
![AArep](images/AArep.png)  
As expected, the models performance was better on proteins with a large number of homologs. Interestingly, the average sequence recovery on proteins with no homologs was 30% with some individual proteins achieving 100% sequence recovery. This demonstrates the models ability to generalize to novel protein ligand complexes but is still too limited to be considered a valuable tool for design.  
![homologs](images/homologs.png)
## Result Recreation Walkthoguh
The notebooks need to be run in a specific order.  
1. Clean Pockets and Examine Ligand Data  
2. Generate Amino Acid Embeddings  
3. Compile Graphs  
4. Writing Fasta **Optional**
5. Sequence Similarity **Optional**
6. Model Training  
7. Model Evaluation  
