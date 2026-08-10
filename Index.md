<div align="center">

# Google Summer of Code 2026

## Final Project Report

<hr>

<img src="assets/images/gsoc-logo.png" alt="Google Summer of Code" width="150">
&nbsp;&nbsp;&nbsp;&nbsp;
<img src="assets/images/brlcad-logo.png" alt="BRL-CAD" width="150">
&nbsp;&nbsp;&nbsp;&nbsp;

<hr>

</div>

## Project

**Geometry Verification and Validation in GUI Qt**

## Organization

**BRL-CAD**

## Contributor

**Kanchan Borole**

## Mentors

**Divyanshu Garg, Himanshu Sekhar Nayak**

## Abstract

Arbalest is a Qt-based GUI application built on top of BRL-CAD. It lets engineers load 3D geometry (.g) models and run Verification and Validation (V&V) checks on them to find issues such as broken geometry, overlaps, or invalid regions.
 
For this project, I worked on rebuilding Arbalest's V&V functionality as a plugin for the current version of Arbalest, which runs on MOOSE, and used BRL-CAD's `libged` library directly to run checks.

---

## Introduction

Arbalest earlier had a working V&V prototype. This prototype was written directly inside Arbalest's core code, so the V&V logic was mixed in with Arbalest's own code, and it used MGED-based commands to run its checks.
 
My focus for this project was to bring V&V functionality into the current version of Arbalest as a **plugin**, instead of writing it directly into Arbalest's core code. Since the current version of Arbalest runs on **MOOSE** and not MGED, I moved the V&V logic to use real `libged` commands directly, instead of the old MGED-based approach.
 
---
 
## Objectives
 
- Update the old V&V prototype and bring it into the current Arbalest as a plugin, so the V&V logic can work on top of Arbalest instead of being written directly into its core code.
- Move the V&V logic from MGED to the current MOOSE-based Arbalest, using real `libged` commands to run checks and get results.
- Add a summary bar, where you can get the summary count of errors, warnings, and passed checks after a validation run.
- Improve the results panel by grouping results using QTreeView, instead of showing them as one flat list.
- Improve viewport linking, so clicking on a result highlights and shows the exact geometry issue directly in the 3D viewport.
- Build a report generator that can export the validation results in JSON, TXT, and CSV formats.
---


## Implementation Details

### Plugin Architecture
 
The first part of my work was designing a plugin architecture for Arbalest. This lets V&V functionality (and other tools in the future) be added on top of Arbalest without needing to modify Arbalest's core code directly, which is how the old prototype was built. This made the V&V code more modular and easier to maintain separately from Arbalest itself.
 
### Moving from MGED to MOOSE (libged)
 
Once the plugin structure was in place, I worked on the V&V logic itself. The old prototype ran its checks using MGED-based commands, which do not work with the current Arbalest. Since Arbalest now runs on MOOSE, I rewrote the checking logic to call `libged` commands directly, so the results (errors, warnings, geometry info) come straight from BRL-CAD's own geometry library.
 
### Features of the V&V Plugin
 
- Runs V&V validation checks on a loaded model and shows the results in a table.
- Results are grouped using QTreeView grouping, instead of a flat list.
- A summary bar shows the issue counts — errors, warnings, and passed checks.
- Clicking on a result shows the test result details in a popup.
- Viewport linking — clicking on an error highlights that geometry in the viewport, so you can directly see where the overlap or issue is.
- Report generator — generates a report of the results in JSON, TXT, and CSV formats.
### Demonstration
 
I tested the plugin on the `shipping_container.g` model.
 
[Add screenshots here — e.g. the V&V panel, the results table, and the details popup.]
 
---

### Overall Workflow


#### Demonstration

#### Results Table
 
The results table shows the V&V results, grouped by part using QTreeView, along with the summary bar showing error, warning, and passed counts.
 
![Results Table](./screenshots/results-table.png)
 
#### Viewport Linking
 
Clicking on a result highlights the exact geometry with the issue in the 3D viewport.
 
![Viewport Linking](./screenshots/viewport-linking.png)
 
#### Generated Reports
 
The report generator can export the validation results in JSON, TXT, and CSV formats.
 
- [Sample Report (JSON)](./reports/sample-report.json)
- [Sample Report (TXT)](./reports/sample-report.txt)
- [Sample Report (CSV)](./reports/sample-report.csv)
#### Tested Models
 
- Tested on `shipping_container.g`
- Tested on `havoc.g`
#### Dark Theme
 
The plugin also works correctly in Arbalest's dark theme.
 
![Dark Theme](./screenshots/dark-theme.png)
 
---


![GED Console](assets/images/ged-console.png)

<video controls width="100%">
  <source src="assets/videos/ged-console-demo.mp4" type="video/mp4">
</video>

### `shipping_container.g`

*Describe how the implementation behaves when working with the `shipping_container.g` model.*

![Shipping Container](assets/images/shipping-container.png)

<video controls width="100%">
  <source src="assets/videos/shipping-container-demo.mp4" type="video/mp4">
</video>

### `havoc.g`

*Describe how the implementation behaves when working with the `havoc.g` model.*

![Havoc](assets/images/havoc.png)

<video controls width="100%">
  <source src="assets/videos/havoc-demo.mp4" type="video/mp4">
</video>

### GUI Improvements

*Describe the GUI-related improvements made during the project, including changes to styling, portability, themes, widgets, or other relevant areas.*

### Testing and Validation

*Describe how the implementation was tested, which models and scenarios were used, and how the resulting functionality was validated.*

---

## Contributions

The major contributions made during the project are summarized below.

#### Pull Requests

<div align="center">

<table>
    <thead>
        <tr>
            <th>Date of Merge</th>
            <th>Pull Request</th>
            <th>Status</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>June 8th, 2026</td>
            <td><a href="https://github.com/BRL-CAD/arbalest/pull/76"> [BRL-CAD/arbalest/PR#76]</a></td>
            <td>Merged</td>
            <td>Initial Geometry Verification & Validation UI/workflow integration.</td>
        </tr>
        <tr>
            <td>July 1, 2026</td>
            <td><a href="https://github.com/BRL-CAD/arbalest/pull/77"> [BRL-CAD/arbalest/PR#77]</a></td>
            <td>Merged</td>
            <td>Add V&V plugin with MOOSE CommandString integration
</td>
        </tr>
        
  
</table>

</div>

---

## Conclusion

*Summarize the work completed during the project, the major outcomes, and how the implementation addresses the objectives defined at the beginning of the project.*

---

## Future Work

The work completed during the project provides a foundation for further improvements. Some possible areas of future development include:

* *Future improvement or extension.*
* *Additional functionality that could be implemented.*
* *Further integration or refinement.*
* *Additional testing or optimization.*

---

## Acknowledgements

I would like to sincerely thank my mentors, the BRL-CAD community, and everyone who contributed to the development and review of this project throughout Google Summer of Code 2026.

*Add any specific acknowledgements here.*

---

## References

* [BRL-CAD Official Website](https://brlcad.org/)
* [BRL-CAD GitHub Organization](https://github.com/BRL-CAD)
* [BRL-CAD GitHub Repository](https://github.com/BRL-CAD)
* [BRL-CAD Documentation](https://brlcad.org/wiki/)
* [Google Summer of Code](https://summerofcode.withgoogle.com/)
* [Google Summer of Code Contributor Guide](https://developers.google.com/open-source/gsoc)
* *Relevant BRL-CAD documentation*
* *Relevant GitHub issues and pull requests*
* *Other technical references used during the project*
