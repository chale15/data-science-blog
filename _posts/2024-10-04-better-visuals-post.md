---
layout: post
title:  "Data Visualization Made Easy!"
date: 2024-10-04
description: 5 Tips and Tricks to make your visuals stand out above the rest   
image: 
display_image: false
---

<p class="intro"><span class="dropcap">T</span>ake your visuals from "meh" to "magnificent" using the 'Plotnine' Python library.</p>

### Introduction

<p class="tip-description">What is the Plotnine Python Library, and how do we use it?
</p>

-   **Overview of Plotnine**
    -   Plotnine is a Python data visualization library that allows users to create simple or complex graphics using a grammar of graphics approach. This method helps you to build visualizations by layering components from the ground up, picking and choosing what elements you want your visual to contain.

-   **History and Development**
    -   Plotnine was developed as a Python adaptation of R’s ggplot2, a package which has been widely embraced due to its intuitive syntax and versatility. The library has evolved through community contributions, continuously integrating new features and updates to improve the user experience, and to allow anyone to create stunning visuals in Python.

-   **Installation and Setup**
    -   To install plotnine, you first need to know which package manager you use. If you're unsure, I recommend this <a href="https://www.jumpingrivers.com/blog/python-package-managers-pip-conda-poetry/" target="_blank" > guide </a>
    -   Then, run the following command from your terminal (if using pip):
    
        {%- highlight bash -%} 
        pip install plotnine 
        {%- endhighlight -%} 
        
        Alternatively, if using conda, you can run this command: 
        
        {%- highlight bash -%} 
        conda install -c conda-forge plotnine 
        {%- endhighlight -%}

    -   Once installed, a simple plot can be created as follows: 
    
        {%- highlight python -%} 

        from plotnine import ggplot, aes, geom_point 
        import pandas as pd

        df = pd.DataFrame({'x': [1, 2, 3], 'y': [4, 5, 6]}) 
        plot = (ggplot(df, aes(x='x', y='y')) + geom_point()) 
        print(plot) 

        {%- endhighlight -%} 

        <img src="{{site.url}}/{{site.baseurl}}/assets/img/basic_p9.png" alt="Basic Plot" />

For more complicated visuals, see the plotnine <a href="https://plotnine.org/reference/" target="_blank"> documentation </a>, 
or any guide for R's ggplot2

------------------------------------------------------------------------

### Tip 1: Start Simple

<p class="tip-description">

Before diving into plotnine, we need to ensure that our data has been cleaned, wrangled, and displays the trends we think it does.

</p>

-   **Data Preparation**
    -   Data visualization begins with clean, well-structured data. Proper data cleaning involves identifying and correcting errors, dealing with missing values, and ensuring that data types are appropriate for analysis. This can be done using tools like Pandas.

    -   Let's use the palmerpenguins dataset as an example. The data is mostly clean already, however the following code removes any missing values and creates a new feature that will help us with our analysis later on. 
    
        {%- highlight python -%} 
        # Load Packages 
        import pandas as pd 
        import palmerpenguins 
        from plotnine import ( 
            ggplot, aes, geom_point, labs, scale_color_manual, theme_minimal, geom_bar, theme, element_text, facet_wrap, scale_fill_manual, theme_bw, theme_light, element_blank, geom_smooth )

        # Load, clean, and feature engineer the penguins dataset

        penguins = palmerpenguins.load_penguins() 
        penguins = penguins.dropna() 
        penguins['species_sex'] = penguins['species'] + ' - ' + penguins['sex'] 
        penguins['species_sex'] = pd.Categorical(penguins['species_sex']) {%- endhighlight -%}

-   **Creating a Simple Plot with Matplotlib**
    -   Before we jump straight to plotnine, it’s beneficial to create a basic plot using <a href="https://matplotlib.org/stable/users/explain/quick_start.html" target="_blank">Matplotlib</a>. This initial step helps you visualize trends and identify potential patterns. For instance, let's say we want to examine the relationship between Bill Length and Bill Depth for Adelie Penguins: 

        {%- highlight python -%} 
        import matplotlib.pyplot as plt

        # Filter the DataFrame for 'Adelie' species

        adelie_penguins = penguins[penguins['species'] == 'Adelie']

        # Create the scatter plot

        plt.scatter(adelie_penguins['bill_length_mm'], adelie_penguins['bill_depth_mm']) 
        plt.title('Basic Scatter Plot') 
        plt.xlabel('Bill Length (mm)') 
        plt.ylabel('Bill Depth (mm)') 
        plt.show() 
        {%- endhighlight -%} 

        <img src="{{site.url}}/{{site.baseurl}}/assets/img/basic_sp.png" alt="Basic Scatter Plot" />

    - Simple visualizations like these help us to see trends and identify relationships, providing a foundation that we can build off of with plotnine.

------------------------------------------------------------------------

### Tip 2: Show Your Labels Some Love

<p class="tip-description">

Labels can make or break your visual, so putting in a little extra work with the labels can make your visual exponentially better.

</p>

-   **Importance of Clear Labels**
    -   Clear labeling is crucial for effective communication in data visualizations. Labels provide context, making it easier for viewers to interpret the information presented.

-   **Customizing Labels in Plotnine**
    -   In plotnine, you can manually adjust labels to improve clarity. Let's start with the following graph. What are we looking at? Who knows! 


    <img src="{{site.url}}/{{site.baseurl}}/assets/img/unlabeled_plot.png" alt="Unlabeled Plot" />

    -   But add labels and ... voila! We can easily see that we're looking at a bar plot of Penguin Counts on our 3 Islands over time! 

    {%- highlight python -%}

    labeled_plot = ( 
        ggplot(penguins, aes(x = 'year', fill = 'species')) + 
        geom_bar(aes(y='..count..'), position='dodge') + 
        labs( x = "Year", 
            y = "Count", 
            title = "Annual Penguin Count by Island" ) + 
        theme(plot_title = element_text(hjust = 0.5)) + 
        facet_wrap('island') + 
        scale_fill_manual(values = ["#26648E","#ff8c00","#53D2DC"]) 
    )
    print(labeled_plot)

    {%- endhighlight -%}

    <img src="{{site.url}}/{{site.baseurl}}/assets/img/labeled_plot.png" alt="Labeled Plot" />

------------------------------------------------------------------------

### Tip 3: Go Beyond the Basic Colors

<p class="tip-description">

Colors can make your visuals pop, but too much color can be distracting...

</p>

-   **The Role of Color in Visualization**
    -   Color can significantly influence how data is perceived. It helps highlight trends and differentiate between categories, enhancing the overall effectiveness of a visual.

-   **Choosing and Applying Color Palettes**
    -   Resources like <a href="https://colorbrewer2.org/#type=sequential&scheme=BuGn&n=3" target="_blank">Color Brewer</a> and <a href="https://color.adobe.com" target="_blank">Adobe Color</a> provide color palettes tailored for data visualization, or a simple Google Search can get the job done as well! Choose colors that align with your theme but aren't so crazy that they detract from the overall image.

-   **Balancing Color Usage**
    -   Use color to draw attention to key data points without overwhelming the viewer. A good rule of thumb is to stick to a maximum of three to six colors in a single visualization. For example, this graph shows Bill Length vs. Bill Depth for all penguins, with different species represented by different colors. 

        {%- highlight python -%} 
        color_plot = ( 
            ggplot(penguins, aes(
                x = 'bill_depth_mm', 
                y = 'bill_length_mm', 
                color = 'species')) + 
            geom_point() + 
            labs( 
                title = "Bill Depth vs. Length", 
                subtitle = "for Adelie, Chinstrap, and Gentoo Penguins on the Palmer Islands", 
                x = "Bill Depth (mm)", 
                y = "Bill Length (mm)", 
                color = "Species" ) + 
                scale_color_manual(values =["#26648E","#ff8c00","#53D2DC"])+ theme_light() 
        ) 
        print(color_plot) 
        {%- endhighlight -%}
        <img src="{{site.url}}/{{site.baseurl}}/assets/img/color_plot.png" alt="Color Plot" />

    -  But what if we want to further classify our penguins by sex? Choosing similar colors to our original three can help us to further differentiate between Male and Female penguins while still maintaining the original classification by species! 
    
     - {%- highlight python -%} 
        color_gender_plot = ( 
            ggplot(penguins, aes(
                x = 'bill_depth_mm', 
                y = 'bill_length_mm', 
                color = 'species_sex')) + 
            geom_point() + 
            labs( title = "Bill Depth vs. Length", 
                subtitle = "for Adelie, Chinstrap, and Gentoo Penguins on the Palmer Islands", 
                x = "Bill Depth (mm)", 
                y = "Bill Length (mm)", 
                color = "Species by Sex" ) + 
            scale_color_manual(values = ["#8faadf","#26648E","#f1c232","#ff8c00","#c5e9ec","#53D2DC"]) + 
            theme_light() 
        ) 
        print(color_gender_plot) 
        {%- endhighlight -%} 

        <img src="{{site.url}}/{{site.baseurl}}/assets/img/color_gender_plot.png" alt="Color by Gender Plot" />

---

### Tip 4: Be Easily Interpretable

<p class="tip-description">

The most important feature of any visual is its interpretability. Visuals exist to present information in a more manageble way than a list of seemingly meaningless numbers. Hence, if the target audience can't easily interpret a visual, the only thing that visual accomplished was to waste the time of the creator and the consumer.

</p>

-   **Emphasizing Clarity and Simplicity**
    -   The principle of "less is more" applies to data visualization. A cluttered visual can confuse rather than inform. Focus on what’s essential. What do the two visuals below have in common? They're both a complete mess! Sure, they present (presumably) meaningful data, however they try and add too many features, taking away all interpretability in the process.

        <img src="{{site.url}}/{{site.baseurl}}/assets/img/cluttered_visual_1.png" alt="Cluttered Visual 1" style="width:400px"/><img src="{{site.url}}/{{site.baseurl}}/assets/img/cluttered_visual_2.png" alt="Cluttered Visual 2" style="width:400px"/>

        -<a href="https://www.elsevier.com/connect" target="_blank"> Image 2 Source</a> 
        
-   **Strategies for Clean Visuals**
    -   Simplify your visuals by removing unnecessary elements, such as excessive gridlines or decorative features that don’t add value. For example, using themes: 

        {%- highlight python -%} 

        plot = (ggplot(df, aes(x='x', y='y')) + 
                geom_point() + 
                theme_minimal()) # Simplified theme 
        print(plot) 

        {%- endhighlight -%}

    - <img src="{{site.url}}/{{site.baseurl}}/assets/img/minimal_p9.png" alt="Minimal Theme Plot" />

    -  Highlight key insights directly through annotations, emphasis, or the use of color, keeping the overall design clean and focused.

------------------------------------------------------------------------

### Tip 5: Play Around!

-   **Experiment!**
    -   Every dataset is unique, and what worked for one visualization might not work well with another. By experimenting with different visual styles and parameters, you can ensure that your visual best suits the data, and highlights the desired information.
-   **Fine-tune Parameters!**
    -   Adjust aspects like point outlines, text sizes, line widths, and shapes to best fit your data. The possibilities are endless! 

        {%- highlight python -%} 
        plot = (ggplot(df, aes(x='x', y='y')) + 
        geom_point(size=3, shape=21, fill='blue', stroke=1.5, alpha=0.7) + 
        theme(text=element_text(size=12))) 
        print(plot) 
        {%- endhighlight -%}

------------------------------------------------------------------------

### Conclusion:
<p class="conclusion">

This blog post covered essential tips for enhancing your data visuals using the plotnine library, from data preparation and clear labeling to effective use of color and simplicity. Each visual you create tells the story of your data, so don't forget to share the stories your data tells and tag me! Happy plotting!

</p>
