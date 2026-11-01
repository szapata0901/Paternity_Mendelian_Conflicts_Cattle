# Mendelian parentage check

A small script I wrote to answer a simple question: *can this animal really be the offspring of this sire?*

Pedigree errors are more common in livestock than most people assume, and they quietly spoil breeding values and mating decisions. I wanted a quick check that works with just the SNP genotypes, without needing a big reference population or allele frequencies. This is that check.

## The idea

If an offspring and a parent carry opposite homozygous genotypes at a SNP, that parent can't have passed the offspring its allele. A few such cases are expected because genotyping is never perfect. Too many means the pairing is wrong. The script counts these conflicts across the autosomes and weighs them against a realistic error level, then gives each candidate one of four calls: **Compatible**, **Doubtful**, **Excluded** or **Indeterminate** (not enough usable SNPs).

You can test several candidate parents at once. It also saves the exact SNPs that conflict, so you can audit a doubtful case instead of trusting a single number.

## Using it

```bash
python mendelian_check.py --raw parentage.raw --offspring ID_OFFSPRING --parent ID_SIRE1 ID_SIRE2
```

It reads a PLINK `.raw` file (`--recode A`), with an optional `.bim` to keep autosomes only. You get a summary CSV per candidate and a second CSV with the conflicting SNPs.

## Worth knowing

It tells you whether a pairing is *compatible*, not how likely it is. When several candidates pass and you need to choose between them, use the likelihood-based version.

Part of the SelectaGen toolkit. The code is private; if you'd like to collaborate or try it on your data, get in touch.
