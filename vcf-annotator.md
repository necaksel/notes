# vcf-annotator
https://github.com/OncoImmunity/vcf-annotator/

python application
uses pydantic for all data structures

input:
A VCF file with variants for a person
like: test_s2957.ensemble_cons.vcf in vfc-annotator
G switched to T at this position

output:
enriched vcf files with RNA reads for each variant and in the specific
format that the [[nnpp]] expects.

as a side effect it runs bam-read-count.
How many reads in the RNA map to this variant.
And we add this to the VCF files.

For each RNA seq:
    find(variant from input variant file)
    increment rna seq read per variant

We use external variant calling tools, we get one VCF file per tool:
- one for germ line variants
- one for somatic variants

[WhatsHap](https://whatshap.readthedocs.io/en/latest/): tool for hasing - which chromosme copy is this variant from. Is it homozygous or
If we have variants that are close together are they on the same chromosome or not.