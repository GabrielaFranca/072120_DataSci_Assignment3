# 072120_Class_Level_BarGraph_Summary
Prompts 1-4 of Assignment #3 Penguins data science
#Data
library(remotes)
remotes::install_github("allisonhorst/palmerpenguins")
library(palmerpenguins)
library(tidyverse)

#Variable class
class(penguins$sex)
class(penguins$body_mass_g)

#Variable levels
levels(penguin$sex)

#Missing Data
is.na(penguins)
is.na(penguins$flipper_length_mm)
is.na(penguins$sex)

#Analysis with NA value
penguins %>%
  group_by(island) %>%
  summarise(mean(bill_length_mm))

#NA counts bar graph
penguins %>%
  #group_by(species) %>%
  select(everything()) %>%
  summarise_all(funs(sum(is.na(.)))) %>%
  pivot_longer(cols = 1:7, names_to = 'columns', values_to = 'NA_count') %>%
  arrange(desc(NA_count)) %>%
  ggplot(aes(y = columns, x = NA_count)) + geom_col(fill = '#F0E442') +
  geom_label(aes(label = NA_count)) +
  #   scale_fill_manual(values = c("darkorange","purple","cyan4")) +
  theme_minimal() +
  labs(title = ‘Palmer Penguins NA Count')

#Summary
summary(penguins)
