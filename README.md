# Scatterplots-in-R-programming-
### Scatterplots ###

pacman::p_load(pacman,rio, tidyverse) # loading pacman, rio and tidyververse

## loading and preparing the data (Google search data)
Google.search.data <- import("StateData.xlsx") %>% as_tibble() %>% 
  select(state_code, psychRegions, instagram:modernDance) %>% 
  mutate(psychRegions = as.factor(psychRegions)) %>%
  print()
view(Google.search.data)

 
### SCATTERPLOTS ### 
## this shows the plot of all associations 
Google.search.data %>% select(instagram:modernDance) %>% plot() 

#Bivariate scatterplot with default
Google.search.data %>% select(scrapbook,modernDance) %>% plot()
#Another way . Remember this will select variables from scrapbook to modernDance
Google.search.data %>% select(scrapbook:modernDance) %>% plot()

## Bivariate scatter with options 
#pch means plotting character
Google.search.data %>% select(scrapbook, modernDance) %>%
  plot(main = "Scatterplot of Ghana with Nana Addo and Adwoa Sarfo", 
       xlab = "scrapbook", ylab = "Modern dance", 
       col = rainbow(6), pch = 20) 

?pch
# Adding a fit linear regressing line (y~x) 
Google.search.data %>% lm(modernDance~scrapbook, data = .) %>% abline()


## identifying outliers 
Google.search.data %>% select(state_code, scrapbook) %>% 
  filter(scrapbook > 4)%>% print() 

#Plotting the Bivariate scatterplot without outliers 

Google.search.data %>% select(scrapbook,modernDance) %>% 
  filter(scrapbook < 4) %>% 
  plot(main = "Scatterplot of Ghana without Nana Addo and Adwoa Sarfo ", 
       xlab = "scrapbook", ylab = "Modern dance", 
       col = rainbow(6), pch = 20)

# Adding a fit without outliers 
Google.search.data %>% filter(scrapbook < 4) %>% 
  lm(modernDance~scrapbook, data = .) %>% abline()
