---
layout: post
title:  "Data Visualization Made Easy!"
date: 2024-10-04
description: 5 Tips and Tricks to make your visuals stand out above the rest   
image: "/assets/img/data_vis_heading.jpg"
display_image: false
---
## 5 Tips and Tricks to Make Your Visuals Stand Out Above the Rest
<p class="intro"><span class="dropcap">T</span>his post highlights different ways to take your visuals from "meh" to magnificent using the 'plotnine' Python library.</p>

### Introduction
<p class="tip-description">[Insert a brief description of the tip here.]</p>


{%- highlight python -%}
from sklearn import datasets
import pandas as pd
import seaborn as sns 
import palmerpenguins
from plotnine import (
    ggplot, aes, geom_point, labs, scale_color_manual, theme_minimal, 
    geom_bar, theme, element_text, facet_wrap, scale_fill_manual, 
    theme_bw, theme_light, element_blank, geom_smooth
)

# Load the penguins dataset and preprocess it
penguins = palmerpenguins.load_penguins()
penguins = penguins.dropna()
penguins['species_sex'] = penguins['species'] + ' - ' + penguins['sex']
penguins['species_sex'] = pd.Categorical(penguins['species_sex'])
{%- endhighlight -%}
---

### Tip 1: Start Simple
<p class="tip-description">[Insert a brief description of the tip here.]</p>

{%- highlight python -%}
# Insert your Python code for this tip here
{%- endhighlight -%}

---

### Tip 2: Show your labels some love!
<p class="tip-description">[Insert a brief description of the tip here.]</p>

{%- highlight python -%}
# Insert your Python code for this tip here
{%- endhighlight -%}

---

### Tip 3: [Insert Tip Title Here]
<p class="tip-description">[Insert a brief description of the tip here.]</p>

{%- highlight python -%}
# Insert your Python code for this tip here
{%- endhighlight -%}

---

### Tip 4: [Insert Tip Title Here]
<p class="tip-description">[Insert a brief description of the tip here.]</p>

{%- highlight python -%}
# Create a color plot for bill depth vs. length
color_plot = (
    ggplot(penguins, aes(x='bill_depth_mm', y='bill_length_mm', color='species')) +
    geom_point() +
    labs(
        title="Bill Depth vs. Length",
        subtitle="For Adelie, Chinstrap, and Gentoo Penguins on the Palmer Islands",
        x="Bill Depth (mm)", 
        y="Bill Length (mm)",
        color="Species"
    ) +
    scale_color_manual(values=["#26648E", "darkorange", "#53D2DC"]) +
    theme_light()
)
color_plot
{%- endhighlight -%}

---

### Tip 5: [Insert Tip Title Here]
<p class="tip-description">[Insert a brief description of the tip here.]</p>

{%- highlight python -%}
# Insert your Python code for this tip here
{%- endhighlight -%}

---

<p class="conclusion">In conclusion, these tips and tricks can significantly enhance your data visualizations. Happy plotting!</p>

