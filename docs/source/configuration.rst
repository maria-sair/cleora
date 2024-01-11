.. _configuration:

Cleora Configuration
==================================

Synopsis
--------

**cleora** [OPTIONS] [inputs]...

Configuration Options
---------------------

1. Input Files  

   - **Usage:** Positional arguments ``[inputs]...``  
   - **Description:** Paths to input files.  

2. File Type  

   - **Option:** ``--type`` or ``-t``  
   - **Description:** Specifies the input file type. Supported types are ``.tsv`` (tab-separated values) and ``.json``.  

3. Dimension  

   - **Option:** ``--dimension`` or ``-d``  
   - **Description:** Sets the embedding dimension size.  

4. Number of Iterations  

   - **Option:** ``--number-of-iterations`` or ``-n``  
   - **Description:** Sets the maximum number of iterations for the embedding process.  

5. Columns  

   - **Option:** ``--columns`` or ``-c``  
   - **Description:** Specifies column names (maximum of 12) with modifiers: ``[transient::, reflexive::, complex::]``.  
   - **Modifiers:**  

     - **transient:** The column is used in the graph creation, but for the etities in this column embedings won't be calculated.

      ::

         Example: There are two columns in our data ``user`` and ``product``, 
         each row stores user id and id of a product user bought. We want to 
         create embeddings of products, but users are what connects products, 
         which are bought together. ``User`` is than transient column used to 
         create graph and compute product embedings. In this case user 
         embeddings won't be created. Transient columns are connected with 
         star expansion of hyperedges. 

     - **complex:** The column contains multiple entities (e.g., products, brands, transactions); in TSV format entities within the same column should be separated by spaces, in JSON format they should nbe stored in an array. 
     
      ::

         Example: There are two columns in data, one column stores user id and 
         other colum stores all products bought by this user. The products 
         column is then a complex column.  

     - **reflexive:** Items in  this column interacts with itself. Each reflexive column will result in the seperate graph and seperate output file. 

      :: 

         Example: There is a column in data storing all products from a one 
         basket. In created graph all each product from a basked is connected 
         with any other product in this basket. The column is connected with 
         clique expansion of hyperedges.  
     
     - **ignore:** The column won't be included in any graph and no output file is created for this field  

   - **Allowed combinations:** ``transient``, ``complex``, ``transient::complex``, ``reflexive::complex``.  

   The picture below present data examples with column configurations and resulting graphs:  

   .. figure:: _static/cleora-columns.png
    :figwidth: 100 %
    :width: 60 %
    :align: center
    :alt: examples use case of column modifiers
 


6. Relation Name  

   - **Option:** ``--relation-name`` or ``-r``  
   - **Description:** Sets the name of the relation for output file name generation.  

7. Prepend Field Name  

   - **Option:** ``--prepend-field-name`` or ``-p``  
   - **Description:** Determines whether to add the field name to the entity identifier in the output.  

8. Log Every N  

   - **Option:** ``--log-every-n`` or ``-l``  
   - **Description:** Logs output every N lines.  

9. In-Memory Embedding Calculation  

   - **Option:** ``--in-memory-embedding-calculation`` or ``-e``  
   - **Description:** Chooses between calculating embeddings in memory or with memory-mapped files. Possible values are ``0``  for calculating embeddings in memory and ``1`` otherwise. (default ``0``)  

10. Output Directory  

    - **Option:** ``--output-dir`` or ``-o``  
    - **Description:** Specifies the output directory for files with generated embeddings.  

11. Output Format 

    - **Option:** ``-f``  
    - **Description:** Sets the format of the output file. Possible formats are ``.txt`` (text file) and ``.npy`` (numpy).  

Examples of Cleora Configuration  
--------------------------------

.. code-block:: bash

    chmod +x cleora
    ./cleora --type tsv \
             --columns="complex::reflexive::a b complex::c" \
             --dimension 128 \
             --number-of-iterations 5 \
             --relation-name=test_relation_name \
             --prepend-field-name 0 \
             file1.tsv file2.tsv

.. note::
   Before the first run, ensure that the Cleora binary file has execute permissions (``chmod +x``). 
