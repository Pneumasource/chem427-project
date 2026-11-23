# Judgment log: 

## How I used AI in this project

(Final submission only.)

## Entries

### Nov 22: Absorbance cutoff for thickness categories (PURITY_MIN)

- **What the assistant suggested:** Set the PURITY_MIN = 0.5
- **What I did:** verified.
- **Why, from my data:** For 1-4 mL and bulk, label_well function finds the maximum absorbance among five, and assigns the corresponding thickness category only if the absorbance is greater than PURITY_MIN (unlabelled otherwise). For PURITY_MIN of 0.3, 0.5, and 0.7:
1. the number of labelled wells are 591, 478, and 293
2. the absorbance median lies in non-platelet region for 0.3 < PURITY_MIN < 0.5
3. the thickness labels (mainly 1 and 2 mL) become increasingly ambiguous, and R^2 < 0.9 for 0.5 < PURITY_MIN < 0.7
Because PURITY_MIN lies between two intervals, there is no need for loss of 

### Nov 22: Treatment of p7 and p8 with identical absorbance spectrum

- **What the assistant suggested:** Determine the absorbance spectrum as p7 and include it instead of p8.
- **What I did:** verified.
- **Why, from my data:** 
1. The shared absorbance spectrum (approximated from emission spectrum) matches 54% with that of p7 and 20% with p8 (58-10% for other plates), and the platelet absorbance of p7 show proportionality of *(1/35) for the lowest [Br] while p8 has almost no observable proportionality.
2. Removing both p7 and p8 abstracts 192 plates from total unlabeled plates of 1351 (14% loss), which also abstracts 122 plates from total labeled plates of 737 (17% loss); also, 50°C plates completely disappear, leaving only 30-40°C plates.