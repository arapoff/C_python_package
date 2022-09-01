
### Background

I would like to make the code I'm working on to be a Python package which is installable via PyPI. 

That is, 

```
pip install secret_package
```

The problem is that the code calls many external libraries and command-line tools. 


How is this usually done?

Here are the tools I am using:

* Samtools: https://github.com/samtools/samtools
* BWA: https://github.com/lh3/bwa
* GATK: https://github.com/broadinstitute/gatk/releases/tag/4.2.6.1
* WhatsHap: https://github.com/whatshap/whatshap

So, for instance, I run via the Python code the following samtools command:

```
samtools index exmaple.bam
samtools faidx example.bam
```

For BWA, I run:

```
bwa index example.fa
```

How do I do this in Python? I use `subprocess`

```
import subprocess

def function_name():
	## index them now
	subprocess.call(['samtools', 'faidx', output_fasta_filename])  
	subprocess.call(['bwa', 'index', output_fasta_filename])  	
	## also need samtools dict
	subprocess.call(['samtools', 'dict', output_fasta_filename, '-o', output_fasta_dict_filename])
```

Here are all of the subprocess commands I use:

* Samtools: 

```
subprocess.call(['samtools', 'faidx', output_fasta_filename])  
```

* BWA: 
```
subprocess.call(['bwa', 'index', output_fasta_filename])  	
```

* GATK

```
gatk_rg = subprocess.call(['gatk', 'AddOrReplaceReadGroups', '--INPUT', output_bam_sorted, '--OUTPUT', output_RG_bam_sorted, '--RGLB', 'lib1', '--RGPL', 'illumina', '--RGPU', 'unit1', '--RGSM', '"CONTIG_ID"'])
```

* WhatsHap

```
subprocess.call(['whatshap', 'polyphase', '--ignore-read-groups', '--ploidy', str(row['estimated_ploidy']), '-o', output_phased_vcf, '--reference={}'.format(row['fasta_files']), nucmer_pair_dfs['HaplotypeCaller_VCFs'], output_bam_sorted])
```

### Task

Create a pip-installable (with support for Mac, Windows, Linux) Python package whereby the above tools (samtools, bwa, gatk, & whatshap) are installed along with the package. I haven't had the time to investigate this. 

### Acceptance criteria 
Share the package 
