# 005: The duplicated absorbance spectra of plates p7 and p8

- **Status:** active
- **Created:** 2026-11-22
- **Updated:** 2026-11-22
- **Due:** 2026-11-23

## Goal

Know which plate the absorbance spectra shared by p7 and p8 belong to, and what leaving either plate or both out costs the analysis. Then record the decision as a step in `CsPbBr_transitions.ipynb`, with the data file left as downloaded.

## Progress log

*2026-11-22.* While counting thickness labels per plate in Exploration, found that p7 and p8 have the same count in every column. Their 96 absorbance spectra are identical value for value, and so are the deconvolution fractions computed from them, the only such pair in the file. Their recipes differ in all 96 wells (p7 is at 50 °C with standard Br, p8 at 30 °C with [Br] 0.42 to 1.70 mM), and so do their emission spectra. Metadata.pdf gives both plates the date 2019-07-25.

*2026-11-22.* Tested which plate the absorbance belongs to.

- **Layout cannot decide it.** The two plates share their Pb and OLA layout, and p7's Cs volume and p8's Br volume correlate at r = 0.69 across wells, so a trend in the spectra fits either recipe.
- **Emission decides it.** Each plate's emission was recorded separately, so I used it as an independent check. On the 13 other plates, the emission peak of wells with each absorbance label has a median of 431 nm (1 ML), 433 nm (2 ML), 460 nm (3 ML), 482 nm (4 ML), and 507.5 nm (bulk). Each well was labelled by the nearest of these peaks. On the 11 of those plates tested, that label matches the absorbance label in 58 to 100% of wells with emission above 500 counts. The shared absorbance labels match p7's emission in 54% of 59 wells and p8's emission in 20% of 56, far below every other plate.
- **Stoichiometry agrees.** p8's own emission falls about 35-fold from the highest Br to the lowest (median maximum 20098 to 578 counts). At [Br] 0.42 mM there are about 0.5 to 1 Br per Pb, against the 3.5 a 2 ML plate (CsPb₂Br₇) needs, so little platelet should form. Yet the shared spectra hold a similar platelet absorbance at every p8 Br level (median 0.30 to 0.50 O.D.).
- **One weak test.** The emission intensity correlates with the shared platelet absorbance at Spearman 0.51 for p7 and 0.40 for p8. Both lie within the 0.31 to 0.67 of the five other plates checked (p4, p5, p6, p9, p21), so this test does not decide.

Conclusion: the spectra are most likely p7's, and p8's real absorbance is missing from the published file.

*2026-11-22.* Listed what leaving both plates out would cost.

- **Wells.** 192 of 1351 (14%). The labelled wells at `PURITY_MIN` 0.5 drop from 737 to 615, since the 61 labelled wells of each plate are the same spectra counted twice.
- **Temperature.** p7 is the only plate at 50 °C, so the range shrinks to 30 to 40 °C, with 35 and 40 °C one plate each.
- **Bromide.** p8 is the only plate below 8.48 mM, so the [Br] range shrinks from 0.42–16.96 mM to 8.48–16.96 mM. The only remaining Br variation is on p0, at one [OLA] (3.65 mM) and one stir rate (800 rpm). The Br-starved regime disappears, and [Br] is one of the five concentrations in the question.
- **Whole-plate test.** It would have 13 plates instead of 15 and lose its two extrapolation tests (50 °C and low Br). Keeping both plates is worse: holding out one leaves its identical spectra in the training set, a leak that inflates the score.
- **First analysis.** Unaffected, since neither plate is in the base set.
- **Exciton energy.** It loses 61 labelled wells, 4 of them 4 ML.

The assistant wrote and ran the code for the second and third entries. It is not in the notebook yet.

**Next.** Decide between keeping p7's absorbance and dropping p8's (proposed), which keeps 50 °C and loses only low Br, and dropping both. Add the emission test and the decision as cells in the notebook. Consider telling the dataset's authors about the duplicate.

## Outcome
