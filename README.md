# Asociační pravidla nad genetickými mutacemi 
Praktická část bakalářské práce na **Vysoké škole ekonomické v Praze**.

Cílem práce je aplikovat metody **Association Rule Mining (ARM)** na data o genetických mutacích chromozomu 21 z projektu **1000 Genomes** (fáze 3).


## Aplikované algoritmy
1. **FP-Growth** 
2. **AMIE 3.5** 


## Struktura repozitáře

```
.
├── explran_chr21.ipynb          # Explorační analýza VCF dat z 1000 Genomes + Stavba RDF grafu         
├── fp-growth.ipynb              # ARM přes FP-Growth (mlxtend)
├── amie.ipynb                   # spuštění AMIE 3.5
├── rdf_graph_final.ttl          # Výsledný RDF graf (Turtle) pro AMIE
├── amie_triples.tsv             # Trojice pro AMIE
├── amie_results_v2.tsv          # Pravidla vygenerovaná AMIE
├── rules_u1_all.csv             # FP-Growth pravidla — varianta U1
├── rules_u2_all.csv             # FP-Growth pravidla — varianta U2
├── rules_u3_all.csv             # FP-Growth pravidla — varianta U3 (nepřiloženo, > 100 MB)
├── igsr_samples.tsv             # Metadata vzorků 1000 Genomes (populace, pohlaví)
├── img_fp-growth/               # Grafy a vizualizace pro FP-Growth
├── img_amie3/                   # Grafy a vizualizace pro AMIE
├── chromozom_21/                # Vstupní VCF soubory (nepřiloženy v repu)
└── data/                        # Předzpracované pickle soubory (nepřiloženy v repu)
```

## Použité technologie

- **Python 3** (Jupyter Notebook)
- `pandas`, `numpy`, `scikit-learn`
- `mlxtend` — implementace FP-Growth
- `pysam` / `cyvcf2` — práce s VCF
- `rdflib` — stavba RDF grafu
- **AMIE 3.5** (Java) — [github.com/lajus/amie](https://github.com/lajus/amie)
- `matplotlib`, `seaborn` — vizualizace

## Vstupní data

Velké zdrojové soubory **nejsou v repozitáři** kvůli omezení velikosti. Lze je stáhnout z níže uvedených zdrojů:

| Soubor | Zdroj |
|---|---|
| `ALL.chr21.phase3_*.vcf.gz` | [1000 Genomes Project, Phase 3](https://www.internationalgenome.org/data) |
| `igsr_samples.tsv` | [IGSR — sample metadata](https://www.internationalgenome.org/data-portal/sample) |
| `whole_genome_SNVs_GRCh37.tsv.gz` (+ `.tbi`) | [CADD v1.6 (GRCh37)](https://cadd.gs.washington.edu/download) |
| `amie3.5.1.jar` | [AMIE — releases](https://github.com/lajus/amie/releases) |

Po stažení je umístit dle struktury výše (VCF do `chromozom_21/`, JAR do kořenu projektu).

## Spuštění

```bash
# 1. Vytvoř virtuální prostředí
python3 -m venv venv
source venv/bin/activate

# 2. Instalace závislostí
pip install -r requirements.txt

# 3. Spuštění notebooků
jupyter notebook
```

Doporučené pořadí spouštění notebooků:

1. `explran_chr21.ipynb` — předzpracování VCF, tvorba transakční matice, stavba RDF grafu
2. `fp-growth.ipynb` — generování pravidel přes FP-Growth
3. `amie.ipynb` —  spuštění AMIE

### Spuštění AMIE samostatně

```bash
java -jar amie3.5.1.jar rdf_graph_final.ttl > amie_results.tsv
```

## Licence a citace

Projekt je součástí kvalifikační práce a slouží k akademickým účelům. Při použití dat citujte primární zdroje.
