# Uncertainty-Aware Imitation Learning for Chemistry Lab Automation

### Laura Jones, Gabriella Pizzuto, Andrew Cooper

### University of Liverpool | Contact: [Laura.Jones@liverpool.ac.uk](mailto:Laura.Jones@liverpool.ac.uk)

Chemistry laboratory automation demands robust robotic manipulation for safety critical applications where errors can result in chemical spills, equipment damage, or safety hazards. Traditional imitation learning approaches lack failure prediction mechanisms, making them unsuitable for deployment in settings where intervention costs are asymmetric—false negatives (missed failures) are far more costly than false positives (unnecessary interventions).

We propose an uncertainty-aware imitation learning framework that combines ensemble-based epistemic uncertainty estimation with data-driven intervention thresholds. Our system uses an ensemble of imitation learning policies, where action variance across the ensemble serves as a proxy for model uncertainty.

The key innovation lies in our calibration methodology: we allocate the slow calibration process to an offline process where we execute policy rollouts without intervention, recording action variance trajectories for both successful and failed executions. Using kernel density estimation on these distributions, we establish the action variance confidence interval that discriminates between nominal and high-uncertainty regions  [1]. We then optimize detection parameters—specifically, sliding window size and peak count thresholds—to maximize balanced accuracy between true positive detection (catching failures) and false positive rate (minimizing unnecessary interventions). This optimization is performed per action component, accounting for 6 degrees of freedom uncertainty.

During deployment, the system monitors action variance in real-time using the calibrated sliding windows. When variance exceeds the threshold for a persistent number of timesteps, control transfers to a backup safety policy, preventing catastrophic failures before they occur.

We evaluate our approach on chemistry laboratory-based tasks using the IsaacLab simulation framework [2]. Our results demonstrate that calibrated intervention significantly improves success rate on tasks, taking a policy success rate from 75% to 95%.

This work provides a practical framework for deploying imitation learning in high-stakes robotics applications where safety and reliability are paramount. The data-driven calibration approach is domain-agnostic and can be adapted to any ensemble-based policy architecture, while the uncertainty-aware switching logic enables human-in-the-loop operation without requiring online learning or reward engineering.

### References

[1] Z. Zhu, S. Wang and H. Zhao, "Uncertainty-aware Deep Imitation Learning and Deployment for Autonomous Navigation through Crowded Intersections," 2024 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), Abu Dhabi, United Arab Emirates, 2024, pp. 13980-13987, doi: 10.1109/IROS58592.2024.10801536.

[2] K. Darvish, A. Sohal, A. Mandal, H. Fakhruldeen, N. Radulov, Z. Zhou, S. Veeramani, J. Choi, S. Han, B. Zhang, J. Chae, A. Wright, Yijie Wang, H. Darvish, Y. Zhao, G. Tom, H. Hao, M. Bogdanovic, G. Pizzuto, A. I. Cooper, A. Aspuru Guzik, F. Shkurti, A. Garg, MATTERIX: Towards a Digital Twin for Robotics-Assisted Chemistry Lab Automation, Nature Computational Science (in press).

