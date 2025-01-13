# Heritage Weaver: Multimodal Linking of Museum Collections

## Short summary
This investigation focused on using embeddings to link the collections of the National Museum of Scotland and Science Museum Group using images of objects as well as associated metadata. We focused on linking 30,000 objects from the Science Museum with 1,500 from the National Museum of Scotland. All the relevant objects were on the theme of communications, textiles, and energy: connecting to the Congruence Engine's industrial heritage theme. 

We used SigLIP to embed the images and descriptions, then stored these vector representations with ‘name’, and ‘record_id’ and ‘img_url’ columns from collections management systems exports as metadata. We split the description into sentences (using the SpaCy sentence splitter for English) and indexed each sentence as a separate vector. 


## Research questions

1) Can images of objects be used to link national museum collections?

2) What role can researcher and curatorial expertise play in computer vision pipelines?

3) Is fine-tuning a model necessary for object embeddings?

4) What type of link is useful or interesting for researchers and curators?


## People 

- **Natasha Kitcher**: Conceptualization, Data curation, Investigation, Resources, Validation, Writing - original draft, Writing - review & editing 

- **Kaspar Beelen**: Data curation, Formal analysis, Investigation, Methodology, Software, Validation, Writing - original draft, Writing - review & editing

- **Geoff Belknap**: Supervision, Data Curation

- **Georgina Grant**: Resources (provided NMS collections data), Data Curation (participation in Heritage Weaver annotation workshops)

- **Jon Agar**: Data Curation (participation in Heritage Weaver annotation workshops)

- **Daniel Belteki**: Data Curation (participation in Heritage Weaver annotation workshops)

- **Max Long**: Data Curation (participation in Heritage Weaver annotation workshops)

- **Bernard Musesengwe**: Data Curation (participation in Heritage Weaver annotation workshops)

- **Jamie Unwin**: Resources (provided SMG collections data) 



## Data
- Science Museum Group object images and metadata from the following categories: telecommunications, radio communication, signalling and telecommunications

- National Museum of Scotland images and metadata from the following categories: telecommunications, computing 



## Method
We used SigLIP to embed the images and descriptions, then store these vector representations with ‘name’, and ‘record_id’ and ‘img_url’ as metadata. We split the description into sentences (using the SpaCy sentence splitter for English) and indexed each sentence as a separate vector. Each image was converted to a 768-dimensional vector using the standard Hugging Face processor.

We continued pre-training SigLIP on the 31,319 records from the NMS and SMG collections, each record pairing images with their object description and/or name s. We trained a SigLIP model by iterating over all the image-text pairs once.  Overall, training took no more than five hours using Google’s Colab L4 GPU. 

To test the links with human expert checkers, we set up an annotation experiment using LabelStudio on Hugging Face Spaces. The main goal of this exercise was to understand the conditions under which multimodal models suggest interesting connections and which connections are most useful. For the annotation experiment we set up an image classification task. For each annotator we sampled multiple record pairs (each pair comparing one NMS to one SMG object) for the different types of multimodal comparisons. We focus on intra-modal comparisons(text-to-text or image-to-image) and cross-modal comparison  (image-to-text and text-to-image)  

A series of historians and curators were recruited to annotate the record pairs, including curators from NMS who were familiar with the collection and objects selected for this work (Geoff Belknap and Georgina Grant), researchers who helped select categories of objects from SMG (Daniel Belteki and Max Long), and then a museum professional from the Discovery Museum in Newcastle (Bernard Musesengwe) and a scientific historian (Jon Agar). We had a spread of people with different levels of engagement with museum objects and a different awareness of our own investigation, so we could get an idea of how the way users might annotate objects could change. 

For the annotation session we only provided selected pairs with high similarity scores, i.e. those connections that model suggests a viable links. On top of this we added examples whose visual and textual representations are highly similar. We performed this sampling procedure for the original out-of-the-box model as well as the fine-tuned SigLIP models. We asked annotators to label the retrieved record pairs and study the relation between model type, comparison type and label to determine which factors are influential. Each annotator was presented with their own sample of 100 pairs to run through and annotate, choosing to assign each pair as either ‘same object,’ ‘similar object,’ ‘same category,’ and ‘no link’. These four labels were chosen to allow for objects to either be identical (two 700-series type telephones), similar (two telephones), the same category (two communications objects), or totally unrelated. 

## Tools



## Key initial findings
We found  fine-tuning models on historical data substantially improved record linkage. The links suggested by historically-aware models were more likely to produce meaningful connections (that is, point to similar items) across collections according to our annotators. Interestingly, we also found that linking based on text was slightly more successful than based on image similarity.


## Licence 
This work is licensed under a [Creative Commons Attribution 4.0 License - CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
