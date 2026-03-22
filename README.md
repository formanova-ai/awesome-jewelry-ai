# Awesome Jewelry AI [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of resources for AI-powered jewelry imagery. It covers research, open-source models, datasets, evaluation tools, commercial platforms, and community references.

Maintained by [FormaNova](https://formanova.ai), the AI photography platform built exclusively for jewelry.

Contributions welcome. Please read the [contributing guidelines](#contributing) before submitting a pull request.

---

## Contents

- [Foundational Research Papers](#foundational-research-papers)
  - [Jewelry-Specific AI](#jewelry-specific-ai)
  - [Generalist Text-to-Image Foundations](#generalist-text-to-image-foundations)
- [Open-Source Models and Implementations](#open-source-models-and-implementations)
- [Datasets](#datasets)
  - [Jewelry-Specific](#jewelry-specific)
  - [RareSense Open Datasets - HuggingFace](#raresense-open-datasets--huggingface)
  - [Gemstone and Mineral](#gemstone-and-mineral)
  - [Reflective and Metallic Objects](#reflective-and-metallic-objects)
  - [Virtual Try-On Reference](#virtual-try-on-reference)
- [Evaluation Metrics and Tools](#evaluation-metrics-and-tools)
- [Production Tools](#production-tools)
  - [Jewelry-Specialized AI Platforms](#jewelry-specialized-ai-platforms)
  - [General Product Photography with Jewelry Support](#general-product-photography-with-jewelry-support)
  - [Virtual Try-On Platforms](#virtual-try-on-platforms)
  - [Managed Services and Agencies](#managed-services-and-agencies)
  - [Generalist Text-to-Image Generators](#generalist-text-to-image-generators)
- [Tutorials and Technical Guides](#tutorials-and-technical-guides)
- [Industry Context](#industry-context)
- [Communities](#communities)
- [Contributing](#contributing)

---

## Foundational Research Papers

### Jewelry-Specific AI

**[DreamSalon: A Staged Diffusion Framework for Preserving Identity-Context in Editable Image Generation](https://openaccess.thecvf.com/content/CVPR2024/papers/Lin_DreamSalon_A_Staged_Diffusion_Framework_for_Preserving_Identity-Context_in_Editable_CVPR_2024_paper.pdf)**
*CVPR 2024*
A staged diffusion framework that preserves fine identity details during image editing. Directly relevant to jewelry try-on scenarios where the wearer's identity and the jewelry's fine geometry must both survive the generation process.

**[ID-Booth: Identity-Consistent Face Generation with Diffusion Models](https://arxiv.org/abs/2504.07392)**
*arXiv 2024*
A diffusion-based framework for generating diverse images while maintaining consistent identity representation. Achieves Fréchet Distance of 1159.54 vs. 1371.13 for DreamBooth. Applicable to virtual try-on systems requiring consistent product rendering across model images.

**[LD-BFR: Vector-Quantization-Based Face Restoration Model](https://dl.acm.org/doi/abs/10.1145/3664647.3680853)**
*ACM 2024*
Demonstrates that the approach preserves fine details like earrings and jewelry that GAN-based methods typically destroy - validating that jewelry poses a specific, documented challenge for restoration models.

**[Catch Missing Details: Image Reconstruction with Frequency-Augmented Variational Autoencoder](https://openaccess.thecvf.com/content/CVPR2023/papers/Lin_Catch_Missing_Details_Image_Reconstruction_With_Frequency_Augmented_Variational_Autoencoder_CVPR_2023_paper.pdf)**
*CVPR 2023*
Addresses quality degradation in VQ-VAE reconstruction - directly relevant to why standard latent diffusion models destroy high-frequency jewelry details (facet edges, prong geometry, engraving) during generation. Essential reading for understanding the core technical problem.

**[RODD: Towards Reflected Object Detection - A Benchmark](https://arxiv.org/html/2407.05575v1)**
*arXiv 2024*
First benchmark for detecting reflected objects in AI models. Contains 21,059 images across 10 categories. Critical for jewelry AI: metal surfaces create complex reflection patterns that confuse standard object detection and segmentation pipelines.

**[SAM Meets Glass: Segment Anything Model Performance on Transparent and Reflective Objects](https://arxiv.org/pdf/2305.00278)**
*arXiv 2023*
Documents that SAM achieves only 48.47% IoU on glass/reflective objects vs. 88.16% for specialized methods. Direct evidence that standard segmentation pipelines fail on the reflective metal and gemstone surfaces that define jewelry.

**[Automatic Identification and Description of Jewelry Through Neural Networks](https://arxiv.org/pdf/2509.00661)**
*arXiv 2025*
VGG-16 + GRU encoder-decoder achieving 93.45% classification accuracy across 4 jewelry categories (necklaces, rings, earrings, bracelets) and generating multi-level descriptions. Dataset: 5,374 images from Spanish jewelry stores.

**[Generative AI in Product Photography: Human-Directed Transfer-based Visual Workflows](https://www.researchgate.net/publication/401881759_Generative_AI_in_Product_Photography_Human-Directed_Transfer-based_Visual_Workflows)**
*ResearchGate 2024*
Examines how generative AI has entered commercial visual production and what human-directed workflows are necessary for professional-grade outputs. Useful framework for understanding where automation ends and oversight begins.

**[Generative Artificial Intelligence as a Tool for Jewelry Design](https://www.gia.edu/gems-gemology/fall-2024-artificial-intelligence-in-jewelry-design)**
*GIA Gems & Gemology, Fall 2024*
Gemological Institute of America evaluation of generative AI programs (Midjourney, DALL-E, and others) applied to jewelry design. Addresses both the creative potential and documented failure modes, including hallucinated compositions and ethical/IP concerns.

---

### Generalist Text-to-Image Foundations

Understanding generalist models is prerequisite knowledge for jewelry AI: their architectural choices explain *why* they fail at product fidelity, which is the core problem jewelry-specialized systems exist to solve.

**[High-Resolution Image Synthesis with Latent Diffusion Models](https://arxiv.org/abs/2112.10752)**
*Rombach et al. - Heidelberg University - CVPR 2022*
The foundational paper for Stable Diffusion. Introduces the VAE compression stage that is the primary source of fine-detail destruction in diffusion-based generation. At f=8 compression, high-frequency information - facet edges, prong geometry, engraving - is systematically eliminated before the diffusion process even begins. Essential reading for understanding jewelry AI's core technical constraint.
GitHub: [CompVis/latent-diffusion](https://github.com/CompVis/latent-diffusion) - 13.9k stars - MIT License

**[Improving Image Generation with Better Captions (DALL-E 3)](https://cdn.openai.com/papers/dall-e-3.pdf)**
*OpenAI Technical Report*
DALL-E 3's technical report focuses on prompt adherence via descriptive caption training. Notably silent on object-level fidelity, i.e. the report does not address whether the model can preserve specific product characteristics from a reference image, which is by design: DALL-E 3 is a text-to-image generator, not a reference-guided fidelity system.

**[Imagen: Text-to-Image Diffusion Models with Deep Language Understanding](https://imagen.research.google/)**
*Google Research*
Google's text-to-image model emphasizing photorealism and language understanding. Design priorities favor creative generation; product-level detail preservation from a reference image is not a documented capability or design goal.

**[Imagen 2 Technical Documentation](https://blog.google/innovation-and-ai/products/google-imagen-2/)**
*Google DeepMind*
Imagen 2 updates on Vertex AI. Improved photorealism, but reference-guided product preservation remains absent from documented capabilities.

**[Demystifying Flux Architecture](https://arxiv.org/html/2507.09595v1)**
*arXiv 2025*
Comprehensive reverse-engineering analysis of Black Forest Labs' Flux architecture. Key finding: Flux uses 16 latent channels (vs. 4 in standard LDM) and adversarial training, providing meaningfully better detail retention than prior diffusion models. Flux.1[schnell] is Apache 2.0 licensed and commercially usable.

| Flux Variant | Use Case | License |
|---|---|---|
| FLUX.1[pro] | Highest performance | API-only, commercial |
| FLUX.1[dev] | Open-weight | Non-commercial |
| FLUX.1[schnell] | Speed-optimized | Apache 2.0 |

**Midjourney**
No formal paper published. Architecture is believed to be diffusion-based with proprietary enhancements. Best available documentation:
- [Midjourney Documentation](https://docs.midjourney.com/) - official usage reference
- Known limitations for product use: no reference image guidance, generates new jewelry rather than preserving the reference piece, style optimization favors artistic interpretation over product accuracy.

**[Gemini Image Generation (Imagen 3)](https://ai.google.dev/gemini-api/docs/image-generation)**
*Google AI Developer Documentation*
Gemini's native image generation via the Gemini API and Google AI Studio. Includes SynthID digital watermarking. Designed for conversational image generation and editing; not architected for reference-guided product fidelity.

---

## Open-Source Models and Implementations

### ControlNet

**[lllyasviel/ControlNet](https://github.com/lllyasviel/ControlNet)**
*ICCV 2023 - Apache 2.0 - 31k+ stars*
Adds conditional control to text-to-image diffusion models via extra input conditions. The Depth and Normal map ControlNets are most relevant for jewelry. They can preserve the 3D geometry of rings, bracelets, and necklaces during scene generation. ControlNet's 512×512 depth resolution significantly outperforms Stability AI's SD2 64×64 depth maps for preserving fine structure.

| ControlNet Model | Input | Best Use for Jewelry |
|---|---|---|
| Canny Edge | Canny edge detection | Preserve outline structure |
| Depth Map | MiDaS depth | Geometry preservation |
| Normal Map | Normal from depth | Fine geometry; better than depth for small details |
| HED Boundary | Soft boundary | Recoloring and lighting variations |
| Human Pose | OpenPose | Try-on with body positioning control |

### IP-Adapter

**[tencent-ailab/IP-Adapter](https://github.com/tencent-ailab/IP-Adapter)**
*BSD-3-Clause - 6.5k stars - Paper: [arXiv:2308.06721](https://arxiv.org/abs/2308.06721)*
Lightweight adapter (22M parameters) enabling pre-trained diffusion models to accept reference image prompts. Allows generating new scenes around a product while preserving product identity. Compatible with ControlNet for combined geometry + reference guidance - the most accessible open-source path toward jewelry fidelity.

| Variant | Description |
|---|---|
| IP-Adapter | Standard, SD 1.5 |
| IP-Adapter-Plus | Enhanced fine-grained features |
| IP-Adapter-XL | For SDXL base models |
| IP-Adapter-FaceID | Face identity preservation |

### Segmentation Models

**[Meta AI / SAM 2](https://ai.meta.com/research/sam2/)**
Segment Anything Model 2 for images and video. Not jewelry-specific - see documented limitations for reflective objects (48.47% IoU on mirror/glass surfaces per [SAM Meets Glass](#jewelry-specific-ai)) - but foundational for building jewelry segmentation pipelines.

**[MathieuNlp/Sam_LoRA - Segment Your Ring](https://github.com/MathieuNlp/Sam_LoRA)**
Applies LoRA to SAM's ViT-B image encoder specifically for ring segmentation. Documents that baseline SAM "struggles to correctly segment the jewelry" and "takes the inside of the ring as part of the object." LoRA weights available for ranks 2-512. Key finding: higher rank (512) performs best; the model still struggles with reflections and gems. Small training dataset (8 images) limits generalization - a contribution opportunity.

### Background Removal

**[Bria RMBG 2.0](https://fal.ai/models/fal-ai/bria/background/remove)**
Professional-grade background removal trained exclusively on licensed data. Available via fal.ai API. Useful as a preprocessing step in jewelry photography pipelines before background generation.

### Jewelry LoRAs and Fine-Tuned Models

**[FLUX Gemstone Necklace / Jewelry Model - RunningHub](https://www.runninghub.ai/model/public/1860872696312590337)**
Flux-based LoRA specifically trained for gemstone and jewelry rendering. Available on the RunningHub platform. One of the few publicly accessible jewelry-specific fine-tuned models.

*Note: The public ecosystem of jewelry-specific LoRAs is sparse. Most available models are style-focused rather than fidelity-focused. This is an active contribution gap.*

### ComfyUI Workflows

**[ComfyUI](https://github.com/comfyanonymous/ComfyUI)**
Node-based Stable Diffusion interface enabling complex, reproducible workflows for product photography. Most accessible path for building custom jewelry photography pipelines without writing code.

**[ComfyUI Examples](https://github.com/comfyanonymous/ComfyUI_examples)**
Official example workflows with metadata enabling direct loading into ComfyUI.

**[Product Photography Workflow - r/comfyui](https://www.reddit.com/r/comfyui/comments/1egbk0b/achieve_perfect_product_placement_preserve/)**
Community-documented workflow for precise product placement while preserving details, including use of externally generated backgrounds.

**[Jewelry Product Images - RunningHub ComfyUI Workflow](https://www.runninghub.ai/post/1888155556365992461)**
ComfyUI workflow for diamond ring design enabling prompt-based background and scene changes while maintaining product fidelity.

---

## Datasets

### Jewelry-Specific

**[Jewelry Segmentation Dataset - Roboflow Universe](https://universe.roboflow.com/jewellerysegmentation/jewelry-segmentation-fy470)**
4,807 jewelry images with segmentation annotations. Format: COCO JSON. License: CC BY 4.0.

**[Jewelry Image Dataset - Hugging Face](https://huggingface.co/datasets/sidd707/jewelry-design-dataset)**
6,100+ high-resolution jewelry images across four categories (rings, necklaces, earrings, bracelets). License: not specified.

**[Jewelry Detection Dataset - Roboflow](https://universe.roboflow.com/amits/jewelry-detection)**
51 images with ring, earring, diamond, and necklace detection annotations. Small but annotated. License: CC BY 4.0.

**[Jewelry Store Pictures Dataset - Roboflow](https://universe.roboflow.com/jewellery/jewellerydataset_storepics)**
Lifestyle and store-environment jewelry images including earrings, rings, and pendants. Useful for virtual try-on training.

**[340K+ Jewelry Images AI Training Dataset - DataSeeds](https://datarade.ai/data-products/200k-jewelry-images-ai-training-data-object-detection-da-data-seeds)**
340,000+ globally sourced jewelry images with full EXIF data and object detection labels. Commercial; request pricing.

**[Jewelry & Fashion Accessories Dataset - OpenDataBay](https://www.opendatabay.com/data/ai-ml/0a24b2bd-1cb3-4f1f-badb-ec14585293af)**
5,000 professional studio jewelry images in JPG format. License: not specified.

**[11k Hands with Jewelry Segmentation - Zenodo](https://zenodo.org/records/6541286)**
11,076 hand photos (1600×1200px) from 190 people aged 18–75 with jewelry segmentation masks. Underutilized resource for ring and bracelet try-on AI.

### RareSense Open Datasets - HuggingFace

RareSense is the AI research organization that develops FormaNova. Their HuggingFace org ([huggingface.co/raresense](https://huggingface.co/raresense)) contains 76 datasets built specifically for jewelry AI pipelines - the largest concentration of jewelry-specific open training data publicly available. Datasets marked *request access* are available to researchers on request via the HuggingFace viewer interface.

#### Necklace Segmentation and Masking

**[raresense/necklace_updated_mask](https://huggingface.co/datasets/raresense/necklace_updated_mask)**
712 necklace images with updated segmentation masks. For training mask-based background replacement pipelines on necklace geometry.

**[raresense/necklace_new_mask](https://huggingface.co/datasets/raresense/necklace_new_mask)**
900 necklace images with revised mask annotations. Complements the above for necklace segmentation training.

**[raresense/necklace_same_zoom](https://huggingface.co/datasets/raresense/necklace_same_zoom)**
1,370 necklace images normalized to consistent zoom level. For models requiring controlled scale consistency across catalog images.

**[raresense/multi_necklace_dataset](https://huggingface.co/datasets/raresense/multi_necklace_dataset)**
4,500 rows. Broad necklace training set for generative model training.

**[raresense/multi_necklace_dataset_2](https://huggingface.co/datasets/raresense/multi_necklace_dataset_2)**
7,100 rows. Extended version - pair with the above for larger-scale necklace model training.

**[raresense/multi_necklace_dataset_2_resized](https://huggingface.co/datasets/raresense/multi_necklace_dataset_2_resized)**
7,100 rows at consistent input dimensions. Ready-to-use for pipelines requiring fixed resolution.

#### Flux Fine-Tuning Datasets

**[raresense/Single_panel_training_flux_jewelry](https://huggingface.co/datasets/raresense/Single_panel_training_flux_jewelry)**
16,400 rows. The largest public jewelry dataset in this collection. It is specifically structured for Flux model fine-tuning on jewelry. Single-panel format optimized for training.

**[raresense/flux_single_panel_necklace](https://huggingface.co/datasets/raresense/flux_single_panel_necklace)**
5,970 rows. Necklace-specific Flux fine-tuning data in single-panel format.

**[raresense/flux_multi_panel_necklace_only](https://huggingface.co/datasets/raresense/flux_multi_panel_necklace_only)**
4,710 rows. Multi-panel necklace variant. It is useful for models that need to learn necklace appearance across multiple contexts simultaneously.

**[raresense/flux_single_panel_ring_only](https://huggingface.co/datasets/raresense/flux_single_panel_ring_only)**
Ring-specific Flux fine-tuning data. One of the few publicly available ring-focused training sets.

#### Hand Jewelry and Pose Estimation

**[raresense/handjewelry_dwpose_classified](https://huggingface.co/datasets/raresense/handjewelry_dwpose_classified)**
6,490 rows of classified hand jewelry images with DWPose annotations. Directly applicable to ring and bracelet virtual try-on pipelines requiring pose-aware generation.

**[raresense/hand_jewellery_amature_test_set_dwpose](https://huggingface.co/datasets/raresense/hand_jewellery_amature_test_set_dwpose)**
310 hand jewelry images with DWPose annotations. Evaluation-focused complement to the classified set above.

**[raresense/jewelry-dwpose-processed-with-feathering](https://huggingface.co/datasets/raresense/jewelry-dwpose-processed-with-feathering)**
11,100 rows. DWPose-processed jewelry images with feathering applied at mask boundaries. It addresses the hard-edge artifact problem that makes composited jewelry imagery look unnatural.

**[raresense/30_hand_jewellery_amature_test_set](https://huggingface.co/datasets/raresense/30_hand_jewellery_amature_test_set)**
30-image curated test set for hand jewelry evaluation. Suitable as a held-out benchmark set.

#### Virtual Try-On (VITON-Style)

**[raresense/Evaluated_viton_style_jewelry_data](https://huggingface.co/datasets/raresense/Evaluated_viton_style_jewelry_data)**
6,340 rows. Evaluated VITON-style jewelry data, pre-screened for quality, making it suitable for fine-tuning without additional filtering.

#### Sketch and CAD

**[raresense/updated_sketches](https://huggingface.co/datasets/raresense/updated_sketches)**
3,310 rows. Jewelry sketch dataset for sketch-to-photo and CAD-to-render pipeline training.

**[raresense/updated-sketch](https://huggingface.co/datasets/raresense/updated-sketch)**
506 rows. Variant sketch dataset. It complements updated_sketches with additional sketch styles.

### Gemstone and Mineral

**[Gemstones Multiclass Classification CNN - Kaggle](https://www.kaggle.com/code/lsind18/gemstones-multiclass-classification-cnn)**
87-class gemstone image dataset with ~90:10 train/test split. Useful for gemstone recognition models.

**[Crystal Gems Dataset - GitHub](https://github.com/loliverhennigh/Crystal-Gems)**
Mineral images and labels sourced from minerals.net. Useful for gemstone classification training.

**[GEMTELLIGENCE - Nature Research 2024](https://www.nature.com/articles/s44172-024-00252-x)**
Deep learning approach for gemstone origin determination. References gemstone classification datasets and methodology for provenance identification.

### Reflective and Metallic Objects

**[RODD - Reflected Object Detection Dataset](https://github.com/Tqybu-hans/RODD)**
21,059 images for reflected object detection across 10 categories. 7:3 train/test split with bounding boxes and real/reflected classifications. Most directly relevant reflective-surface dataset publicly available.

**[ROBI: Multi-View Dataset for Reflective Objects](https://www.researchgate.net/publication/351476192_ROBI_A_Multi-View_Dataset_for_Reflective_Objects_in_Robotic_Bin-Picking)**
Multi-view dataset of highly reflective industrial objects. Methods applicable to jewelry metal perception.

**[Sim-to-Real Dataset of Industrial Metal Objects - MDPI 2024](https://www.mdpi.com/2075-1702/12/2/99)**
Diverse metallic object dataset addressing symmetry, texturelessness, and high reflectivity - properties shared with jewelry metals.

### Virtual Try-On Reference

**[Awesome Virtual Try-On - GitHub](https://github.com/minar09/awesome-virtual-try-on)**
Curated list of VTON research, code, and datasets. Primarily clothing-focused; jewelry-specific resources are sparse, representing an active gap.

---

## Evaluation Metrics and Tools

No published benchmark exists specifically for jewelry AI fidelity. The following metrics are the current best practice for evaluating jewelry generation quality.

### Perceptual and Structural Similarity

**[LPIPS - Learned Perceptual Image Patch Similarity](https://github.com/richzhang/PerceptualSimilarity)**
*Zhang et al. - CVPR 2018 - BSD License - 4.2k+ stars*
Measures perceptual similarity using deep network activations. Better than PSNR/SSIM for detecting the kinds of degradation that matter for jewelry: facet edge loss, prong geometry changes, subtle texture destruction. Variants: `alex` (best forward scores), `vgg` (perceptual loss training), `squeeze` (lightweight).

**[IQA-PyTorch (pyiqa)](https://github.com/chaofengc/IQA-PyTorch)**
*3.2k stars - pip install pyiqa*
Comprehensive PyTorch image quality toolbox with GPU acceleration. Includes SSIM, MS-SSIM, LPIPS, PSNR, FID, SFID, NIMA, and more in a unified interface. Recommended as the primary evaluation library for jewelry AI pipelines.

### Generative Quality

**[Fréchet Inception Distance - TorchMetrics](https://lightning.ai/docs/torchmetrics/stable//image/frechet_inception_distance.html)**
Measures distance between distributions of real and generated images using Inception-v3 features. Standard metric for generative model quality; lower = better. Widely used but increasingly supplemented by newer metrics.

**[Rethinking FID: Towards a Better Evaluation Metric for Image Generation](https://openaccess.thecvf.com/content/CVPR2024/papers/Jayasumana_Rethinking_FID_Towards_a_Better_Evaluation_Metric_for_Image_Generation_CVPR_2024_paper.pdf)**
*Jayasumana et al. - CVPR 2024*
Proposes improvements to FID methodology. 399+ citations indicate significant community momentum toward alternative evaluation approaches.

### Identity and Product Preservation

**[Composite Image Evaluation Toolkit - bcmi](https://github.com/bcmi/Composite-Image-Evaluation)**
Provides DINO score (ViT-S/16 cosine similarity - measures structural/identity preservation) and CLIP score (semantic similarity) in a single toolkit. DINO score is particularly valuable for measuring whether generated jewelry matches the reference product's geometry and identity.

**[Inpainting Evaluation Metrics - GitHub](https://github.com/SayedNadim/Inpainting-Evaluation-Metrics)**
Implements L1, L2, SSIM, PSNR, and LPIPS for evaluating inpainting quality. Relevant for measuring seam artifacts at jewelry/background boundaries.

### Recommended Metric Stack for Jewelry AI

| Aspect | Metric | Rationale |
|---|---|---|
| Fine detail preservation | LPIPS | Captures facet edge and prong changes |
| Metal color accuracy | SSIM + Delta-E (CIELAB) | Structural + color fidelity combined |
| Product identity preservation | DINO Score | Measures whether the piece is recognizably the same |
| Scene generation quality | FID | Overall generative quality |
| User perception | Human evaluation | Gold standard for ecommerce fit |

For color accuracy: Delta-E values below 1.0 are imperceptible; above 3.5 are perceptible at first sight. Gold-to-silver color shift in generated images typically scores Delta-E > 5.

*A standardized Jewelry Fidelity Benchmark (JFB) does not yet exist. This represents the most significant evaluation gap in the field and an open contribution opportunity.*

---

## Production Tools

### Jewelry-Specialized AI Platforms

Tools built exclusively for jewelry, with no multi-category scope.

**[FormaNova](https://formanova.ai)**
The broadest jewelry-specialized platform: combines AI photography, worn jewelry preservation, and CAD generation in one product. Core capabilities:
- **Worn jewelry preservation**: upload a photo of jewelry being worn (on hand, neck, or ear), the AI preserves the jewelry with pixel-level fidelity while replacing the model, background, and context with studio-quality output
- **Unworn product photography**: transform flat product shots into professional backgrounds and lifestyle scenes
- **CAD generation**: generate jewelry CAD designs from reference images - a capability absent from all other platforms in this list
- Preserves geometry, metal type, gemstone color, and setting details across generation
- Target: jewelry brands, ecommerce operators, designers, and photographers
- Pricing: credit-based, from $9/month.

**[NeuroViz](https://neuroviz.ai/)**
AI photography platform trained on 50,000+ jewelry images and fine-tuned exclusively on jewelry materials. 
- **15+ specialized tools**: including retouching, scene generation, virtual try-on, video generation, and 3D models. 
- Claims 90% cost savings vs. studio.
- Batch processing available.
- Isolated processing - images do not train third-party models.
- Pricing: from $30/month.

---

### General Product Photography with Jewelry Support

Multi-category tools with meaningful jewelry capability. Not jewelry-exclusive.

**[Claid AI](https://claid.ai/)**
AI photo editing studio for ecommerce. Offers background generation and on-model placement with a jewelry-specific workflow for ring placement. Broad multi-category platform (apparel, food, cosmetics, jewelry). Pricing: credit-based, from $9/month. API available.

**[Photoroom](https://www.photoroom.com/)**
AI background removal and product photography with dedicated jewelry features. Automates image production for luxury and vintage pieces. Free tier; paid plans from $9/month. API available.

**[Pebblely](https://pebblely.com/)**
Background generation with a dedicated jewelry category. Fast and accessible for small sellers. 40 free images/month; paid plans from $19/month. API available for enterprise.

---

### Virtual Try-On Platforms

**[TryonJewel](https://tryonjewel.com/)**
AI and AR-powered platform for real-time 3D virtual try-on for earrings, necklaces, bracelets, and rings.

**[KiviSense Jewelry AR](https://tryon.kivisense.com/blog/ar-solution-jewelry/)**
Virtual jewelry try-on via phone or webcam for earrings, pendants, bracelets, rings, and charms.

**[SellerPic](https://www.sellerpic.ai/tools/virtual-try-on-accessories)**
Virtual try-on for accessories including rings, jewelry, glasses, and watches. On-model image generation for ecommerce listings.

**[Bandy AI](https://bandy.ai/ai-virtual-try-on-accessories)**
Accessories try-on generating on-model images with rings, jewelry, and hats.

**[Pic Copilot](https://www.piccopilot.com/tools/tryon-accessories)**
Accessory fitting previews (sunglasses, handbags, jewelry) on professional AI fashion models.

**[The New Black AI](https://thenewblack.ai/ai-design-features/ai-virtual-try-on-jewelry)**
Virtual try-on for rings, bracelets, necklaces, and earrings with on-model output.

**[HuHu AI](https://huhu.ai/virtual-jewelry-try-on/)**
Jewelry try-on overlaying accessories onto model photos for on-model product imagery.

---

### Managed Services and Agencies

Human-operated studios and agencies delivering finished jewelry visuals - 3D renders, animation, CAD, and photography - using professional software and AI tooling behind the scenes. The output is manually delivered; not an automated self-serve platform.

**[CrystalClear3D](https://www.crystalclear3d.com/)**
Jewelry 3D animation, photorealistic render, and CAD/CAM design service. Works with brands ranging from independent designers to Blue Nile and Helzberg Diamonds. Delivers 360° animations, hero renders, and CAD files as finished assets. Pricing is per-project.

**[Thinkspace](https://www.thinkspacehq.com/)**
Full-service jewelry digital platform combining ecommerce website build, 3D product configurator, 360° web spin, diamond search integration, and marketing services. More of a technology partner for jewelry retailers than a pure photography service. It is relevant for brands needing a complete visual infrastructure rather than individual image outputs.

**[SeePossible - Precious Preview](https://www.seepossible.com/precious-preview)**
Fine jewellery rendering and animation service delivering CGI-based product imagery and brand content. Works with established jewelry names including Raymond, Farah Khan, Walking Tree, and With Clarity. Relevant for brands that want photorealistic rendered imagery without a physical photoshoot - distinct from AI generation in that outputs are traditionally rendered rather than diffusion-based.

---

### Generalist Text-to-Image Generators

These are not product photography tools by design, but they are the first tools most jewelry sellers attempt. Documented here, along with an assessment of respective jewelry-specific capability and failure modes.

**[DALL-E 3](https://platform.openai.com/docs/guides/images) - OpenAI / ChatGPT**

| Capability | Assessment |
|---|---|
| Background replacement | Partial - generates scenes but not reference-guided |
| Object fidelity | No native reference preservation |
| Worn / on-model generation | Generates, does not preserve the specific piece |
| Metal color accuracy | Unreliable - prone to prong hallucination, stone shape distortion |
| Best use for jewelry | Mood board ideation; not suitable for product imagery |

**[Gemini Image Generation (Imagen 3)](https://ai.google.dev/gemini-api/docs/image-generation) - Google**

| Capability | Assessment |
|---|---|
| Background replacement | Partial - scene generation, not reference-guided |
| Object fidelity | No native reference preservation |
| Worn / on-model generation | Not designed for product photography |
| Metal color accuracy | Prompt-dependent, unreliable |
| Best use for jewelry | Creative concepting; not suitable for product imagery |

**[Midjourney](https://www.midjourney.com/)**

| Capability | Assessment |
|---|---|
| Background replacement | Scene generation, not reference-guided |
| Object fidelity | High distortion of specific product details |
| Worn / on-model | Strong style; weak product accuracy |
| Metal color accuracy | Variable |
| Best use for jewelry | Hero campaign imagery where artistic interpretation is acceptable; not for accurate product representation |

**[Adobe Firefly](https://firefly.adobe.com/)**

| Capability | Assessment |
|---|---|
| Background replacement | Generative Fill feature; limited reference guidance |
| Object fidelity | Limited |
| Notable | Trained on licensed data only - commercially safe outputs |
| Best use for jewelry | Background fill as a step in a broader editing workflow |

**[Flux.1 - Black Forest Labs](https://blackforestlabs.ai/)**

| Capability | Assessment |
|---|---|
| Detail retention | Better than prior diffusion models due to 16-channel VAE |
| Reference guidance | Requires IP-Adapter or similar - not native |
| Fine-tuning potential | Open weights (FLUX.1[dev]) allow jewelry-specific fine-tuning |
| Best use for jewelry | When fine-tuned for jewelry, shows meaningful promise over SDXL |

**[Stable Diffusion 3.5 - Stability AI](https://stability.ai/)**

| Capability | Assessment |
|---|---|
| Architecture | Improved over SD 1.5 and SDXL |
| Reference guidance | Requires ControlNet + IP-Adapter combination |
| Notable | Open-source; most customizable option for building bespoke pipelines |
| Best use for jewelry | Potential foundation for custom fine-tuned jewelry pipelines |

*No published systematic study tests these generators on jewelry fidelity metrics. Documented failure modes above are drawn from community observations on Reddit and LinkedIn. Systematic academic evidence of these failure modes does not yet exist. It is an open research gap.*

---

## Tutorials and Technical Guides

### Jewelry-Specific

**[How To Use Stable Diffusion ComfyUI Workflows For eCommerce Jewelry](https://www.youtube.com/watch?v=EVkarQQPKFY)**
*Video / YouTube - Intermediate*
Step-by-step ComfyUI workflow specifically for ecommerce jewelry, demonstrating transformation of product images for marketplace use.

**[AI-Enhanced Jewelry Photography: Quick Setup, Stunning Results](https://www.youtube.com/watch?v=qv1YMbpO4Tw)**
*Video / YouTube - Beginner*
Covers jewelry photography basics combined with AI enhancement. Useful entry point for jewelers new to AI tooling.

**[How I Fine-Tuned Stable Diffusion to Produce Museum-Grade Jewelry Photography](https://www.linkedin.com/pulse/how-i-fine-tuned-stable-diffusion-produce-jewelry-2-hours-monti-jhm8f)**
*Case Study / LinkedIn - Advanced*
Practical report documenting SDXL fine-tuning for jewelry. Explicitly documents pre-fine-tuning failures: "distort shapes; turn bracelets into random metal blobs; add imaginary gemstones." One of the few published accounts of jewelry-specific fine-tuning challenges and results.

**[Mastering Jewellery Photos - Deep-image.ai](https://deep-image.ai/blog/mastering-jewelry-photography-a-step-by-step-guide-to-creating-backgrounds-with-deep-image-ai/)**
*Tutorial / Blog - Beginner*
Step-by-step guide to AI background generation for jewelry product photos.

### Product Photography Pipelines

**[How to Use Stable Diffusion to Generate Product Images - Mercity.ai](https://www.mercity.ai/blog-post/use-stable-diffusion-to-generate-product-images)**
*Tutorial / Blog - Intermediate*
Comprehensive guide covering workflow setup, prompt engineering, and product-specific considerations for Stable Diffusion.

**[From White to Wow: Crafting Captivating Scenes with Stable Diffusion](https://medium.com/design-bootcamp/from-white-to-wow-crafting-captivating-scenes-with-stable-diffusion-76bfe45c7299)**
*Tutorial / Medium - Intermediate*
Transforming white-background product shots into styled scenes using Stable Diffusion.

**[Developing an AI Solution for Product Photography: What We Learned - ML6](https://www.ml6.eu/en/blog/developing-an-ai-solution-for-product-photography-what-we-learned)**
*Case Study / Blog - Advanced*
Enterprise implementation experience report. Practical lessons from building AI product photography at scale.

**[Product Photography with ComfyUI - MyAIForce](https://myaiforce.com/comfyui-product-photography/)**
*Tutorial / Blog + Video - Intermediate*
ComfyUI workflows for product photography including blending, relighting, and detail enhancement.

### Fine-Tuning

**[The Guide to Fine-Tuning Stable Diffusion with Your Own Images - Tryolabs](https://tryolabs.com/blog/2022/10/25/the-guide-to-fine-tuning-stable-diffusion-with-your-own-images)**
*Tutorial / Blog - Advanced*
Comprehensive DreamBooth implementation guide. The foundation for jewelry-specific model fine-tuning.

**[Stable Diffusion 3 Medium Fine-Tuning Tutorial - Stability AI](https://stability.ai/learning-hub/stable-diffusion-3-medium-fine-tuning-tutorial)**
*Tutorial / Official Documentation - Advanced*
Official Stability AI fine-tuning guide for SD3 Medium.

### Prompt Engineering for Jewelry

**[Stable Diffusion Prompts for Jewelry - OpenArt](https://openart.ai/blog/post/stable-diffusion-prompts-for-jewelry)**
*Prompt Guide - Beginner*
25 curated prompts optimized for jewelry generation in Stable Diffusion.

**[Midjourney Prompts for Jewelry - Galaxy AI](https://blog.galaxy.ai/midjourney-prompts-for-jewelry)**
*Prompt Guide - Beginner*
Midjourney-specific prompts for jewelry design and photography.

---

## Industry Context

### Market Size

- Global online jewelry market: **$75.3B (2023)**, projected $103.9B by 2030 at 4.7% CAGR - [Yahoo Finance / Global Industry Analysts 2024](https://finance.yahoo.com/news/online-jewelry-business-report-2024-083200093.html)
- Online jewelry market projected to grow **$58.4B from 2024–2028** - [Technavio / PR Newswire](https://www.prnewswire.com/news-releases/online-jewelry-market-size-is-set-to-grow-by-usd-58-4-billion-from-2024-2028--innovation-in-jewelry-design-and-technology-boost-the-market-ai-role-and-impact-technavio-302227514.html)
- Total jewelry market: **$381.54B (2025)**, projected $578.45B by 2033 at 5.5% CAGR - [Grand View Research](https://www.grandviewresearch.com/industry-analysis/jewelry-market)

### Photography Cost Benchmarks

- Freelance photographer: **$25–$50/image** (decent); **$600/hour** (high-end) - [Picup Media](https://blog.picupmedia.com/how-much-is-photography-costing-your-jewelry-business/)
- Lifestyle with model: **$1,500–$3,000 for 30 pieces** ($50–$100/item) - [Picup Media](https://blog.picupmedia.com/how-much-is-photography-costing-your-jewelry-business/)
- Studio day rates: **$1,000–$2,500+** - [2025 Cost Guide](https://iguana-perch-ng66.squarespace.com/blog/the-cost-of-a-jewelry-photographer-near-me-what-to-expect-in-2025)
- Agency pricing (e.g. Squareshot): **from $70/image** with 8-day delivery - [Squareshot](https://www.squareshot.com/services-categories/jewelry)

### Photography Quality and Conversion

- Jewelry shoppers view an average of **8–12 images** before purchasing - more than nearly any other product category - [Razor Creative Labs](https://www.razorcreativelabs.com/blog/why-high-end-jewelry-photography-is-the-most-challenging-product-photography)
- A/B test: improved product photography led to a **54% lift in conversions** for an 8-figure jewelry brand - [Blue Stout Case Study](https://bluestout.com/case-studies/how-this-8-figure-jewelry-brand-lifted-product-conversions-by-54-percent/)
- **15% of rings are returned for resizing** - accurate visual representation reduces this - [Post Industria](https://postindustria.com/how-to-reduce-returns-in-jewelry-e-commerce-with-disruptive-technologies-ar-commerce/)

### Platform Image Requirements

| Platform | Main Image Background | Min Resolution | Product Coverage |
|---|---|---|---|
| Amazon | Pure white (RGB 255,255,255) | 2000×2000px recommended | 85%+ of frame |
| Etsy | No strict background requirement | 635px width minimum | No requirement |
| Shopify | Flexible | 2048×2048px recommended | No requirement |

- [Amazon requirements](https://ailee.ai/guides/amazon-product-image-requirements)
- [Etsy requirements](https://help.etsy.com/hc/en-us/articles/115015663347)
- [Photography guide for Shopify, Etsy, and Amazon](https://news.centurionjewelry.com/jewelry-ecomm-tech/detail/how-to-photograph-jewelry-for-shopify-etsy-and-amazon-listings)

### Industry Research

**[A Guide to AI Visual Tools for Jewelers - American Gem Society](https://www.americangemsociety.org/a-guide-to-ai-visual-tools-for-jewelers/)**
Comprehensive practitioner guide to AI visual tools from the American Gem Society.

**[Jewelry Photography Insights from 1,000+ E-commerce Sellers - Photoroom](https://www.photoroom.com/blog/jewelry-photography-ecommerce)**
Survey data on photography practices, editing pain points, and visual strategies across jewelry ecommerce sellers.

---

## Communities

### Reddit

| Community | Size | Focus |
|---|---|---|
| [r/StableDiffusion](https://www.reddit.com/r/StableDiffusion/) | 1M+ | Technical AI image generation; product photography workflows |
| [r/comfyui](https://www.reddit.com/r/comfyui/) | Active | ComfyUI workflows and custom nodes |
| [r/midjourney](https://www.reddit.com/r/midjourney/) | Active | Midjourney prompts and outputs |
| [r/jewelers](https://www.reddit.com/r/jewelers/) | Active | Professional jewelry community; AI tool discussions |
| [r/productphotography](https://www.reddit.com/r/productphotography/) | Active | Product photography equipment, technique, and AI |

### Discord

- [Midjourney Official Discord](https://discord.gg/midjourney) - Primary Midjourney community
- [Flux Generative Art Discord](https://discord.com/invite/6SVng3Q4eR) - 2,900+ members, Flux-focused
- [Photography Lounge Discord](https://discord.com/invite/photography) - 37,000+ members, professional photography

### Developer Communities

- [AUTOMATIC1111 WebUI Discussions](https://github.com/AUTOMATIC1111/stable-diffusion-webui/discussions) - Technical Stable Diffusion implementation
- [ComfyUI GitHub](https://github.com/comfyanonymous/ComfyUI) - Issues and discussions on product photography workflows

*No dedicated community exists specifically for AI jewelry photography. This repository is intended to serve as a gathering point. Open an issue to share resources, discuss findings, or propose additions.*

---

## Contributing

Contributions are welcome. To add a resource:

1. Fork this repository
2. Add your resource to the appropriate section with a one-sentence description of why it belongs
3. Ensure the link is live and the resource is actively maintained
4. Submit a pull request

**What we include:** Papers with DOI or arXiv ID, GitHub repos with evidence of active use, live commercial tools, and datasets with clear license information.

**What we don't include:** Broken or abandoned links, unverifiable claims, SEO content farms, or tools that are waitlist-only with no live product.

**Open contribution gaps:** Jewelry-specific LoRAs, a Jewelry Fidelity Benchmark (JFB), systematic failure mode studies for generalist generators on jewelry, and advanced technical tutorials on detail-preserving fine-tuning pipelines.

---

*Maintained by [FormaNova](https://formanova.ai) - AI photography and CAD generation built exclusively for jewelry.*
