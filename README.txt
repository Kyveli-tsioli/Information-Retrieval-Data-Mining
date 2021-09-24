The code for the project can be found at the "IRDM_CW1_St_number_20102571.ipynb" file.
This notebook contains all the necessary functions that implement the project questions.

The function "read_file" is used to read the files as pandas dataframes.

The function "preprocessing" takes as arguments the data as a list and 2 flags denoting whether stemming and stop words removal should be performed.

The function "term_frequencies" is used for the Zipf's law verification.

The function "build" is called only once in order to create the initial data structures (dictionaries) that will contain all the information needed from the raw data, in an efficient and useful form. Three dictionaries are returned:
- dictionary whose keys are the query IDs and whose values are the lists of associated passage IDs 
- dictionary whose keys are the query IDs and whose values are the list of the pre-processed query tokens
- dictionary whose keys are the passage IDs and whose values are the list of the pre-processed passage tokens

The function "inv_idx" is responsible for creating the query-specific inverted index.
It takes as argument the dictionary which associates passage IDs with cleaned lists of theis tokens, and performs filtering so that we are only handling the passage IDs that are relevant to each specific query. (Reminder: goal is to re-rank)

The "tf_idf_representation" function computes the tf_idf representation of each passage.

The "cosine_similarity" function computes the similarity between a query and one of its associated passages which are represented as vectors, using the dictionary data structure. In this dictionary, the key is the token of the passage and the respective value is the tf_idf representation of that token. For speed up in the computational time, the dot product is performed only on the common keys between the 2 vectors, while in the normalisation all the tokens that make up each vector are taken into account.

The function "BM_25" calculates the BM_25 score for the passages of each query.
The case of query tokens appearing more than once in the query is taken into consideration.

Then all the scores are computed and sorted in decreasing order. 

The function "smoothing" performs smoothing according to the 3 specified techniques.
The output is calculated in the logarithmic scale to avoid overflow/underflow issues.
Attention should be paid on how the frequencies and the lengths are computed.

Then we perform smoothing for all the query and their associated passages,
Using the relevant inverted index for deriving the frequencies, and the scores calculated from the above function. 