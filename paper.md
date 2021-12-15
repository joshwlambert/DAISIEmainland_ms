---
title: 'DAISIEmainland: an R package for simulating an island-mainland system for macroevolution on islands'
tags:
  - R
  - island biogeography
  - macroevolution
  - simulation
authors:
  - name: Joshua W. Lambert
    orcid: 0000-0003-0872-7098
    affiliation: 1
  - name: Pedro Santos Neves
    orcid: 0000-0003-0872-7098
    affiliations: 1
  - name: Richèl J.C. Bilderbeek
    orcid: 0000-0003-0872-7098
    affiliations: 1
  - name: Rampal S. Etienne
    orcid: 0000-0003-0872-7098
    affiliations: 1
affiliations:
 - name: Groningen Institute for Evolutionary Life Sciences, University of Groningen, Box 11103, 9700 CC Groningen, The Netherlands
   index: 1
date: 15 December 2021
bibliography: paper.bib
---

# DAISIEmainland: an R package for simulating an island-mainland system for macroevolution on islands

## Authors: Joshua W. Lambert, Pedro Neves, Richel Bilderbeek

## Summary

Islands have long been study systems in evolutionary biology for isolated evolution. The evolutionary dynamics of island species can be reconstructed with molecular data from present day species. DAISIEmainland is an R package that simulates the colonisation and diversification species from a evolving mainland species pool to an focal island system. The package contains functionality to visualise simulated data, calculate and plot summary metrics of the simulated data. The data outputted in the `DAISIE` format (see Etienne et al., 2022), for ease of application to the DAISIE R package which provides a suite of phylogenetic likelihood inference models for island biogeography.

[Insert figure here]

## Statement of Need

The performance of a model of island biogeography -- DAISIE -- is assumed to be reliable even in under biologically unrealistic assumption. DAISIEmainland allows for the simulation of phylogenetic island biogeography data that can be used to test whether a dynamic mainland species pool causes poor model estimation performance. The package allows for testing multiple scenarios that may be faced by empiricists: mainland species go extinct before the present, mainland species are taxonomically known but not phylogenetically sampled, and mainland species are taxonomically undiscovered. 

## Simulation Algorithm

The Gillespie algorithm is a stochastic exact solution that is used simulate processes (refs). It has several applications and extensions (see Allen and Dytham, tau leaping paper). The Gillespie algorithm can be used in evolutionary biology, for example to efficiently simulate a birth-death process (ref). The island-mainland simulation in the DAISIEmainland package uses a two-part Gillespie simulation. Firstly the mainland, which is simulated under a Moran process (Moran, 1958) uses a Gillespie algorithm where the time steps are given by the rate of mainland extinction which is the only parameter that effects events on the mainland. The Moran process means every species extinction is immediately followed by a random species giving rise to two new species (speciation). The second Gillespie algorithm is for simulating the island, and involves exploiting the memoryless aspect of the Gillespie algorithm. The algorithm checks whether an changes have occurs on the mainland since the last time step and if so the system is updated and the returned to that point in time.

## Example of research applicaton

The first scientific application of the DAISIEmainland R package is to conduct a performance analysis of the DAISIE inference model (Lambert et al., 2022). The DAISIE inference model can test many hypotheses in island biogeography, but under the assumption that the mainland species do not evolve macroevolutionary time scales (several millions of years). The DAISIEmainland package can produce data simulated with dynamic mainland and thus by applying this data to the inference model and quantifying the error in parameter estimates the performance and robustness of the models can be determined. See Lambert et al. 2022 or `DAISIEmainland:: more detail.

## Acknowledgements

Thanks to Luis Valente and Shu Xie for helpful discussions. JWL was funded through a Study Abroad Studentship by the Leverhulme Trust and was also funded by a NWO VICI grant awarded to RSE. PSN was funded through a FCT PhD Studentship with reference SFRH/BD/129533/2017, co-funded by the Portuguese Ministério da Ciência, Tecnologia e Ensino Superior and the European Social Fund.

## References

Lambert et al., 2022 The effects...

Etienne R.S et al., 2022 DAISIE R package