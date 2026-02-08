## Background
This repository contains the source data and code to compile a checklist of flowering plants recorded in the Guianas (Guyana, Suriname, and French Guiana). It was developed for [Flora of the Guianas Consortium]( https://www.naturalis.nl/en/science/flora-of-guianas).

## Workflow
(1) Data retrieval (POWO, Tropicos, WFO, GBIF) → (2) Data cleaning → (3) Mapping to Darwin Core → (4) Dataset integration → (5) Manual quality control → (6) Compute indicators of [content quality](https://academic.oup.com/bioscience/advance-article/doi/10.1093/biosci/biaf191/8442886) and [governance](https://academic.oup.com/bioscience/advance-article/doi/10.1093/biosci/biaf071/8443372) for the checklist


## Published dataset
[Dataset on GBIF]( https://www.gbif.org/data-quality-requirements-checklists)

[Dataset on XXX]( https://www.naturalis.nl/en/science/flora-of-guianas)

## Code 
#### 1. Data retrieval 
#### 1.1 Plants of the World
````
library(kewr)
library(dplyr)
library(tidyr)

# Request a list of accepted species that occur in a Guyana, Suriname, French Guiana
# See https://barnabywalker.github.io/kewr/articles/building-checklist.html

query <- list(distribution="Iceland")
filters <- c("accepted", "species")

pp<-!duplicated(df_Guianas2$powo_id)
powo_id<-df_Guianas2[pp,c("powo_id")]

info_names_acc<-list()
ll_acc<-list()

for (i in 1:length(powo_id)){
  info_names_acc[[i]] <- lookup_powo(powo_id[[i]])
  ll_acc[[i]]<-tidy(info_names_acc[[i]])
  #print(mass)
}
