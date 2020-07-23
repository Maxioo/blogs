---
layout: article
title: A Survey on Knowledge Graphs Representation, Acquisition and Applications
key: 100017
category: papers
tags: papers
date: 2020-07-22 14:16:00 +08:00
---

# A Survey on Knowledge Graphs:Representation, Acquisition and Applications

## 0. Summary

This paper gives a full-view categorization and new taxonomies to knowledge graph in 
1. **KRL, knowledge acquisition and knowledge-aware application.**
2. **Transformer-based encoding, GNN based propagation, RL based path reasoning and meta relational learning.**
3. Summary and outlook on future directions.

## 1. Categorization

- Knowledge representation learning
  - Representation Space
    - Point-wise
    - Manifold
    - Complex
    - Gaussian
    - Discrete
  - Scoring Function
    - Distance
    - Semantic Matching
    - Others
  - Encoding Models
    - Linear/Bilinear
    - Factorization
    - Neural Nets
    - CNN
    - RNN
    - Transformers
    - GCN
  - Auxiliary Information
    - Textual
    - Type
    - Visual
- Knowledge acquisition
  - Entity Discovery
    - Recognition
    - Typing
    - Disambiguation
    - Alignment
  - Relation Extraction
    - Neural Nets
    - Attention
    - GCN
    - GAN
    - RL
    - Others
  - Knowledge Graph Completion
    - Embedding-based Ranking
    - Path-based Reasoning
    - Rule-based Reasoning
    - Meta Relational Learning
    - Triple Classification
- Downstream knowledge-aware application
  - NLU
  - QA
  - Dialog system
  - Recommender system
  - Others
- Temporal Knowledge Graph
  - Temporal Embedding
  - Entity Dynamics
  - Temporal Relational Dependency
  - Temporal Logical Reasoning

## 2. Knowledge Representation Learning

### 2.1 Representation Space

#### 2.1.1 Point-Wise Space

Related model:

- TransE
- TransR
- NTM
- TransH

#### 2.1.2 Complex Vector Space

Related model:

- ComplEx: Hermitian dot product
- RotatE: Hadmard product
- QuatE: Hamiltion product

#### 2.1.3 Gaussian Distribution

Related model:

- KG2E
- TransG

#### 2.1.4 Manifold and Group

- ManifoldE: Manifold-based embedding
- TorusE: With Lie Group
- DihEdral: dihedral symmetry group

### 2.2 Scoring Function

Similar to energy function in the energy-based learning framework.

#### 2.2.1 Distance-based Scoring

- SE:  $f_r(h,t)=||M_{r,1}h-M_{r,2}t||_{L_1}$
- TransE:  $f_r(h,t)=||h+r-t||_{L_1/L_2}$
- TransH:  $f_r(h,t)=-||(h-w^T_rhw_r)+r-(t-w^T_rtwr)||^2_2$
- TransR:  $f_r(h,t)=-||M_rh+r-M_rt||^2_2$
- TransD:  $f_r(h,t)=-||(r_ph_p^T+I)h+r-(r_pt_p^T+I)t||_2^2$
- TransA:  Mahalanobis distance:  $f_r(h,t)=(|h+r-t|)^TW_r(|h+r-t|)$
- TransF:  $f_r(h,t)=(h+r)^Tt+h^T(t-r)$
- ...

#### 2.2.2 Semantic Matching

- SME

- DistMult
- HolE
- ANALOGY
- CrossE
- TorusE
- DihEdral

### 2.3 Encoding Models

