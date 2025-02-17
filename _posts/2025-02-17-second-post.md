---
title:  "Second post on the  personal website"
layout: post
mathjax: true
categories: media
---

## Welcome back!

This is the second test blog post on my personal website.

> Running block quote with >?
>
> hello
>
> hello?



Here is some *R* code 
```r
ggplot(data = res_mod_16, aes(x = Driver, y = estimate)) +
  
  # 95 %prediction interval (PI): twigs
  ggplot2::geom_errorbar(aes(ymin = lowerPR, 
                              ymax = upperPR,
                              x = Driver,
                              group = Genus),
                          width = 0, 
                          position = position_dodge(width = 0.6),
                          show.legend = FALSE, 
                          size = 1.2, 
                          alpha = 1) +
  
  # 95 %CI: branches
  ggplot2::geom_errorbar(aes(ymin = lowerCL, 
                              ymax = upperCL,
                              x = Driver,
                              group = Genus),  
                          width = 0, 
                          position = position_dodge(width = 0.6),
                          show.legend = FALSE, 
                          size = 3.5, 
                          alpha = 1) +
  
    # pieces of fruit (bee-swarm and bubbles)
  ggbeeswarm::geom_quasirandom(data = res_mod_16_data, 
                               aes(y = yi, 
                                   x = moderator, 
                                   size = 1/(sqrt(vi)), 
                                   colour = Genus,
                                   fill = Genus), 
                               alpha= 0.2,
                               width = 0.2,
                               dodge.width = 0.6) +
  
  scale_color_manual(breaks = c("Alexandrium", "Pseudo-nitzschia"),
                     values=c("#D55E00", "#009E73")) +
  
  
  # Dashed line at 0
  ggplot2::geom_hline(yintercept = 0, linetype = 2, colour = "black", alpha = 0.5) +
  
# Estimate points for trunks
  ggplot2::geom_point(aes(y = estimate,
                          shape = Genus,
                          fill = Genus),
                      size = 3,
                      position = position_dodge(width = 0.6)) +
  
  scale_shape_manual(values = c(22,23))+
  scale_fill_manual(breaks = c("Alexandrium", "Pseudo-nitzschia"),
                     values=c("#D55E00", "#009E73")) +
    

  ggplot2::theme_bw() +
  #ggplot2::guides(fill = "none", colour = "none") +
  ggplot2::theme(legend.position= c(0.6, 0.01), 
                 legend.justification = c(1, 0),
                 legend.margin = margin(t = -3,
                                        r = 0,
                                        b = -0.4,
                                        l = 0,
                                        unit = "mm"),
                 legend.background = element_rect(fill='white', 
                                                  colour = 'white'), #transparent legend bg
                 
                 legend.box.background = element_rect(fill='white', 
                                                      colour = 'white'), #transparent legend panel))) 
          plot.margin = margin(t = 0,
                             r = 0,
                             b = -3,
                             l = 4,
                             unit = "mm"))+
  
  ggplot2::theme(legend.title = element_text(size = 9)) +
  ggplot2::theme(legend.direction="horizontal") +
  ggplot2::theme(legend.background = element_blank()) +
  ggplot2::labs(y = bquote(LRR^~Delta),
                x = "",
                colour = "Genus", 
                size = "Precision (1/SE)") +
  ggplot2::theme(axis.text.y = element_text(size = 10, 
                                            colour ="black", 
                                            hjust = 0.5, 
                                            angle = 0),
                 
                 axis.text.x = element_text(size = 12, 
                                            colour ="black", 
                                            hjust = 0.5),
                 
                 axis.title.y = element_text(size = 13, 
                                            colour ="black", 
                                            hjust = 0.5,
                                            vjust = 2,
                                            angle = 90),
                 panel.grid.major.y = element_line(colour = "grey98"),
                 panel.grid.major.x = element_blank())+
  
  scale_y_continuous(limits = c(-2, 6.8),
                     breaks = seq(-1, 7, by = 1),
                     minor_breaks = NULL)+
  
  annotate(geom = "label", #Estimates Demand Alexandrium
           x = 0.7, 
           y = y_pos,
           fill = "white",
           colour = "black",
           label.size = NA,
           label = paste0(round(100*((exp(res_mod_16$estimate[1]))-1),0), "% increase", 
                          "\n", 
                          "[95% CI: ", round(100*((exp(res_mod_16$lowerCL[1]))-1),0), 
                         # "%",
                          " - ",
                          round(100*((exp(res_mod_16$upperCL[1]))-1),0), "]",  
                          "\n",
                          "[95% PI: ", round(100*((exp(res_mod_16$lowerPR[1]))-1),0), 
                         # "%",
                          " - ", 
                          round(100*((exp(res_mod_16$upperPR[1]))-1),0), "]"
                         ),
           parse = FALSE,
           size = annot_size)+ 
  
    annotate(geom = "label", ## K (n) Demand Alexandrium
           x = 0.7, 
           y = y_pos - 0.85, 
           fill = "white",
           colour = "black",
           label.size = NA,
           label = "K (N) = 14 (46)", 
           color = "black", 
           parse = FALSE, 
           size = annot_size)+
  
  annotate(geom = "label", #Estimates Demand Pseudo-nitzschia
           x = 1.25, 
           y = y_pos, 
           fill = "white",
           colour = "black",
           label.size = NA,
           label = paste0(round(100*((exp(res_mod_16$estimate[3]))-1),0), "% increase", 
                          "\n", 
                          "[95% CI: ", round(100*((exp(res_mod_16$lowerCL[3]))-1),0), 
                         # "%",
                          " - ",
                          round(100*((exp(res_mod_16$upperCL[3]))-1),0), "]",  
                          "\n",
                          "[95% PI: ", round(100*((exp(res_mod_16$lowerPR[3]))-1),0), 
                         # "%",
                          " - ", 
                          round(100*((exp(res_mod_16$upperPR[3]))-1),0), "]"
                         ),
           parse = FALSE,
           size = annot_size) +
  
  
  annotate(geom = "label", ## K (n) Demand Pseudo-nitzschia
           x = 1.25, 
           y = y_pos-0.85, 
           fill = "white",
           colour = "black",
           label.size = NA,
           label = "K (N) = 8 (20)", 
           size = annot_size) +
  
  annotate(geom = "label", #Estimates resource Alexandrium
           x = 1.8, 
           y = y_pos, 
           fill = "white",
           colour = "black",
           label.size = NA,
           label = paste0(round(100*((exp(res_mod_16$estimate[2]))-1),0), "% increase", 
                          "\n", 
                          "[95% CI: ", round(100*((exp(res_mod_16$lowerCL[2]))-1),0), 
                         # "%",
                          " - ",
                          round(100*((exp(res_mod_16$upperCL[2]))-1),0), "]",  
                          "\n",
                          "[95% PI: ", round(100*((exp(res_mod_16$lowerPR[2]))-1),0), 
                         # "%",
                          " - ", 
                          round(100*((exp(res_mod_16$upperPR[2]))-1),0), "]"
                         ),
           parse = FALSE,
           size = annot_size) +
  
  annotate(geom = "label", ## K (n) resource Alexandrium
           x = 1.8, 
           y = y_pos-0.85, 
           fill = "white",
           colour = "black",
           label.size = NA,
           label = "K (N) = 16 (29)", 
           color = "black", 
           parse = FALSE, 
           size = annot_size)+
  
  annotate(geom = "label", #Estimates resource Pseudo-nitzschia
           x = 2.38, 
           y = y_pos, 
           fill = "white",
           colour = "black",
           label.size = NA,
           label = paste0(round(100*((exp(res_mod_16$estimate[4]))-1),0), "% increase", 
                          "\n", 
                          "[95% CI: ", round(100*((exp(res_mod_16$lowerCL[4]))-1),0), 
                         # "%",
                          " - ",
                          round(100*((exp(res_mod_16$upperCL[4]))-1),0), "]",  
                          "\n",
                          "[95% PI: ", round(100*((exp(res_mod_16$lowerPR[4]))-1),0), 
                         # "%",
                          " - ", 
                          round(100*((exp(res_mod_16$upperPR[4]))-1),0), "]"
                         ),
           parse = FALSE,
           size = annot_size) +
  
  annotate(geom = "label", ## K (n) resource Pseudo-nitzschia
           x = 2.38, 
           y = y_pos-0.85, 
           fill = "white",
           colour = "black",
           label.size = NA,
           label = "K (N) = 3 (18)", 
           size = annot_size) 

#  ggsave(path = "figures_manuscript", "orchard_manual_DriverGenus_vert.tiff", width = 150, height = 130, units = "mm", dpi=700)
  

```

