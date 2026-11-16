# BEV CAN Attack Dataset

The dataset available in this repository contains the vehicle and CAN data used in our paper: **Detecting Attacks on Electric Vehicle Battery Management Systems and Powertrain Control: From Residual Checks to Black-Box Machine Learning**.

## Experiments and data collection

The dataset was generated using an extended Simulink battery electric vehicle (BEV) model and contains nominal and attacked traces recorded under two homologation driving cycles: WLTC Class 3b and FTP75.

**Driving cycles:** Two driving scenarios were used to evaluate the attacks and detection methods:

- **WLTC Class 3b**
- **FTP75**

**Vehicle architecture:** The simulated BEV architecture includes the Battery Management System (BMS), Vehicle Control Unit (VCU), Charger Control Unit (CCU), front and rear Motor Control Units (MCUs), Instrument Cluster (IC), HVAC controller, driver interface, and battery pack.

**Attack targets:** The attacks are applied to safety- and operation-relevant signals exchanged over the CAN bus:

- **Battery state of charge (SoC)**
- **Battery voltage (BatVolt)**
- **Battery temperature (Temp)**
- **Torque command (Tq_cmd)**

**Attack types:** Four attack types are included for each target signal:

- **Surge**
- **Bias**
- **Geometric**
- **Fuzzy**

**Threat model:** The adversary is assumed to have access to the CAN bus and can manipulate battery-state information transmitted by the BMS and torque-command messages exchanged between the VCU and the MCUs. The internal computations of the BMS and the battery-protection functions remain uncompromised.

## Dataset

**Dataset content:** The dataset contains processed CSV traces and raw CAN logs for nominal and attacked operation. The traces cover both WLTC Class 3b and FTP75 and include attacks targeting battery voltage, SoC, battery temperature, and torque-command signals.

The full release contains:

- 2 nominal traces, one for each driving cycle;
- 32 attacked traces, covering 4 target signals, 4 attack types, and 2 driving cycles;
- 34 processed CSV files in total;
- the corresponding raw CAN logs.

Due to their size, the dataset files are hosted externally and can be accessed using the following link

## Folder structure

```text
|
|------ Dataset
|       |------ BMS_IDS_Vector_replay_csv
|       |       |------ FTP75
|       |       |------ WLTC
|       |------ BMS_IDS_Matlab
|       |       |------ FTP75
|       |       |------ WLTC
```


## File structure

The processed traces are stored in CSV format. Each file contains the time-series data associated with one driving cycle and one operating condition. Column names and signal units are included in the CSV header.

The raw traces preserve the recorded CAN messages, including the timestamp, CAN identifier, payload length, and data bytes.

## File naming convention

Files follow one of these patterns:

**Nominal traces:**

```text
trace_can_no_attack_<driving_cycle>.csv
```

**Attacked traces:**

```text
trace_can_<signal>_<attack>_<driving_cycle>.csv
```

### Components

1. **`trace_can`** - Indicates that the file contains vehicle/CAN trace data.
2. **`<signal>`** - Targeted signal:
   - `BatVolt` = battery voltage
   - `SoC` = battery state of charge
   - `Temp` = battery temperature
   - `Tq_Command` = torque command
3. **`<attack>`** - Applied attack:
   - `Surge`
   - `Bias`
   - `Geometric`
   - `Fuzzy`
4. **`<driving_cycle>`** - Driving scenario:
   - `WLTC` = Worldwide Harmonised Light Vehicles Test Cycle, Class 3b
   - `FTP75` = Federal Test Procedure 75

## Examples

**Nominal trace:**

```text
trace_can_no_attack_WLTC.csv
```

Nominal vehicle and CAN data recorded during the WLTC Class 3b scenario.

**Battery-voltage attack:**

```text
trace_can_BatVolt_Surge_FTP75.csv
```

Vehicle and CAN data recorded during FTP75 while a surge attack targets the battery-voltage signal.

**State-of-charge attack:**

```text
trace_can_SoC_Geometric_WLTC.csv
```

Vehicle and CAN data recorded during WLTC Class 3b while a geometric attack targets the battery SoC signal.

**Torque-command attack:**

```text
trace_can_Tq_Command_Fuzzy_FTP75.csv
```

Vehicle and CAN data recorded during FTP75 while a fuzzy attack targets the torque-command signal.

## CAN communication matrix

The supplementary material provides the CAN communication matrix of the simulated BEV. For each signal, the matrix specifies the transmitting ECU, receiving ECU, CAN identifier, physical range, bit allocation, resolution, unit, description, and transmission period.

The main attack targets use the following messages:

| Target signal | TX ECU | RX ECU | CAN ID | Period |
|---|---|---|---|---|
| Battery SoC | BMS | VCU | `0x11E` | 10 ms |
| Battery voltage | BMS | VCU | `0x11E` | 10 ms |
| Battery temperature | BMS | VCU | `0x11E` | 10 ms |
| Battery voltage | BMS | CCU | `0x13C` | 10 ms |
| Battery temperature | BMS | CCU | `0x13C` | 10 ms |
| Torque command | VCU | Front MCU | `0x23B` | 10 ms |
| Torque command | VCU | Rear MCU | `0x24A` | 10 ms |

The complete matrix is available in [`supplementary/SUPPLEMENTARY.md`](supplementary/SUPPLEMENTARY.md).

## Supplementary material

The supplementary material contains:

- the complete CAN communication matrix;
- detailed WLTC and FTP75 results for CUSUM, Chi-Square, Energy, and EWMA detectors;
- detailed WLTC and FTP75 results for KNN, Decision Tree, Gaussian Naive Bayes, and XGBoost;
- TP, TN, FP, FN, FPR, FNR, TPR, TNR, accuracy, precision, and F1-score for each evaluated configuration.

See [`supplementary/SUPPLEMENTARY.md`](supplementary/SUPPLEMENTARY.md).

## Dataset download

Due to their size, the processed CSV traces and raw CAN logs are hosted externally.

- **Processed CSV traces:** 
- **Raw CAN logs:** 

## Contact

For any questions about our work and dataset, don't hesitate to contact us (adriana.berdich at upt.ro or bogdan.groza at upt.ro).
