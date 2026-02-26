# Error Analysis (Failure Modes) + Iteration Plan

## Evidence source
Examples referenced from:
- /results/val_preds/
- /results/new_preds/
- /results/curves/

## False Positives (FP) — model predicted equipment but it was wrong
1. **FP #1 (image name):**
   - What happened:
   - Likely reason (hypothesis):
2. **FP #2 (image name):**
   - What happened:
   - Likely reason (hypothesis):
3. **FP #3 (image name):**
   - What happened:
   - Likely reason (hypothesis):

## False Negatives (FN) — equipment present but model missed it
1. **FN #1 (image name):**
   - What happened:
   - Likely reason (hypothesis):
2. **FN #2 (image name):**
   - What happened:
   - Likely reason (hypothesis):
3. **FN #3 (image name):**
   - What happened:
   - Likely reason (hypothesis):

## 3 Prioritized next improvements (data-driven)
1. **Add data for [gap]**: (e.g., night/low-light, rain, backlit, distance shots)
2. **Add hard negatives**: images that look similar but are not the class (e.g., scaffolding vs crane parts).
3. **Refine labeling**: tighten/standardize boxes for [class] and add examples for occlusion/partial visibility.
