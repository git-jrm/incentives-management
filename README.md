# Incentives Management

## Overview

**Incentives Management** is an enterprise-grade compensation system that automates performance-based bonus calculations by evaluating daily operational objectives through the OKR (Objectives and Key Results) methodology.

Instead of managing granular tasks, the architecture maps each business day as a high-level **Objective**, where the scheduled daily goals act as quantitative **Key Results**. 

The system features a real-time computation engine that tracks completion rates and time-bound compliance, programmatically triggering financial incentives and bonus eligibility as soon as the daily objective is marked as completed through the fulfillment of its activities (goals).

This is the MVP wireframe validate with stakeholder:

#### DESKTOP
```text
+--------------------------------------------------------------------------------------------------------------+
| OCTOBER 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁             |
| NOVEMBER 😁 🙂 😐                                                                                            |
+--------------------------------------------------------------------------------------------------------------+
|   sun 1/11  |   mon 2/11  |   tue 3/11  |                wednesday 4/11     | thu 5/11 | fri 6/11 | sat 7/11 |
+-------------+-------------+-------------+-----------------------------------+----------+----------+----------+
| ☑️ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (FF)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
| ☑️ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (MM)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
| ☑️ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (JJ)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
|             | ☑️ GOAL (X) | ☑️ GOAL (X) |                                   | GOAL (X) | GOAL (X) |          |
|             | ☑️ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X)                       | GOAL (X) | GOAL (X) |          |
|             | ☑️ GOAL (X) | ✔️ GOAL (X) | ☑️ GOAL (X)                       |          |          |          |
|             | ✔️ GOAL (X) | ✖️ GOAL (X) | ✔️ GOAL (X)                       |          |          |          |
+-------------+-------------+-------------+-----------------------------------+----------+----------+----------+
| ☑️ In-time      ✔️ Done      ✖️ Not done      😁 All in time      🙂 All done      😐 Something left undone  |
+--------------------------------------------------------------------------------------------------------------+
```

#### MOBILE
```text
+------------------------------------+
| NOVEMBER 😁 🙂 😐                  |
+------------------------------------+
|           wednesday 4/11           |
+------------------------------------+
| [GOAL (X)]  [GOAL (X)]  (FF)  [+]  |
| [GOAL (X)]  [GOAL (X)]  (MM)  [ ]  |
| [GOAL (X)]  [GOAL (X)]  (JJ)  [ ]  |
|                                    |
| ☑️ GOAL (X)                        |
| ☑️ GOAL (X)                        |
| ✔️ GOAL (X)                        |
+------------------------------------+
| ☑️ In-time   ✔️ Done   ✖️ Not done |
| 😁 All in time    🙂 All done      |
| 😐 Something left undone           |
+------------------------------------+
```

Each GOAL have own and range of values for example:
- 9:00 - 10:00 hrs : 20000
- 10:00 - 11:00 hrs : 16000
- 11:00 - 12:00 hrs : 15000
- 12:00 - 13:00 hrs : 14000





