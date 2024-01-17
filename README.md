# Sigma-Genomics
Project database for storing multiple genes for individuals and querying variants.

## What this database is for
Sigma Genetics is a database designed to store personal and genetic data for **human** individuals. Additionally, this database can handle the results of analyses corresponding to this data. The database is organized with "People" at the highest level of organization who each have a "genome" and associated "analyses". People can be connected in a many-to-many relationship with the analyses. A current limitation of the database is that it can only handle simply-formatted genetic data, so formatting and cleaning will be necessary before anything could be inserted. In a full implementation of this system, users would be able to access their own data online.

![Entity relationship diagram](images/entity_relationship_diagram.png?raw=true "Entity relationship diagram")

## Example queries
The following are examples of ways that we can query the database if we were to try and answer particular questions regarding the information available.

If we were to select out all of the "Male" individuals, we could use:
```
SELECT *
FROM person
WHERE sex = "Male"
```
![Male individuals](images/male_individuals.png?raw=true "Male individuals")

For available gene sequences with nucleotide lengths greater than 8:
```
SELECT *
FROM sequence
WHERE LENGTH(sequence) > 8
```
![Length eight](images/length_eight.png?raw=true "Length eight")

As a more advanced query, we could return the name, sex, and ethnicity for a specific start position ("GRCh38:chr1:0")
```
SELECT DISTINCT first_name, last_name, sex, ethnicity, start_position
FROM person
JOIN genome ON person.genome_id = genome.genome_id
JOIN genome_snps ON genome.genome_id = genome_snps.genome_id
JOIN snp ON genome_snps.snp_id = snp.snp_id
JOIN position ON snp.position_id = position.position_id
WHERE start_position = "GRCh38:chr1:0"
```
![Chosen start position](images/chosen_start_position.png?raw=true "Chosen start position")
