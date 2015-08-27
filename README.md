Code :: InformationIsPower
==================

Code provided on the exeResearch LLC website ( www.exeResearch.com ).

The following functions/applications are commonly used in our research
projects. A brief description of each function is provided below along
with detailed instructions. The Scientific Vector Language (SVL)
functions require the use of
[Chemical Computing Group, Inc's](http://www.chemcomp.com) Molecular
Operating Environment (MOE).  

##MACCS Key Counts (SVL)
This function counts the occurrence of the 166 MACCS keys for each
molecule in a MOE database (mdb). The number of each key's occurrence
is written to a user specified CSV file. The option to include the
compounds' names and endpoint values in the CSV file is an option from the
``opts`` variable.

The default values are:
* Column (field) with molecule is 'mol' (``molField:'mol'``)
* Include the endpoints if the endpoint column name is provided (``endpointField:''``)
* Include the compound's name or SMILES string. Not indicating a compound name file
  (``nameField:''``) uses the compound's name returned with ``cName Chains[]`` or the 
  compound's SMILES string if no name is present.
* Column headers for MACCS keys will be returned in lower case letters (``uppers:0``)

####Instructions
Load this function  
``load '~/code/svl/utilities/MACCSkeyCounts.svl';``

Calculate the MACCS Key Counts for a MDB of compounds  
``MACCSkeyCounts['Selwood_dataset.mdb', 'Selwood_MACCSkeyCounts.csv', [molField:'mol', endpointField:'pEC50', nameField:'name']]``

***

##Set Amide Bonds to 180 Degrees (SVL)
It is common for small drug-like compounds and peptides that are constructed
from SMILES strings and even SDfiles to have amide bonds where the hydrogen of
the nitrogen atom and the oxygen of the carboxyl group result in a dihedral 
angle of approximately 0 degrees. This function sets all amide dihedral angles
to 180 degrees and provides the option for energy minimization (this
functionality is not implemented in the MDB version because of the energy
minimization function with the MDB framework). The interactive (MOE 3D window)
version allows the user to select the amide bond of interest.

The MDB version of this function provides the option to overwrite the original
molecule or create a new column (field) for the compounds. The MDB version
does indicate how many amide bonds were corrected. It is recommended that
after changing the amide dihedral angle(s) within a database of compounds
that the MDB energy minimization (MDB | Compute | Energy Minimize) function
be performed using the desired molecular force field. 

Note: Amide groups within rings are not modified.

The default values are:
* No energy minimization for MOE 3D window (``nrgOpt:0``)
* Column (field) with molecule is ``'mol'`` (``molField:'mol'``)
* Save corrected compound to a new column ``'modMol'`` (``newMolField:'modMol'``)
* Maximum peptide length is set with ``'maxPeptideLength'`` (``maxPeptideLength:15``)

####Instructions
Load this function  
``load '~/code/svl/utilities/db_SetAmide180.svl'``

For a compound in the MOE 3D window (either a single small-organic
drug-like compound or a selected molecule)  
``SetAmide180[]``

For a compound in the MOE 3D window with energy minimization of the new
conformation  
``SetAmide180[nrgOpt:1]``

For a collection of compound in a MDB saving the new conformation to
the originating column of the compound  
``db_SetAmide180['drugLike_compounds.mdb', [molField:'mol', newMolField:'']]``

***

###Notes:
* SVL functions (code) are traditionally stored by the author in
  ``~/code/svl``. Unless otherwise noted, the provided SVL code is stored
  in ``~/code/svl/utilities``. The instructions for each function reflects
  where each file is stored.

