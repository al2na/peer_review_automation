# 2ndOpinion Automation Report: Paper peer review

**Execution Date:** 8/11/2026, 11:59:23 PM
**Status:** completed · **Steps Executed:** 15 · **Cloud Calls:** 15

---

## Execution Step Outputs


### Step 1: Extract claims 1 (step)

{"claim1":"A supervised variational autoencoder trained on 118,263 bulk RNA-seq samples across 42 tissues learns a tissue-aware latent representation that is primarily organized by tissue identity and achieves 94.9% balanced accuracy in tissue-of-origin classification using a 121-dimensional latent space.","claim2":"The trained model generalizes to an independent cohort of 734 pediatric tumors (TARGET) unseen during training, achieving 84.6% agreement with the expected tissue of origin.","claim3":"Compared with a bulk RNA-seq foundation model (BulkFormer), the supervised VAE yields higher developmental tissue-origin accuracy on TARGET (84.6% vs 76.8%), while also providing a highly compressed, reconstructive latent representation that enables reconstruction and imputation beyond simple nearest-neighbor baselines, as demonstrated in TARGET and related analyses."}

---

### Step 2: Claim 1 Literature Search (step)

JUDGMENT:
Already established — the core claim has been demonstrated previously.

RATIONALE:
A 2026 bioRxiv preprint reports a supervised VAE trained on ~118k bulk RNA-seq samples across 42 tissues, yielding a 121-dimensional latent space with tissue-of-origin classification at ~94.9% balanced accuracy, supporting a tissue-aware latent representation. Related work (Flexynesis Tissue VAE) documents similar approaches for unified tissue representation across major expression compendia.

KEY PAPERS:
- An atlas-scale generative model for unified representation learning of bulk RNA-seq data. bioRxiv. https://www.biorxiv.org/content/10.1101/2026.06.18.733198v1
- Flexynesis Tissue VAE: RNA model. https://bio.rodeo/models/flexynesis-tissue-vae
- Flexynesis tissue-VAE manuscript — code and reproduction. https://github.com/BIMSBbioinfo/flexynesis_tissue_vae_manuscript
- Atlas Tissue Representation — code and reproduction. https://github.com/BIMSBbioinfo/atlas_tissue_representation

---

### Step 3: claim support (step)

CLAIM:
A supervised variational autoencoder trained on 118,263 bulk RNA-seq samples across 42 tissues learns a tissue-aware latent representation that is primarily organized by tissue identity and achieves 94.9% balanced accuracy in tissue-of-origin classification using a 121-dimensional latent space.

SUPPORTING EVIDENCE:

Experiment/analysis:
Train a supervised variational autoencoder (VAE) with a tissue-classification head on bulk RNA-seq data (118,263 training samples) mapped to 42 tissue categories; input comprised 16,115 genes after filtering; latent space size set to 121 dimensions; encoder outputs mean and log-variance for reparameterization; loss combines MMD regularization, reconstruction, and cross-entropy classification.
System/sample:
Bulk RNA-seq samples assembled from ARCHS4 (ARCHS4 v2.5 bulk-filtered), GTEx v8, and TCGA; final training/test compendium: 146,537 total samples across 42 tissues (118,263 training, 28,274 test). Sources include ARCHS4 (majority), GTEx, and TCGA; gene set: 16,115 genes.
Comparison/control:
Held-out test set composed of 28,274 labeled samples; performance reported against 42 tissue categories. Also compares to baselines in figures (e.g., kNN on raw/reduced features, scGPT zero-shot) to contextualize performance.
Measurement:
Tissue-of-origin classification performance measured as balanced accuracy and weighted F1 score.
Result:
Held-out test achieved 94.9% balanced accuracy and 96.2% weighted F1 across 42 tissue categories.
Relevance to claim:
Direct support for the claim that the supervised VAE yields a tissue-aware latent representation and achieves 94.9% BA in tissue classification using a 121-dimensional latent space.
Source:
Main Results section; Figure 2 and Table 2 (text describing 94.9% BA and 96.2% weighted F1 for the 118K test split). Relevant passages note 118K training, 28,274 test, 16,115 genes, 121 latent dimensions, and the 94.9% BA/96.2% F1. Also described in the Methods with architecture details.

Experiment/analysis:
Visualization and latent-space organization assessment.
System/sample:
Latent embeddings for held-out test samples (n = 28,274) from the 118K compendium.
Comparison/control:
Latent-space visualization colored by tissue and by data source to assess whether tissue identity dominates structure over source effects.
Measurement:
t-SNE visualization (Kobak–Berens protocol) of 121D latent space; source-mixing metrics: kNN source mixing (k=20) and local inverse Simpson index (LISI).
Result:
Latent space is primarily organized by tissue identity; samples cluster by organ system with clear tissue sub-clusters; when colored by data source, ARCHS4/GTEx/TCGA co-cluster within tissue neighborhoods rather than forming source-specific islands. Source effects are secondary (e.g., kNN source mixing = 0.012; LISI ceiling ~3.0 for 118K). Relevance to claim:
Supports the part of the claim stating that tissue identity is the primary organizing axis of the latent space, with source effects secondary.
Source:
Results description around the latent-space structure and Figure 1 (and related text) detailing tissue-driven clustering and modest cross-source mixing.

Experiment/analysis:
Cross-cohort transfer validation on TARGET paediatric cancers.
System/sample:
TARGET paediatric cancer RNA-seq cohort (n = 734 across seven cancer categories); expression aligned to the 16,115 model genes.
Comparison/control:
Model applied to TARGET without having seen TARGET data during training; nearest-neighbor (k=5, Euclidean) classification against 118K reference embeddings; compared against developmental-origin rubric (adult-tissue correlates).
Measurement:
Overall accuracy of tissue-of-origin assignments on TARGET; category-specific mappings discussed.
Result:
Overall accuracy 84.6% (621/734) in assigning expected tissues; specific notes include detailed mappings (e.g., AML mapping to blood/bone marrow/lymphoid at 99%, neuroblastoma to brain 72%, Wilms tumour across intermediate-mesoderm tissues 65%).
Relevance to claim:
Demonstrates that the learned tissue-aware latent representation generalizes to an unseen, developmentally related cohort, supporting the claim that the latent space captures tissue identity in bulk RNA-seq and is transferable to external data.
Source:
TARGET validation results and Figure 4; accompanying text describing per-cancer mappings and overall 84.6% accuracy.

Experiment/analysis:
Model robustness and comparisons to baselines (supporting the value of the 118K supervised VAE as a tissue-aware representation).
System/sample:
Comparison against multiple baselines on the same held-out 118K test split; includes kNN baselines with various feature reductions, and zero-shot scGPT baseline.
Comparison/control:
Direct comparisons to top-kNN baselines (e.g., top-2,000 HVG + kNN; all genes + PCA; HVG + UMAP; etc.) and to BulkFormer (a bulk RNA-seq foundation model), evaluated under the same protocol.
Measurement:
Balanced accuracy on held-out 118K test split; latent-space dimensionality vs accuracy; zero-shot scGPT performance.
Result:
Supervised VAE achieves 94.9% BA, outperforming several baselines (e.g., top-2,000 HVG + kNN around 93.4%); BulkFormer achieves 76.8% on TARGET for developmental tissue-of-origin, while the VAE achieves 84.6% on TARGET (and 94.9% BA on 118K test). This positions the VAE as a strong tissue-aware representation with compact latent space (121D).
Relevance to claim:
Contextualizes and reinforces the claim by showing the superiority of the supervised VAE’s tissue-aware latent representation relative to baselines and a competing bulk foundation model.
Source:
Figure 5 and Figure 6 descriptions; accompanying text discussing baselines and BulkFormer comparison.

OVERALL SUPPORT:
The experiments establish that a supervised VAE trained on a large, multi-source bulk RNA-seq compendium (118,263 training samples across 42 tissues) learns a 121-dimensional latent representation in which tissue identity is the dominant organizing axis. The model achieves 94.9% balanced accuracy on tissue-of-origin classification in held-out data, with robust reconstruction/imputation, and demonstrates transfer to unseen pediatric-tumor cohorts (TARGET) with 84.6% accuracy, outperforming several baselines and BulkFormer in this setting. This combination of architecture, dataset scale and curation, latent-space organization, and transfer performance supports the claim.

Assumptions and notes:
- The claim is supported by the primary reported metrics for the 118K training run: 94.9% BA and 96.2% weighted F1, using a 121-dimensional latent space.
- “Latent space organized by tissue identity” is supported by the described t-SNE visualization and source-mixing metrics indicating tissue-driven structure with minimal source-driven clustering.
- All results are from the manuscript text provided; no external data or citations were introduced.

---

### Step 4: Support needed (step)

- ESSENTIAL 1: Demonstrate that the 121-dimensional latent space encodes tissue identity and that this encoding is the primary organizing signal
  - What to provide: Quantitative evidence that latent features correlate with tissue-of-origin (e.g., mutual information or ANOVA-like effect sizes between latent dimensions and tissue labels) and qualitative/quantitative clustering evidence (e.g., t-SNE/UMAP visuals with clear tissue clusters; silhouette scores by tissue; classification performance using only latent features).
  - Why needed: Shows the claim that the latent representation is tissue-aware and organized by tissue identity, not by non-biological factors.

- ESSENTIAL 2: Establish robust, unbiased assessment of tissue-of-origin classification performance
  - What to provide: A clearly described training/validation protocol (train/validation/test splits with stratification across 42 tissues), cross-validation or multiple random seeds, and report of balanced accuracy on held-out test data at 121-d latent representation. Include baseline comparisons (e.g., using raw input, PCA, or different latent dimensionalities) and batch-effect controls.
  - Why needed: Confirms the reported 94.9% balanced accuracy is reproducible, not due to data leakage, overfitting, or batch artifacts, and that the metric is computed correctly across tissue classes.

- ESSENTIAL 3: Provide ablations/controls showing the role of supervision and the chosen latent dimensionality
  - What to provide: Analyses showing (a) performance when supervision is removed (unsupervised VAE) or when the latent space dimension is varied (e.g., 50, 100, 150) to demonstrate that 121 dimensions are necessary or optimal; (b) comparison to alternative discriminators or simple classifiers trained on the latent space; (c) controls for potential confounders (batch, platform, sample size per tissue) to ensure tissue signal—not technical artifacts—drives performance.
  - Why needed: Establishes that the tissue-aware organization and high accuracy depend on the supervised objective and the chosen latent capacity, supporting causal interpretation of the model’s design choices rather than incidental results.

---

### Step 5: Support needed 2 (step)

Assumptions:
- Claim type: descriptive external validation of a model’s generalization to an independent pediatric tumor cohort.
- Ground truth: tissue of origin labels in TARGET are assumed accurate.

 Essential 1 — Independent validation dataset and proper data handling
- What to provide: Full description of the independent TARGET cohort used for validation (n=734), including how samples were selected, preprocessing, and ensuring no overlap/leakage with training data (no shared patients, samples, or preprocessing steps that would leak information).
- Why needed: Confirms genuine external generalization and rules out data leakage or familiar-tissue bias driving the 84.6% score.

 Essential 2 — Transparent performance metrics with uncertainty, stratified by tissue type
- What to provide: Overall accuracy (84.6%) plus per-tissue accuracy, confusion matrix, and 95% confidence intervals or bootstrapped CIs for the metric reported. Include calibration if applicable.
- Why needed: Demonstrates robustness across tissue types and reveals potential tissue-specific limitations; avoids overinterpretation of a single aggregate number.

 Essential 3 — Validation controls to rule out confounders and alternative explanations
- What to provide: Analyses addressing potential confounders (e.g., batch effects, platform differences, sample processing) and a null/negative control (e.g., random labels) to ensure performance is not due to artifacts. Include a baseline comparison to a simple classifier or prior method.
- Why needed: Ensures the observed generalization is attributable to the model’s true predictive signal rather than artifacts or chance.

---

### Step 6: claim 1 support reasoning (step)

CLAIM:
A supervised variational autoencoder trained on 118,263 bulk RNA-seq samples across 42 tissues learns a tissue-aware latent representation that is primarily organized by tissue identity and achieves 94.9% balanced accuracy in tissue-of-origin classification using a 121-dimensional latent space.

VERDICT:
Partially supported

REASONING:
The manuscript provides strong support for the 94.9% balanced accuracy in tissue-of-origin classification using a 121-dimensional latent space, and shows that tissue identity dominates the latent structure via qualitative t-SNE visualization and low source-mixing metrics. However, it lacks explicit quantitative evidence proving that the latent dimensions encode tissue identity as the primary organizing signal (e.g., direct correlations or mutual information between latent features and tissue labels, or quantitative clustering metrics by tissue). Essential ablation controls (supervised vs unsupervised VAE and latent-dimension sensitivity) are also not shown, limiting the causal inference about the role of supervision and the chosen 121 dimensions. Given these gaps, the claim about the latent space being primarily organized by tissue identity is supported qualitatively but not with fully quantified evidence.

SUPPORTED VERSION:
A supervised VAE trained on a large bulk RNA-seq compendium across 42 tissues achieves 94.9% balanced accuracy in tissue-of-origin classification using a 121-dimensional latent space, with evidence suggesting tissue identity largely drives the latent structure (visual clustering and low source-mixing metrics).

---

### Step 7: claim support 2 (step)

CLAIM:
The trained model generalizes to an independent cohort of 734 pediatric tumors (TARGET) unseen during training, achieving 84.6% agreement with the expected tissue of origin.

SUPPORTING EVIDENCE:

Experiment/analysis:
Model validation on an independent pediatric cancer cohort (TARGET) to assess transfer to unseen data.

System/sample:
TARGET pediatric tumor RNA-seq samples (n = 734) across seven cancer types; expression data aligned to the 16,115 model genes.

Comparison/control:
Samples were not part of the training set (unseen); they were embedded with the trained Standard VAE and classified by k-nearest-neighbour (k = 5, Euclidean) against the 118K reference embeddings. Expected tissues were defined by developmental biology (adult tissues corresponding to developmental origins).

Measurement:
Agreement between model-predicted tissue of origin and the expected developmental tissue origin; overall accuracy reported as percentage of samples matching the developmental expectation.

Result:
Overall accuracy 84.6% (621/734). Breakdown for key categories:
- Acute Myeloid Leukemia: 99% mapping to blood/bone marrow
- Acute Lymphoblastic Leukemia: 96% mapping to blood/lymphoid
- AML Induction Failure: 100%
- Neuroblastoma: 72% mapping to brain
- Wilms Tumor: 65% mapping to intermediate-mesoderm tissues
- Rhabdoid Tumor: 100%
- Clear Cell Sarcoma of the Kidney: 0% (maps to no expected tissue)

Relevance to claim:
Demonstrates the model’s ability to generalize to an entirely independent, unseen pediatric cohort and recover tissue-of-origin signals that align with developmental biology, supporting claim of cross-cohort generalization.

Source:
Main manuscript results describing TARGET validation and 84.6% accuracy (TARGET overall accuracy: 84.6% = 621/734). Refer to the TARGET validation section and Figure 4, as well as associated figure/table text (TARGET mapping details and category breakdown).

---

### Step 8: Claim 2 Literature Search (step)

JUDGMENT:
Insufficient literature to judge

RATIONALE:
Current searches (PubMed and web) found no directly relevant studies testing generalization of pediatric tissue-of-origin classifiers to an independent cohort like TARGET (n=734) with reported 84.6% agreement. Without such evidence, the novelty/replication status cannot be assessed.

KEY PAPERS:
None found.

---

### Step 9: Support needed 3 (step)

Here are the 3 most important evidentiary requirements to convincingly support the claim, tailored to its descriptive/comparative nature.

- ESSENTIAL 1: Independent, statistically validated benchmark on TARGET for tissue-origin accuracy
  - What to provide: A held-out TARGET test set evaluation comparing BulkFormer and the supervised VAE, reporting overall accuracy (84.6% vs 76.8%), per-tissue accuracy, confusion matrices, and calibration. Include statistical significance (e.g., bootstrap CIs or permutation tests, p-values) and a pre-registered or clearly documented data split that avoids leakage.
  - Why needed: Demonstrates that the accuracy gain is real and not due to dataset leakage, overfitting, or chance, and shows how performance varies across tissue origins.

- ESSENTIAL 2: Quantitative evidence of latent-space compression and reconstructive/imputation capability
  - What to provide: Metrics for latent representation quality and reconstruction/imputation, such as MSE/R2 for expression reconstruction across TARGET (and relevant related analyses), plus comparisons to nearest-neighbor baselines using identical inputs and latent dimensionality. Include qualitative examples (e.g., reconstructed profiles or imputed values) and demonstrate performance beyond NN baselines on multiple tissues.
  - Why needed: Substantiates the claim of a highly compressed, reconstructive latent representation and shows it provides value beyond simple nearest-neighbor approaches.

- ESSENTIAL 3: Robustness and generalizability with ablations and cross-dataset validation
  - What to provide: (a) Ablation showing the contribution of supervision to tissue-origin accuracy (e.g., removing supervision degrades accuracy); (b) validation on related analyses or external datasets (not TARGET) to demonstrate generalizability; (c) controls for model capacity and preprocessing (equal latent dimensionality, fixed hyperparameters) to ensure fair comparison.
  - Why needed: Ensures the observed advantage is due to the supervised VAE design rather than artifacts, and shows the approach generalizes beyond the specific TARGET setting.

---

### Step 10: claim support 3 (step)

CLAIM:
Compared with a bulk RNA-seq foundation model (BulkFormer), the supervised VAE yields higher developmental tissue-origin accuracy on TARGET (84.6% vs 76.8%), while also providing a highly compressed, reconstructive latent representation that enables reconstruction and imputation beyond simple nearest-neighbor baselines, as demonstrated in TARGET and related analyses.

SUPPORTING EVIDENCE:

Experiment/analysis:
Direct comparison of developmental-tissue-origin accuracy on the TARGET pediatric cancer cohort using embeddings from the supervised VAE vs BulkFormer-93M.
System/sample:
TARGET paediatric cancer RNA-seq cohort (n = 734 samples across seven cancer types).
Comparison/control:
Supervised VAE (the model developed in this work) vs BulkFormer-93M (out-of-the-box BulkFormer baseline). Both models were embedded and evaluated with the same kNN classifier (k = 5, Euclidean) against the same held-out reference and rubric.
Measurement:
Overall developmental tissue-of-origin accuracy; per-category distribution illustrated for Wilms tumor.
Result:
Supervised VAE achieved 84.6% accuracy (621/734); BulkFormer-93M achieved 76.8% accuracy. In Wilms tumor specifically, the VAE assigned 86 samples to intermediate-mesoderm tissues (correct) and 44 to brain (incorrect), whereas BulkFormer assigned 12 to intermediate-mesoderm, 98 to brain (incorrect), and 22 to other tissues.
Relevance to claim:
Directly supports the claim that the supervised VAE outperforms BulkFormer on developmental tissue-origin accuracy in TARGET, including improved handling of a representative challenging cancer (Wilms tumor).
Source:
Figure 6a–b; Figure 6 caption (TARGET comparison), and related text describing 84.6% vs 76.8% accuracy and Wilms-tumor mappings.

Experiment/analysis:
Comparison of latent representations in terms of reconstruction/imputation capabilities and baseline performance.
System/sample:
Bulk RNA-seq compendium used for training (118K) and held-out test data (n = 28,274); baselines include kNN on raw expression, HVG-based reductions, and zero-shot scGPT.
Comparison/control:
Standard VAE vs Denoising VAE (20% gene masking) to test robustness of reconstruction/imputation; plus comparison to multiple kNN baselines and a zero-shot single-cell foundation model (scGPT).
Measurement:
Per-gene reconstruction Spearman ρ, per-sample reconstruction Spearman ρ, and imputation performance at 30–30% masking; accuracy vs baselines (Figure 5).
Result:
Reconstruction and imputation performance were nearly identical between Standard and Denoising variants (per-gene ρ ~0.935; per-sample ρ ~0.829–0.830; imputation at 30% masking ~0.874–0.879). The supervised VAE achieved the highest tissue-classification accuracy (94.9%) in this comparison, outperforming the baselines (e.g., scGPT ~61.0%; HVG-based baselines ~84.2–93.4% depending on method).
Relevance to claim:
Supports the part of the claim that the latent representation is both highly compressed and capable of reconstruction/imputation beyond nearest-neighbor baselines, illustrating practical utility of the learned latent space for reconstruction tasks.
Source:
Figure 5 (and related text describing per-gene/single-sample reconstruction, denoising vs standard, and baseline comparisons).

Experiment/analysis:
Qualitative demonstration that latent space encodes tissue identity while being robust to source heterogeneity.
System/sample:
Held-out bulk RNA-seq samples (n = 28,274) projected into a 121-dimensional latent space and visualized by t-SNE (Kobak–Berens protocol); data sources include ARCHS4, GTEx, and TCGA.
Comparison/control:
Coloring by tissue category vs coloring by data source to assess organizing axes.
Measurement:
Latent-space structure showing tissue-driven clustering and cross-source mixing metrics (LISI and kNN source mixing).
Result:
Latent space is primarily organized by tissue identity; source effects are secondary and detectable but do not override tissue clustering.
Relevance to claim:
Supports the assertion that the model learns a tissue-aware representation that generalizes across studies, a key aspect of the claim about a high-quality latent representation suitable for reconstruction and cross-study transfer.
Source:
Figure 1a–c descriptions and accompanying text.

Overall SUPPORT: 
The evidence shows that the supervised VAE outperforms BulkFormer on developmental tissue-origin accuracy in TARGET (84.6% vs 76.8%), and that the model provides a compact, reconstructive latent representation whose usefulness for reconstruction/imputation surpasses simple NN baselines. Additional analyses demonstrate tissue-driven latent organization and cross-study transferability, supporting the claim that the model yields a compressed, reconstructive, tissue-aware representation with practical transfer capabilities.

---

### Step 11: Claim 3 Literature Search (step)

JUDGMENT:
Insufficient literature to judge

RATIONALE:
No PubMed hits or credible web sources directly comparing BulkFormer with a supervised VAE on TARGET tissue-origin accuracy or demonstrating reconstruction/imputation beyond nearest-neighbor baselines. Related work on RNA-seq VAEs exists broadly, but not specifically validating the exact claim or dataset combination.

KEY PAPERS:
None retrieved directly supporting or refuting the core claim. (No directly relevant studies found in PubMed or high-confidence web sources.)

Note: If you want, I can broaden the search to include general VAEs for RNA-seq and imputation approaches to assemble context around the claim.

---

### Step 12: claim 2 support reasoning  (step)

VERDICT:
Partially supported

REASONING:
The evidence shows the model was evaluated on an independent TARGET cohort (n=734) with 84.6% overall agreement to the developmental/expected tissue origin, indicating some generalization to unseen pediatric data. However, essential elements are missing: (1) full description of cohort selection, preprocessing, and avoidance of data leakage; (2) per-tissue accuracy, confusion matrix, and confidence intervals to gauge robustness and uncertainty; (3) analyses addressing confounders (batch effects, platform differences) and inclusion of null controls or baseline classifiers. Without these, the claim of robust external generalization remains incompletely supported.

SUPPORTED VERSION:
The model generalizes to an independent TARGET pediatric cohort (n=734) with 84.6% overall agreement between predicted tissue of origin and developmental-origin expectations, but further validation details (uncertainty, per-tissue performance, and control analyses) are needed for full endorsement.

---

### Step 13: claim 3 support reasoning  (step)

VERDICT:
Partially supported

REASONING:
- Essential 1 (TARGET benchmark with stats): The manuscript reports higher accuracy for the supervised VAE (84.6%) vs BulkFormer (76.8%) on TARGET, but there is no presentation of statistical validation (e.g., confidence intervals, p-values) or a preregistered data split explicitly preventing leakage. Without independent significance testing and leakage control, the claim that the improvement is robust remains insufficiently demonstrated.
- Essential 2 (latent-space compression and reconstruction/imputation): There is quantitative evidence that the latent space is compact and supports reconstruction/imputation beyond nearest-neighbor baselines (gene-wise and sample-wise Spearman correlations, masking-imputation results), and qualitative demonstrations. This convincingly supports the claim of a highly compressed, reconstructive latent representation.
- Essential 3 (robustness and generalizability with ablations and cross-dataset validation): The manuscript includes ablation-type comparisons (Standard vs Denoising variants) and cross-dataset/latent-space analyses (t-SNE across ARCHS4/GTEx/TCGA) to argue robustness and generalizability. However, explicit ablations showing supervision-specific contributions to tissue-origin accuracy (e.g., removing supervision degrades accuracy) and controlled, fair comparisons (equalize capacity, preprocessing) are not fully detailed. The cross-dataset evidence helps, but the controls for model capacity/preprocessing could be stronger.

SUPPORTED VERSION:
Original claim is adequately supported for the qualitative idea that the supervised VAE outperforms BulkFormer on TARGET tissue-origin accuracy and yields a compact, reconstructive latent representation with evidence of cross-study transfer. However, the strongest, independent statistical validation on TARGET and explicit ablations for supervision-driven gains are not fully demonstrated. A stronger, preregistered TARGET benchmark with stat tests would elevate the claim to fully supported.

---

### Step 14: final synthesis (Terminal Output)

MAJOR POINTS

1) Insufficient quantitative evidence that tissue identity is the primary organizing signal in the latent space
- Why it matters: The claim hinges on the latent representation being “primarily organized by tissue identity.” Current support relies on qualitative visuals (t-SNE) and low source-mixing metrics without direct, quantitative linkage between latent features and tissue labels (e.g., correlations, mutual information, or clustering metrics by tissue).
- What to address: Provide explicit quantitative analyses showing that latent dimensions correlate with tissue labels (e.g., compute MI between each latent dimension and tissue category, / or perform supervised clustering metrics, or canonical correlation with tissue labels). Include ablation data to show how removing supervision or reducing latent dimensionality affects tissue-specific structure.
- Concrete suggestions: report per-dimension correlations with tissue labels, MI scores, and tissue-wise clustering metrics (e.g., ARI/NMI). Run an ablation: train an identical model with unsupervised VAE and compare tissue-label alignment to the supervised model.

2) Incomplete, under-detailed external-generalization evidence to TARGET cohort
- Why it matters: The claim of generalization to an independent pediatric cohort (TARGET, n=734) rests on 84.6% agreement but lacks crucial methodological and statistical details that determine robustness (cohort selection, preprocessing, leakage control, per-tissue performance, uncertainty estimates, batch effects).
- What to address: Provide a complete description of data processing, split strategy to avoid leakage, and full performance metrics with uncertainty. Include per-tissue accuracies, confusion matrices, and confidence intervals; assess confounders (batch, platform) and present null controls or baseline comparisons.
- Concrete suggestions: pre-register analysis plan or provide a preregistered-like breakdown; report 95% CIs for overall and per-tissue accuracy; show confusion matrices; include a baseline classifier (e.g., random, majority vote, or unsupervised-bias controls) to contextualize 84.6% figure.

3) Lack of explicit demonstration that supervision and 121 latent-dimension choice causally drive improved tissue-origin performance
- Why it matters: The claim implies supervision and the chosen latent dimensionality are critical. Without direct ablations isolating the contribution of supervision and the 121-dim bottleneck, attribution remains speculative.
- What to address: Provide controlled ablations isolating the effects of supervision and latent dimensionality on tissue-origin accuracy, using identical architectures and preprocessing where possible.
- Concrete suggestions: (a) train an unsupervised VAE with the same capacity and compare tissue-origin accuracy and latent-space organization; (b) train with varying latent dimensions (e.g., 64, 128, 256) to test stability of tissue-specific structure and performance; (c) ensure capacity/effective sample size is matched when comparing to BulkFormer.

MINOR POINTS

- Reporting clarity: Provide clear, standardized metrics (per-tissue accuracy, overall accuracy, F1, confusion matrices) and specify statistical tests used for comparisons.
- Reproducibility: Include availability of code, data processing steps, and random seeds or a fixed train/validation/test split protocol to enable replication.
- Terminology and scope: Clarify what is meant by “primary organizing signal” and present precise operational definitions (e.g., thresholds used for low source-mixing, criteria for tissue dominance in latent structure).
- Contextualization: Briefly discuss potential confounders (e.g., tissue mixture, sample quality, developmental stage) that could influence latent organization and generalization, and how they were mitigated.

---

