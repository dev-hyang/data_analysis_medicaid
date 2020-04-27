### Followups 2020-Apr-5
> **Data part**
- [x] State level for Connecticut
- [x] County level, for Indiana/Connecticut

> **Build Github/Upload data files & Jupyter notebook (2020-Apr-12)**
- [x] Start drafting the report now
    - Start from a Outline first(Just key point): data source (how to collect, how to process, how to output)
    - Write up the details in each contents/chapter
        - population data source<br>
        - price Fee Schedule structure (medicaid (CMS + STATE (mainly)), medicare (CMS), private insurance (assupmtion-to be same as medicare, not enough time to contact the private providers))<br>
        - Take a weighted sum of the above three fee schedule. What is the wight? How to choose the weight? Why do you choose the population rate as the weights? <br>
    - Understandable to readers(hard)
    - Conclusion & Further Research direction
- [x] Build Github
- [x] Upload Final Jupyter notebook script as well as data files
- [x] Add a new state like N.Y.C. if possible rather than visualizing
- [x] Make a duplicate medicare column in the price table as private insurance amount

> *Visualization (less important) {Optional}*
- [ ] State level, nationwide %Medicaid, %Medicare, % Private visualize with COVID data from CDC. Heatmap %Medicaid. COVID map side by side; Heatmap %Medicaid, COVID map overlay circles, the size of each circle is Number of COVID cases by state
- [ ] Try the same heatmap by county (California, LA, CT) by county levle. COVID data from Johns Hopkins or CDC

> *Challenge*{optional}
- [ ] can you visualize compete with [data usa](https://datausa.io/profile/geo/connecticut#health)

https://towardsdatascience.com/a-complete-guide-to-an-interactive-geographical-map-using-python-f4c5197e23e0

2020-Apr-23
- [ ] Updates
    - [x] Title -> Estimation of physician fees adjusted for demographic data
    - [ ] 1.1 Specify the goals/objectsions instead of what of data there : 
        - such as "get total population per state/county census data", "get the medicaid enrollment data - our denominator", 
        - calculate the weighting coefficients based on the fraction of each population in state/county