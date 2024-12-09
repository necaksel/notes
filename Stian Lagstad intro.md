# Stian Lågstad intro
[[Stian Lagstad]]

## [[2024-12-04]]
Myself:
- Started in december 2022
- [[Fredrik Larsen]] (engineer, on parental leave until january)
- [[Runar Furenes]] (engineer in [[ID]], quit a while ago)

The previous engineers went out:
- [[Harald Kirkerød]]
- [[Stefan Kjartansson]]

### The Personalized Cancer Vaccine (PCV) team:
Software in production (in clinical trials):
- [[ngs-pipeline]] (the "upstream" bioinformatics pipeline, written in nextflow): https://github.com/OncoImmunity/ngs-pipelines
	- From sequencing data (fastq files) -> variants (gene fusions, splice variants, "normal variants")
- [[NIP]]/[[prediction-runner]] (the "downstream" prediction pipeline, written in prefect): https://github.com/OncoImmunity/prediction-runner
	- From variants to candidate epitopes / a vaccine design
- [[NNPP]] (the packer+ansible repository that creates a virtual machine image with the above included): https://github.com/OncoImmunity/nnpp
	- NNPP: NEC Neoantigen Prediction Pipeline
	- We ship this VM image as our product, to our colleagues in the NEC Japan [[AIDD]] (Artificial Drug Development) group.

[[WES]] - whole exome sequencing
[[WGS]] - whole genome sequencing

[[Brandon Malone]] - Had the main responsibility of this WGS project.

Software in production in the future:
- [[nnpp-wgs]] (the "new pipeline", written entirely in nextflow): https://github.com/OncoImmunity/nnpp-wgs
	- Longer-term this should replace the two "separate" components we have in production today
	- Short-term it's only for the WGS project

Input data to our pipelines:
- 3 things from the patient: dna-tumor, dna-normal, rna-tumor
- A big set of reference data files

The team and its composition
- [[Hugues Fontenelle]] - team lead
- ?[[Susanne Tande]]? - role unclear, currently on maternal leave until january
Bioinformaticians
- [[Angelina Sverchkova]]
- [[Natalia Mikheecheva]]
- [[Per Brattås]] (50% now, shared with [[ID]])
- [[Sumana Kalyanasundaram]]
Engineers
- [[Erlend Fauchald]]
- [[Fredrik Larsen]] (paternal leave until january)
- [[Moritz von Stetten]]
- [[Stian Lagstad]] (consultant, on paternal leave from january onwards)
- [[Trym Bremnes]]

#### The current work
On [[nnpp-wgs]]:
- [[Moritz von Stetten]]
- [[Stian Lagstad]]
- Some help from bioinformaticians when needed: [[Natalia Mikheecheva]], [[Sumana Kalyanasundaram]]

On benchmarking of our variant calling pipeline:
- [[Natalia Mikheecheva]], [[Sumana Kalyanasundaram]], [[Angelina Sverchkova]] working on this
- Motivation: Provide some regressions tests for ourselves, and also to support the business development side of the company - to get NOI into the door of "big pharma" companies. Remember: The overall goal of the company now is to get a deal with big pharma.

Follow-up on clinical trials:
- all bioinformaticians, [[Hugues Fontenelle]], maybe others where needed
- Quality control of the run on new patients

Div other projects (mostly bioinformaticians):
- "fresh frozen" or "FFPE"
- "dark antigens" / splicing / gene fusions

#### Some history
Previously the PCV team was split in two. We had the "bioinf team" and the "NIP team".
NIP stands for NEC Immune Profiler (this is the [[prediction-runner]])

The bioinf team:
- [[Hugues Fontenelle]] - team lead
- all the bioinformaticians mentioned above
- [[Stian Lagstad]]

The NIP team:
- [[Susanne Tande]] - team lead
- [[Fredrik Larsen]]
- Some people from the data science team ([[Elena Volkova]], [[Ghazal Azadi]], others)

There was no real point in having two teams, managing two different parts of the one product (what we actually use in production). It just lead to overhead, the need to sync, misunderstandings, etc.
I argued pretty much from day one that these two teams should be merged into a single team, and now it has been done.

#### Why Nextflow?
What do we need in an orchestrator?
1. It should assemble "lego bricks" (i.e. Docker containers, Singularity containers, or similar). What we want to do is to stitch together applications in a directed acyclic graph of task dependencies.
2. It should work with multiple runtime environments (e.g. Kubernetes, Google/AWS batch, locally on a single machine, etc.)
3. It should support caching/resumability
4. It should be possible to define what resources (cpu, memory, disk size, etc.) each task in the graph needs

"The great orchestrator war of 2024": https://neconcoimmunity.atlassian.net/wiki/spaces/OP/pages/1367605350/Comparison+of+workflow+systems+orchestrators

Some people wanted [[prefect]] to be used, but [[prefect]] is not made for the above tasks. The choice landed on [[nextflow]], which has the right level of abstraction and supports all the above.

Why do I bring up this at all? Because maybe [[nextflow]] would be a better choice for the [[indit]] pipeline also :) 

### "Engineering/operations team"
Not really a team, but the software engineers in the company meet every couple of weeks with our IT sysadmin [[Stephane Beyls]].

Members
- [[Aksel Lenes]]
- [[Elena Volkova]]
- [[Fredrik Larsen]] (paternal leave)
- [[Hugues Fontenelle]]
- [[Maria Slanova]] (on maternal leave)
- [[Moritz von Stetten]]
- [[Stian Lagstad]]
- [[Trym Bremnes]]

Responsibilities:
- Make sure our various teams have a good starting point for projects, with our [[Cookiecutter]] templates:
	- https://github.com/OncoImmunity/cookiecutter-pyproject
	- https://github.com/OncoImmunity/cookiecutter-pylibrary
- Spread good practices, do training sessions (such as the Cursor demo/workshop)
- Make sure that our fleet of development machines are up and healthy (mostly on [[Stephane Beyls]], although he needs help from engineers)
- Make sure that the office wifi, printer, it onboarding and such things happen ([[Stephane Beyls]])


## Keeps notes in obsidian
Notes in obsidian:
- One note per person
- One note per day.
- Meetings link back to the day in the header [2024-12-04]

Linking to all the things
folk kunne ikke
ngs+pipeline burde vært et produkt.

nnpp is what we deliver to the AIDD group
wgs-nnpp was two teams

covid_mutant


### PCV work
[[WES]] Whole exome sequencing i pipelinen nå. NNPP-WES
[[WGS]] er et nytt prosjekt.
shared variants accross cancer patients 
NEC + google i japan
[[WGS]] should take over for ngs-pipeline NNPP

Brandon started a new pipeline for [[WGS]]. [[WGS]] is hard to change

On-going work

Patient handling
- tumor biopsy
    - WES
    - estimate purity
    - order new biopsy if it is shit
- blood biopsy
    - dna normal
- rna tumor

tumor sample will contain many things, healthy tissue, etc
cancer purity matters We estimate it in two ways.

fresh frozen vs FFPE
fresh frozen preserves the RNA better.

### Nextflow beats prefect
Nextflow does what indit does. Better.
Spreading stuff over docker images is hard in prefect.
Resumability is hard. Caching is hard you need to do it yourself.

prefect is not made for this.

indit run --google-batch

nextflow would be better. Saved compute and human time.
With google batch.

## Tension with QMS
- Stephane: sysadmin that can handle things. apply for access to install something. no sudo access. Grammarly burde vi ikke ha. Sender data om en pasient. His incentive is to comply with laws.

Stian does not ask for these things.
Pinalee conflict. If we do everything she wants to do. Then we'll drown in 
complicance work. Pushes Saverio on this.
Pinalee wants to do too much. Point explode in to too much work.

FDA and EMA needs our approval.
Vipps and google are much stricter and they move fast. They get a lot done.
Fleet management, pings home all the time to update about what is there.
Deep insight. Pings home.
Apply for production, everything logs.

What is sensitive data in different tasks.

Hemmelighetshold. Hold deg til offentlige ting og pressemeldinger.
Det vi finner i posters.
De opplever at konkurenter tries to keep this secret and then you
are asked for this. Recruiters and hiring.
We're far ahead.

Kaidre talk to him. Get the presentation from Kaidre. This is what we're best in the world on.
Nykode.

Close down machines for Tailscale.
Pair program to do work faster.
Resistance to pair program.
People not sharing as much as usual. Due to how people work. Workshops 
Runar was the only one caring about developer stuff. 

https://www.amazon.com/Gods-Debris-Experiment-Scott-Adams/dp/0740747878
[[books]]

### Questions
- access to hetzner : Ask for access for hetzner. Configure a machine. Restart things. Is all good.
- mono-repo vs cookicutter pluss modules in docker images

Speed of change, speed of model updates.
Hva er målet som du tenker på det. Tjene penger. Inngå deals med big pharma. Patentere vaksiner. Trenger benchmarking av at vår tech er bra.
- Hva er styrken?
- binding modeller?

- Mistet founderne hva gjorde det.


- Obsidian ntes are they flat? Tags?
How do you work day to day? Up for pair programming a few hours one day in december
to get a sense for what tools you run and use?