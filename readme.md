# Predict proteins 3D structures generated from a bacteria coding DNA sequence
This project was done as part of School of AI health hackathon. 
It's heavly based on Eric Alcaid https://github.com/EricAlcaide/MiniFold/ work's.

## Context

Generation of 3D proteins structures of gut bacterias

By using Mini Alphafold library based on deep neural network, we want to predict new 3D configurations of proteins from primary structures of amino acids. In biology, protein function depends on its size and its tertiary structure, which defines the biological activity and.
The process will be conduct on intestinal microbiotia, which constitutes a interesting field of investigation, given its relative newness and the large number of proteins involved.

## Solving the problem

Protein folding is the biological process where the amino-acid primary sequence is transformed into a native 3-dimensional structure, that determines its biological activity. However, to model those configurations in research domain, it implies and complex process witch are done actually with NMR and radio cannot be done using traditional tools. Indeed, using artificial intelligence and deep learning, the objective is to understand the relation between the 3-dimensional structure of a protein and the amino acid primary sequence.


## Pipeline

Input your a bacteria coding DNA sequence to generate 3D structure of proteins
<img src="https://github.com/styloInt/ScaleProteoFold/blob/master/imgs/Pipeline.PNG">


## Running on your computer

### Re-Training (optional)
Here are the following steps in order to run the code locally or in the cloud:
1. Clone the repo: `git clone https://github.com/styloInt/ScaleProteoFold`
2. Install dependencies: `pip install -r requirements.txt`
3. Get & format the data
	1. Download data [here](https://github.com/aqlaboratory/proteinnet) (select CASP7 text-based format)
	2. Extract/Decompress the data in any directory
	3. Create the `/data` folder inside the `MiniFold` directory and copy the `training_30` file to it. Change extension to `.txt`.
4. Execute data preprocessing notebooks (`preprocessing` folder) in the following order (we plan to release simple scripts instead of notebooks very soon):
	1. `get_proteins_under_200aa.jl`:  - selects proteins under 200 residues - (you will need the [Julia programming language](https://julialang.org/) v1.0 in order to run it)
		1. **Alternatively**: `julia_get_proteins_under_200aa.ipynb` (you will need Julia as well as [iJulia](https://github.com/JuliaLang/IJulia.jl))
	3. `get_angles_from_coords_py.ipynb` - calculates dihedral angles from raw coordinates
	4. `angle_data_preparation_py.ipynb`
5. Run the models!
	1. For **distance prediction**: `predicting_distances.ipynb`
	2. For **angles prediction**: `predicting_angles.ipynb`

### Predict proteins structures generated by a bactaria

```
	python predictsStructure/predictSequences.py filename_sequence
	
	example : python predictsStructure/predictSequences.py dnaseq.txt
```
Create the folder : predictsStructure/saveResults
It will save the results in this directory

# Limitatons
We had to compute the PSSM(Position-Specific Scoring Matrix). We need to do more extensive tests to check the function.

## Future

The future directions of the project as well as planned/work-in-progress improvements are extensively exposed in the [future.md](future.md) file. In a brief way, some promising ideas:

* Train with crops of 64x64, not windows of 200x200 (and average at prediction time).
* Use data from Multiple Sequence Alignments (MSA) such as paired changes bewteen AAs.
* Use distance map as potential input for angle prediction (or vice versa?) .
* Train with more data (in the cloud?)
* ...

*"Science is a Work In Progress."*


## Limitations

This project has been developed in one week by 1 person and,, therefore, many limitations have appeared.
They will be listed below in order to give a sense about what this project is and what it's not.
We used the pretrained models of Eric Alading. Improving the results was not the goal of this project.

* **No usage of Multiple Sequence Alignments (MSA)**: The methods developed in this project don't use [MSA](https://en.wikipedia.org/wiki/Multiple_sequence_alignment) nor MSA-based features as input. 
* **Computing power/memory**: Development of the project has taken part in a computer with the following specs: Intel i7-6700k, 8gb RAM, NVIDIA GTX-1060Ti 6gb and 256gb of storage. The capacity for data exploration, processing, training and evaluating the models is limited.
* **GPU/TPUs for training**: The models were trained and evaluated on a single GPU. No cloud servers were used. 

Due to these limitations and/or constraints, the precission/accuracy the methods here developed can achieve is limited when compared against SOTA algorithms.


## References
* [MiniFold](https://github.com/EricAlcaide/MiniFold/)
* [DeepMind original blog post](https://deepmind.com/blog/alphafold/)
* [AlphaFold @ CASP13: “What just happened?”](https://moalquraishi.wordpress.com/2018/12/09/alphafold-casp13-what-just-happened/#s2.2)
* [Siraj Raval's YT video on AlphaFold](https://www.youtube.com/watch?v=cw6_OP5An8s)
* [ProteinNet dataset](https://github.com/aqlaboratory/proteinnet)

 
