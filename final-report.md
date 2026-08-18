<div align="center">

# Google Summer of Code 2026 -  Final Project Report

</div>

---
## Project

**Geometry Verification and Validation GUI in Qt**

## Organization

**BRL-CAD**

## Contributor

**Kanchan Borole**

## Mentors

**Divyanshu Garg, Himanshu Sekhar Nayak**

## Abstract

Arbalest is a Qt-based GUI application built on top of BRL-CAD. This project focuses on the Verification and Validation (V&V) part of Arbalest — checking 3D geometry (.g) models for issues such as broken geometry, overlaps, or invalid regions.
 
For this project, I worked on rebuilding Arbalest's V&V functionality as a plugin for the current version of Arbalest, which runs on MOOSE, and used `libged` commands directly to run checks.

---

## Introduction

Arbalest earlier had a working V&V prototype. This prototype was written directly inside Arbalest's core code, so the V&V logic was mixed in with Arbalest's own code, and it used MGED. While it started within Arbalest, the V&V GUI ended up becoming its own application fork over time.
 
My focus for this project was to separate the V&V domain logic out of Arbalest's core code and bring it into the current version of Arbalest as a **plugin**, instead of it being written directly into Arbalest's core code. As part of this, the V&V logic was also migrated from the old MGED-based approach to work with the current MOOSE-based Arbalest.
 
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
 
The first part of my work was designing a plugin architecture for Arbalest. This lets V&V functionality (and other tools in the future) be added on top of Arbalest without needing to modify Arbalest's core code directly. This made the V&V code more modular and easier to maintain separately from Arbalest itself.
 
### Moving from MGED to MOOSE
 
Once the plugin structure was in place and UI Integration done, I worked on the V&V logic. The old prototype ran its checks using `libged` commands and uses mged, which do not work with the current Arbalest. Since Arbalest now runs on MOOSE, I rewrote the checking logic to call `libged` commands and get the results and then added features like visual linking, more info popup, etc.

### Verification & Validation Workflow

The validation workflow begins after loading a model geometry into Arbalest. The user can select the required validation checks according to their needs and run them. Once the checks are completed, the results are displayed in a table along with a summary showing the number of errors, warnings, and passed checks.

The results can be filtered by category, allowing users to view all results or only errors, warnings, or passed checks. By selecting a particular result, user can visualize the corresponding geometry or object in the 3D viewport and view additional information about that result. Finally, the validation results can be generated as a report, which can be used to review the identified issues and assist in correcting the model geometry.

### Features of the V&V Plugin
 
- Runs V&V validation checks on a loaded model and shows the results in a table.
- Results are grouped using QTreeView grouping, instead of a flat list.
- A summary bar shows the issue counts — errors, warnings, and passed checks.
- Clicking on a result shows the test result details in a popup.
- Viewport linking — clicking on an error highlights that geometry in the viewport, so you can directly see where the overlap or issue is.
- Report generator — generates a report of the results in JSON, TXT, and CSV formats.

## Demonstration

### Results Table
 
The results table shows the V&V results, grouped by part using QTreeView, along with the summary bar showing error, warning, and passed counts.
 
![Results Table](./assets/img/Verification&ValidationTable.png)
 
### Viewport Linking
 
Clicking on a result highlights the exact geometry with the issue in the 3D viewport.
 
![Viewport Linking](./assets/img/VisualizeObject1.png)
![Viewport Linking](./assets/img/VisualizeObject2.png)

 
### Generated Reports
 
The report generator can export the validation results in JSON, TXT, and CSV formats.
 
- [Sample Report (CSV)](./assets/report/sample_report.csv)
- [Sample Report (TXT)](./assets/report/sample_report.txt)
- [Sample Report (JSON)](./assets/report/sample_report.json)

### Tested Models


### `shipping_container.g`

The V&V functionality was tested on the `shipping_container.g` model. Clicking the **V&V** option runs the V&V checks and displays the test results, which can be filtered by **Errors, Warnings, and Passed tests**. Clicking an error or test result visualizes the corresponding part of the model, and the Test Result Details popup provides additional information. We can also generate the report in three different formats.

[assets_video_Shipping_container.webm](https://github.com/user-attachments/assets/d29c48f3-ac34-43f1-bb91-5f2dc2812a81)



### `havoc.g`

The V&V functionality was tested on the `havoc.g` model. Clicking the **V&V** option runs the V&V checks and displays the test results, which can be filtered by **Errors, Warnings, and Passed tests**. Clicking an error or test result visualizes the corresponding part of the model, and the Test Result Details popup provides additional information. We can also generate the report in three different formats.

[assets_video_havoc.webm](https://github.com/user-attachments/assets/0a18205f-1383-4342-a4e7-da04ff93926f)



---

## Contributions

The contributions made during the project are summarized below.



<div align="center">

<table>
    <thead>
        <tr>
            <th>Pull Request</th>
            <th>Description</th>
            <th>Work Done</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://github.com/BRL-CAD/arbalest/pull/76"> BRL-CAD/arbalest/PR#76</a></td>
            <td>Initial Geometry Verification & Validation UI/workflow integration.</td>
            <td>V&V UI component integration under src/plugins/vv/ui/, V&V panel and dock widget integration, grouped validation result handling, validation summary handling, context menu integration, export support</td>
        </tr>
        <tr>
            <td><a href="https://github.com/BRL-CAD/arbalest/pull/77"> BRL-CAD/arbalest/PR#77</a></td>
            <td>Add V&V plugin with MOOSE CommandString integration</td>
            <td>This adds the Geometry V&V plugin using BRLCAD::CommandString::Parse() for running validation tests on BRL-CAD geometry. The test selection dialog is updated with grouped tests using getDoubleGroupedTestSuites(). Added getMemoryDatabase() in Document.h for writable database access.</td>
        </tr>
        <tr>
            <td><a href="https://github.com/BRL-CAD/arbalest/pull/78"> BRL-CAD/arbalest/PR#78</a></td>
            <td>UI/UX Improvements for Geometry Verification & Validation</td>
            <td>Added Dark Theme support for VV widget, Implemented Progress Bar, Improved Results Table and added UI icons, Fixed tab switching state handling.</td>
        </tr>
        <tr>
            <td><a href="https://github.com/BRL-CAD/arbalest/pull/79"> BRL-CAD/arbalest/PR#79</a></td>
            <td>Added test result details popup</td>
            <td>Added a test result details view that allows users to easily inspect passed tests and errors from the V&V results table. Users can right-click or click on a test result to view its complete details in a pop-up.</td>
        </tr>
        <tr>
            <td><a href="https://github.com/BRL-CAD/arbalest/pull/80"> BRL-CAD/arbalest/PR#80</a></td>
            <td>Added Visual Linking Feature</td>
            <td>Added a context menu action allowing users to right-click on a test/error item and instantly view the corresponding object/geometry in the 3D viewport.</td>
        </tr>
        <tr>
            <td><a href="https://github.com/BRL-CAD/arbalest/pull/81"> BRL-CAD/arbalest/PR#81</a></td>
            <td>Improve report generation and export logic</td>
            <td>Implemented report export functionality that allows users to generate and export the report in three formats: JSON, TXT, and CSV. This makes it easy for users to save and use the generated report in their preferred format.</td>
        </tr>
        
  
</table>

</div>

---

## Conclusion

This project brings V&V functionality into Arbalest as a plugin, built on the current MOOSE-based Arbalest. The V&V plugin runs validation checks, shows grouped results with a summary bar, show error object/geometry in the 3D viewport, and generates report. It helps validate models through checks such as duplicate IDs, overlapping regions, null regions, solid outside of region, Nested regions, and other validation checks, making it easier to identify and review issues in the model.

---

## Future Work

The work completed during the project provides a foundation for further improvements. Some possible areas of future development include:

- **AI integration** — using AI to automatically detect geometry issues or suggest fixes, as a long-term possibility for the project.
- **Per-object severity icons in 3D viewer** — a small color marker directly on the geometry object, so problem areas are visible without opening the results panel.
- **Checking for more issues** — new validation checks beyond what currently exists, such as duplicate object names or invalid region IDs.
- **Geometry repair workflow** — a way to fix common issues directly from the GUI instead of manually editing the model.

---

## Acknowledgements

I am grateful to Sean Morrison, Daniel Rossberg, Divyanshu Garg, Himanshu Sekhar Nayak, and the whole BRL-CAD community for their guidance and support throughout this GSoC period. 

Their feedback at every step helped me understand the project better and stay on the right track. I am thankful for such a supportive and active open-source environment, and I have learned a lot throughout this GSoC journey. 

I hope to continue contributing to BRL-CAD beyond this GSoC period.

---

## References

- BRL-CAD's Arbalest Repository: [https://github.com/BRL-CAD/arbalest](https://github.com/BRL-CAD/arbalest)
- Daily Logs: [https://github.com/KanchanBorole/gsoc-2026-brlcad-vv/blob/main/Daily%20Logs.md](https://github.com/KanchanBorole/gsoc-2026-brlcad-vv/blob/main/Daily%20Logs.md)
- V&V Reference(Old Fork): [https://brlcad.org/design/v&v/](https://brlcad.org/design/v&v/)
- Old V&V Fork: [https://github.com/isaacy13/arbalest](https://github.com/isaacy13/arbalest)
- BRL-CAD Repository: [https://github.com/BRL-CAD/brlcad](https://github.com/BRL-CAD/brlcad)
- BRL-CAD's MOOSE Repository: [https://github.com/BRL-CAD/MOOSE](https://github.com/BRL-CAD/MOOSE)
- Additional Information: [https://github.com/KanchanBorole/gsoc-2026-brlcad-vv](https://github.com/KanchanBorole/gsoc-2026-brlcad-vv)

---
