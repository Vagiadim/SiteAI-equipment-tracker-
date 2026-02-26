# Governance + Licensing Checklist

## Privacy & consent
- Data source: construction imagery for equipment detection.
- No personal identifying information is intentionally collected.
- If faces/plates appear, the system is not designed to identify people.

## Data minimization
- Only equipment classes required for the AECO objective are labeled.
- Avoid collecting unnecessary metadata (names, locations, worker identity).

## Limitations (when NOT to use)
- Not for safety-critical automation (e.g., autonomous shutdown decisions).
- Performance may degrade in: occlusion, low-light, extreme distance, unusual camera angles.

## Risk note (false negatives vs false positives)
- **False negatives are more harmful** for planning/compliance use cases because missed equipment can lead to incomplete reporting or missed hazards.
- False positives increase review workload but are easier to correct by a human reviewer.

## Licensing
- Repository code: MIT License (see LICENSE file).

## Dataset rights (must be explicit)
- Roboflow dataset: [public / licensed / owned by team]  
- Link + dataset version: [paste Roboflow link + version tag]
