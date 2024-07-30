import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import linregress

# Read data from file
df = pd.read_csv('epa-sea-level.csv')

# Create scatter plot
plt.scatter(df['Year'], df['CSIRO Adjusted Sea Level'])

# Create first line of best fit
res = linregress(df['Year'], df['CSIRO Adjusted Sea Level'])
years_extended = pd.Series(range(1880, 2051))
sea_levels_extended = res.intercept + res.slope * years_extended
plt.plot(years_extended, sea_levels_extended, label='Best fit line 1')

# Create second line of best fit from year 2000
recent_df = df[df['Year'] >= 2000]
res_recent = linregress(recent_df['Year'], recent_df['CSIRO Adjusted Sea Level'])
years_recent_extended = pd.Series(range(2000, 2051))
sea_levels_recent_extended = res_recent.intercept + res_recent.slope * years_recent_extended
plt.plot(years_recent_extended, sea_levels_recent_extended, label='Best fit line 2', color='red')

# Add labels and title
plt.xlabel('Year')
plt.ylabel('CSIRO Adjusted Sea Level')
plt.title('Rise in Sea Level')
plt.legend()

# Save plot and return data for testing (do not modify)
plt.savefig('sea_level_plot.png')

def draw_plot():
    return plt.gca()
