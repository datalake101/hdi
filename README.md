# Libraries
library(dplyr)
library(stringr)
library(ggplot2)
library(maps)
library(viridis)
 

rm(list=ls())
options(scipen = 999)

world <- map_data("world")
world <- world %>%
    dplyr::rename(country = 'region')

 
hdi_data <- read.csv("https://raw.githubusercontent.com/datalake101/hdi/main/hdi.csv")
hdi_data <- hdi_data %>% select(iso3, country, hdi_2021)

newWorld <- inner_join(world, hdi_data, by = "country")

 

#plot

ggplot(data = newWorld, mapping = aes(x = long, y = lat, group = group)) + 
    coord_fixed(1.3) +
    geom_polygon(aes(fill = hdi_2021)) +
    scale_fill_viridis_c(option = "cividis") + 
    ggtitle("Human Development Index 2021") +
    theme(
        axis.text = element_blank(),
        axis.line = element_blank(),
        axis.ticks = element_blank(),
        panel.border = element_blank(),
        panel.grid = element_blank(),
        axis.title = element_blank(),
        panel.background = element_rect(fill = "white"),
        plot.title = element_text(hjust = 0.5),
        legend.title = element_blank()
    )


    <img width="909" alt="image" src="https://github.com/datalake101/hdi/assets/80239178/a5f81443-081a-4dd9-8161-f7990eeb1628">
