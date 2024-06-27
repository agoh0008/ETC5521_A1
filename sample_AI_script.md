# Sample AI script

## Question 1

**ME:** ggplot(numbat_sightings, aes(x = day, y = sightings)) +
  geom_boxplot() +
  labs(x = "Day",
       y = "Number of Sightings",
       title = "Distribution of Daily Numbat Sightings") +
  theme_minimal()

how do i label outliers in my plot

**CHATGPT:** To label outliers in your boxplot created using ggplot2 in R, you can use the geom_text() function to add text labels to the plot. Here's how you can modify your existing code to label the outliers:


library(ggplot2)

ggplot(numbat_sightings, aes(x = day, y = sightings)) +
  geom_boxplot() +
  geom_text(data = numbat_sightings %>% filter(sightings > (quantile(sightings, 0.75) + 1.5 * IQR(sightings)) |
                                                sightings < (quantile(sightings, 0.25) - 1.5 * IQR(sightings))),
            aes(label = sprintf("Outlier: %d", sightings), x = day, y = sightings),
            vjust = -0.5, hjust = 0.5, color = "red") +
  labs(x = "Day",
       y = "Number of Sightings",
       title = "Distribution of Daily Numbat Sightings with Outliers Labeled") +
  theme_minimal()


In this code, the geom_text() function is used to add labels to the plot for data points that are considered outliers based on the IQR method. The data argument specifies the subset of the data that contains the outlier points. The aes(label = sprintf("Outlier: %d", sightings), x = day, y = sightings) argument sets the label content and position for each outlier. The vjust and hjust arguments control the vertical and horizontal positioning of the labels. The color argument sets the color of the labels (you can adjust this as needed).

Make sure you adjust the outlier detection logic based on your dataset and requirements. The code above assumes that you want to label outliers above the upper whisker and below the lower whisker using the IQR method.

**Analysis: ChatGPT was helpful in guiding me on how to label outliers in my plot, which showed distinctly on my boxplot when I tested it. Its instructions were straightforward as it provided clear explanations on how the outlier detection logic works and how to adjust the appearance of the labels. This not only ensures that I implement the solution correctly, but also understand the underlying concepts behind it. The solution was also customizable to my specific dataset and requirements, as ChatGPT highlighted that I might need to adjust the outlier detection logic based on my data and explained the parameters that can be modified for positioning and styling of the outlier labels.**
