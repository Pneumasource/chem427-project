# 004: Choose PURITY_MIN, the share of absorbance that gives a well a thickness label

- **Status:** active
- **Created:** 2026-11-22
- **Updated:** 2026-11-22
- **Due:** 2026-11-23

## Goal

A value of `PURITY_MIN` justified from the data. That means knowing, for 0.3, 0.5, and 0.7, how many labelled wells in the base set are really mixtures of two thicknesses, how many are diluted by non-platelet species, and how many rest on an unstable deconvolution. The value chosen, and its reason, goes in the Parameters cell of `CsPbBr_transitions.ipynb`.

## Progress log

*2026-11-22.* Compared the three purity cutoffs on the labels from the thickness-label cell of the first analysis (cell 18 in VS Code), in the base set of 915 wells (30 °C, [Br] 12.72 mM, without the 15 low-volume p14 wells). A labelled well counts as *mixed* if its second-largest thickness holds at least 0.25 of the absorbance, or comes within 0.1 of the largest. Its fit counts as *unstable* if the deconvolution R² is below 0.9, or the fit took more than 1000 iterations (the 96th percentile is 940).

| PURITY_MIN | labelled | second thickness ≥ 0.25 | top two within 0.1 | R² < 0.9 | iterations > 1000 |
|---|---|---|---|---|---|
| 0.3 | 591 | 159 (27%) | 36 | 43 (7.3%) | 16 |
| 0.5 | 478 | 128 (27%) | 17 | 36 (7.5%) | 9 |
| 0.7 | 293 | 20 (7%) | 0 | 14 (4.8%) | 3 |

*2026-11-22.* Split the wells into bands by the share of their dominant thickness, to see where each problem comes from. The two problems sit in different bands.

| band | wells | platelets' total share (median) | second thickness ≥ 0.25 | R² < 0.9 | iterations > 1000 |
|---|---|---|---|---|---|
| 0.3 to 0.5 | 113 | 0.58 | 27% | 6.2% | 6.2% |
| 0.5 to 0.7 | 185 | 0.92 | 58% | 11.9% | 3.2% |
| 0.7 and above | 293 | 0.97 | 7% | 4.8% | 1.0% |

- **0.3 to 0.5: platelets mixed with other species.** These wells are mixed with non-platelet species rather than with a second thickness: a median of 42% of their absorbance is non-platelet. Of the 113, 85 have a platelet as their largest component of all 12. Their largest non-platelet components are Cs₄PbBr₆ (28), background (23), CsPb₂Br₅ (23), PbBr₂ (21), and PbBr₃⁻ (18). They also take the most iterations to fit (6.2% over 1000).
- **0.5 to 0.7: two thicknesses mixed.** These are platelet wells (92% platelet absorbance) split between two thicknesses. 58% hold a second thickness of 0.25 or more, and every such second thickness is adjacent: 1 ML with 2 ML in 76 wells, 2 ML with 3 ML in 24, 3 ML with 4 ML in 6, and 2 others, 108 in all. This band also has the highest share of low R², 11.9%. That falls on the 1 ML and 2 ML labels, 25% and 12% of which have R² below 0.9, while 3 ML, 4 ML, and bulk have none.
- **0.7 and above: largely clean.** Only 7% hold a second thickness of 0.25 or more, none are near ties, and 4.8% have R² below 0.9.

So thickness mixing and the least stable fits remain at a cutoff of 0.5 or below, carried by the 1 ML and 2 ML wells of the 0.5 to 0.7 band. A cutoff of 0.3 adds wells diluted by non-platelet species. Raising the cutoff from 0.5 to 0.7 removes 185 wells, 108 of them mixed and 22 with R² below 0.9. It also removes the wells that lie on a thickness boundary, and in the first analysis that lowered the share of `[Cs]` steps that make the product thicker from 22% to 16%, and of `[Pb]` steps from 16% to 9%. The direction of every effect was the same at all three cutoffs.

The assistant wrote and ran the code for both entries. It is not in the notebook yet.

**Next.** Put the comparison in a cell under Checking the assumptions. Decide between 0.5, which keeps the boundary wells and states their mixing as a limit, and 0.7, which keeps clean labels and treats the trend shares as lower bounds. Check whether the low-R² 1 ML wells change any conclusion.

## Outcome
