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
  - name: Richèl J.C. Bilderbeek
    orcid: 0000-0003-0872-7098
    affiliations: 1
affiliations:
 - name: Groningen Institute for Evolutionary Life Sciences, University of Groningen, Box 11103, 9700 CC Groningen, The Netherlands
   index: 1
date: 15 December 2021
bibliography: paper.bib
---

# Summary

Evolutionary biology is the study of, among others, speciation and extinction of a community of species. Ideally, such species communties are independent and isolated. Islands are a setting in which this happens naturally and, due to this, these are the most ideal systems to study within evolutionary biology. However, we cannot directly measure when an island was colonized, when a colonist species speciated, or when some of these new species went extinct. We can, however, use genetic data to reconstruct the evolutionary history of an island community. One of the common simplifying assumptions made (by, for example, the `DAISIE` R package [@etienne_daisie_2022]) is, that mainland species (i.e. the species that colonize the island) cannot go extinct. `DAISIEmainland`, however, is an R package allows the mainland species to go extinct and speciate. Providing a more realistic model of the island and the mainland for evolutionary biology research, `DAISIEmainland` allows the: (1) simulation of the evolutionary history on islands, (2) visualise that history, (3) calculate and plot summary metrics of the simulated data, with the goal of being able to simulate island and test current inference models in island biogeography (e.g. `DAISIE`).

# Statement of Need

Analysis of phylogenetic data has provided many insights in evolutionary biology. Central to these advances is the R language and the multitude of R packages which has facilitated the widespread utilisation these methods [@paradis_analysis_2006]. Phylogenetic research in the domain of island biogeography was lacking until the development of the Dynamic Assembly of Island biota through Speciation, Immigration and Extinction (DAISIE) model provided several key findings the macroevolution of island species [@valente_equilibrium_2015; @valente_simple_2020]. However, the performance and robustness of this island biogeography inference model is unknown when its assumptions are violated under biologically realistic scenarios. A central assumption of the DAISIE likelihood model is a static unevolving mainland pool of species. DAISIEmainland allows for the simulation of phylogenetic data of island species that can be used to test whether a dynamic mainland species pool causes poor model estimation performance. The package allows for testing multiple scenarios that may be faced by empiricists: mainland species go extinct before the present, mainland species are taxonomically known but not phylogenetically sampled, and mainland species are taxonomically undiscovered. The DAISIEmainland package has been applied to test the the robustness of the `DAISIE` model [@lambert_effect_2022] (see `vignette(topic = "inference_performance", package = "DAISIEmainland")` for details). `DAISIEmainland` outputs data in the `DAISIE` format [@etienne_daisie_2022], for ease of application to the `DAISIE` R package which provides a suite of phylogenetic likelihood inference models for island biogeography.

## Simulation of the evolutionary history on islands

**[RJCB: I feel a vignette is a superior place to show the detailed mathematics, similar to the (not yet existing) plotting vignette]**

DAISIEmainland simulates events (i.e. speciation, extinction and immigration)
on both the mainland and island, using the Doob-Gillespie algorithm.
The Doob-Gillespie algorithm is a stochastic exact solution that is used to simulate continuous-time processes [@gillespie_general_1976; @gillespie_exact_1977; @gillespie_stochastic_2007].
The mainland is simulated under a Moran process [@moran_random_1958], whereby every species extinction is immediately followed by a random species giving rise to two new species (speciation). Figure 1 shows how this shapes the history of the mainland:
the number of species at any given times is the same.

![mainland](figs/mainland.png)
Figure 1: Mainland 


The island Doob-Gillespie algorithm is altered to accommodate the dynamic mainland pool. The time-steps are bounded to not jump over changes on the mainland to ensure the present state of the system (i.e. species on mainland) is always up-to-date. The algorithm checks whether any changes have occurs on the mainland since the last time step and if so the system is updated and the returned to the time at which the mainland last changed. This is valid owing to the Markov (memoryless) property of the Doob-Gillespie algorithm [@gillespie_general_1976; @gillespie_exact_1977; @gillespie_stochastic_2007].
**[RJCB: is this correct? The mainland is simulated first, which is a great simplification to prevent that 'time-steps are bounded']**

![island](figs/island.png)
Figure 2: Island

For both the island and mainland the timing and type of events are 
sampled from an exponential distribution, based on the rates of all events
possible.
For the mainland process, mainland extinction rate ($\mu_M$) is the only parameter,
whereas, for the island there are rates of cladogenesis ($\lambda^c$) (i.e. 
an island species splitting up in two), 
island extinction ($\mu$), colonisation ($\gamma$), and anagenesis ($\lambda^a$) (i.e.
an island species became different from its mainland ancestor).
The Doob-Gillespie samples time steps and events 
until the time step exceeds the total time of the simulation. 
The simulated data is formatted and the endemicity of each island colonist is assigned which is used in the `DAISIE` inference model. 

The `DAISIEmainland` simulation outputs two data sets: (1) contains full information of all species colonisation times, and (2) an incomplete information data set which resembles what an empirist would have access to. These two data sets allow for the quantification of error in estimation when the empirists does not have access to all the data (Fig. 2).

# Visualise that history

DAISIEmainland can show the simulated island and mainland histories,
such as displayed in the figures of this article.

**[RJCB: note that this vignette does not exist yet]**
See `vignette(topic = "visualising_data", package = "DAISIEmainland")` for details.

# Calculate and plot summary metrics of the simulated data

# Acknowledgements

JWL was funded through a Study Abroad Studentship by the Leverhulme Trust and was also funded by a NWO VICI grant awarded to RSE.

# References
