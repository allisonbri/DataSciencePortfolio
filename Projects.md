# My Projects
<ins>**Transportation and Art Museums in North Carolina Counties**</ins> ~
[Link to code](PortfolioProject1.ipynb)

**Overview**  
This project examines whether transportation patterns are related to the types of museums found in North Carolina counties. Using county-level data, it compares how residents commute (for example, by car, public transit, walking, or biking) with the percentage of each county's museums that are classified as art museums. The goal is to see whether counties dominated by a particular mode of transportation tend to have a higher or lower share of art museums.  

**Research Question and dataset:**  

Is there a relationship between the most common mode of transportation used in different North Carolina counties and the percentage of museums in those counties that are classified as art museums?  

https://api.census.gov/data/2024/acs/acs1?get=NAME,B01001_001E&for=county:*&in=state:37&key={api_key}  
Unit of analysis: county  
44 rows and 8 columns used with 26 missing values in columns: Total_Transp_By_Vehicles_Available	Total_Public_Transp	No_Vehicle_Available    and   Walks  
https://museumsdatabase.com/  
Anthropic. (2026). Claude Sonnet 5 [Large language model]. https://claude.ai  
Artificial Intelligence was used to help create a csv dataset from the museum database website.  
Unit of analysis: county  
44 rows and 3 columns: percent_art_museum        museum_count	art_museum_count  

**Context:**  
Museum types may reflect the character of the communities around them. Counties where nearly everyone drives tend to be rural or suburban, while counties with more transit, walking, or biking tend to be denser and more urban, where arts institutions are often concentrated. This project asks whether car reliance is associated with the share of a county's museums that are art museums. The analysis is correlational and cannot show causation.  

<ins>Key Variables</ins>  

'''Car usage  

Concept: How much a county's residents rely on private cars rather than other modes of transportation.  
Measure: Number of workers who commute by personal car, truck, or van.  

'''Percentage of art museums  

Concept: How strongly a county's museums lean toward art rather than other types.  
Measure: (art museums ÷ total museums) × 100  
Art museum is defined as the museum database labels the museums, it is not based on the name of the museum.   

'''Walks  

Concept: How much workers in a county walk rather than rely on other modes of transportation.  
Measure: Number of workers who walk to work  

Controls: population density, median household income, and percentage of adults with a bachelor's degree, all at the county level.

**Findings:**  

<img width="310" height="280" alt="image" src="https://github.com/user-attachments/assets/345c4419-53c4-4d90-a37e-6360b48547e8" /> <img width="310" height="280" alt="image" src="https://github.com/user-attachments/assets/eea22c69-3f2a-46f1-b954-08de4ddffadf" /> <img width="310" height="280" alt="image" src="https://github.com/user-attachments/assets/57541c95-ce15-4d72-9353-0077564531d4" />

There is an indirect relationship, however there is not a strong direct correlation. The amount of art museums in a county appears to be more related to population size rather than transportation method. This result is likely due to the size of counties and its relationship with funding and tourism.



**Ethics and Limitations:**  
We are missing some possible confounding variables like tourism and county land area which could skew our results or leave aspects unaccounted for. There is also a large amount of missing values in the data which could be indicative of a possible sampling bias and therefore may be skewing the findings. As well there are some major outliers as seen in the visualizations that the conclusion does not address.  

**Sources**  
Bingham-Hall, J., & Kaasa, A. (2011). New cultural infrastructure: Can we design the conditions for culture?  
Smith, J. K. (2014). The museum effect: How museums, libraries, and cultural institutions educate and civilize society. Bloomsbury Publishing PLC.  
Teuguia, F. (2025). Navigating the legal landscape of APIs: Innovations, strategies for sustainable, inclusive, and secure digital ecosystems. World Futures, 81(4), 255-290.
