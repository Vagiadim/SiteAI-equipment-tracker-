# Governance + Licensing Checklist

## Privacy & consent
- Data source: construction imagery for equipment detection.
- No personal identifying information is intentionally collected.
- If faces/plates appear, the system is not designed to identify people.
  
As this system utilizes computer vision on active construction sites, the following governance protocols are established to ensure compliance with global privacy standards (GDPR/Local Regulations):

* [ ] **Anonymization:** Ensure all workers' faces and vehicle license plates are blurred if captured in high-resolution frames.
* [ ] **Data Minimization:** The system only processes images for equipment detection; no biometric or individual worker tracking data is stored or analyzed.
* [ ] **Purpose Limitation:** This AI is strictly for equipment logistics and site progress; it is prohibited for use in individual worker productivity surveillance.

## Technical Accountability
* [ ] **Reproducibility:** All training weights (`best.pt`) and hyperparameters are version-controlled in the GitHub repository to allow for third-party auditing.
* [ ] **Bias Mitigation:** The dataset includes machinery from multiple manufacturers and colors (Yellow, Orange, White) to prevent model bias toward specific brand aesthetics.
* [ ] **Edge Security:** For production deployment, processing should occur on-site (Edge AI) to reduce the risk of transmitting sensitive site imagery over public networks.

## Safety-Critical Operations (Human-in-the-loop)
* [ ] **Recall vs. Precision:** In safety-critical zones (e.g., Tower Crane swing radius), the model must be tuned for high **Recall** to ensure no machinery is missed, even at the cost of "False Positives."
* [ ] **Non-Criticality Clause:** This model is a "monitoring aid." It must NOT be used for automated safety-critical shutdowns without a human safety officer's verification.
* [ ] **Failure Mode Disclosure:** Users are notified that detection confidence drops in low-light, heavy dust, or night-shift conditions not fully represented in the v9 training set.

## Data minimization
- Only equipment classes required for the AECO objective are labeled.
- Avoid collecting unnecessary metadata (names, locations, worker identity).

## Environmental & Social Impact
* [ ] **Efficiency Optimization:** By reducing equipment idle time through AI tracking, the project aims to lower the carbon footprint of site operations.
* [ ] **Upskilling:** The deployment of this tool is intended to augment site supervisors' capabilities, transitioning manual logging tasks into high-value data analysis roles.

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





