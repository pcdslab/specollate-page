## Train, Test, and Validation Datasets

We use NIST and MassIVE spectral libraries to train SpeCollate. The spectral libraries are preprocessed to generate two sets of data, i.e., spectra and their corresponding peptides. The preprocessed training data can be downloaded from [here](https://drive.google.com/uc?export=download&id=10bZbMdc2eN_l4ToJd6ruzNX7t6wIUfHw). We obtained *~4.8* million spectra with known peptide sources containing *~.5* million spectra from modified peptides. Nine different types of modifications found in the training dataset are used for training the network. These modifications and their corresponding character values are given in table 1. Other details of the training dataset are given in table 2.

*Table 1: Modifications used in the training data and the corresponding character assignment for represention within peptide sequence.*  

| Modifications   | Value |
| --------------- | ----- |
| Phosphop        | p     |
| Oxidation       | o     |
| Deamidation     | h     |
| Carbamidomethyl | c     |
| Acetyl          | a     |
| Ammonia-loss    | r     |
| Carbamyl        | y     |
| Dehydrated      | d     |
| Delta:H(2)C(2)  | t     |

<br/>

*Table 2: Characteristics of training dataset used. Data was acquired from online repositories including NIST peptide library, MassIVE. The post translation modifications in the dataset are CAM, Phosphorylation, Oxidation, and N-terminal Acetylation.*  

| Parameters         | Values |
| ------------------ | ------ |
| Training Samples   | 4.8M   |
| Charge 2           | 2.6M   |
| Charge 3           | 1.6M   |
| Charge 4           | 0.4M   |
| Other Charges      | 1.2M   |
| Unmodified Samples | 4.3M   |
| Modified Samples   | 0.5M   |
| Max Charge         | 8      |
| Number of Species  | 7      |

Train/Test split of 80/20 was used for the following libraries to train SpeCollate:
- [human_synthetic_hcd_selected](https://chemdata.nist.gov/dokuwiki/doku.php?id=peptidew:lib:kustersynselected20170530)
- [cptac2_mouse_hcd_selected](https://chemdata.nist.gov/dokuwiki/doku.php?id=peptidew:clib:mousehcd_selected20141124)
- [chinese_hamster_hcd_selected](https://chemdata.nist.gov/dokuwiki/doku.php?id=peptidew:lib:cho_20180223)
- [human_hcd_tryp_best](https://chemdata.nist.gov/dokuwiki/doku.php?id=peptidew:lib:humanhcd20160503)
- [MassIVE](https://massive.ucsd.edu/ProteoSAFe/result.jsp?task=daa7c2c21f9a45c08c41e071a3729d67&view=download_filtered_mgf_library&show=true)
- [rat_qtof_consensus_final_true_lib](https://chemdata.nist.gov/dokuwiki/doku.php?id=peptidew:lib:rat_qtof)
- [human_hcd_tryp_good](https://chemdata.nist.gov/dokuwiki/doku.php?id=peptidew:lib:humanhcd20160503)
- [human_hcd_semitryp](https://chemdata.nist.gov/dokuwiki/doku.php?id=peptidew:lib:humanhcd20160503)

The following dataset was witheld for validation purpose:
- [human_hcd_labelfree_phospho_selected_passed](https://chemdata.nist.gov/dokuwiki/doku.php?id=peptidew:lib:phoshopept_labelfree_20190214)
- [ProteomeTools](http://www.proteometools.org/index.php?id=53)
