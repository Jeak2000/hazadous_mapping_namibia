# Namibia MSc Project — AI Coding & Research Context

> **Purpose of this document:** This file provides persistent context to an AI coding/research agent assisting with the Namibia MSc project. It should be read before proposing code, data-processing workflows, GIS methods, or methodological decisions.
>
> **Primary use:** Assistance with Google Earth Engine (GEE), Python/PyGIS, ArcPy/ArcGIS, raster processing, hydrological analysis, remote sensing, spatial analysis, and reproducible GIS workflows.
>
> **Important:** This is a working project context. Some elements are confirmed decisions; others are candidates under investigation. Do not treat an open methodological question as a final decision.

---

## 1. Project at a glance

**Researchers**
- Jacob Hagedorn Hansen
- Johanne Søe Naldal

**University**
- Aalborg University (AAU), Copenhagen
- MSc programme: Surveying, Planning and Land Management (SPLM / cand.geom.)

**Supervisor**
- Åse Christensen

**Project period**
- Field/project stay in Namibia: August–November 2026
- Final MSc project and report are completed as part of the third semester.
- The project is a **20 ECTS MSc project**.

**NGO / project partner**
- Development Workshop Namibia (DWN)

**Study areas**
- Windhoek (WDH), Namibia
- Oshakati (OSH), Namibia

**Report language**
- English

---

## 2. Current project focus

The project focuses on **hazardous areas in urban informal settlements** in Windhoek and Oshakati, Namibia.

The current definition of a hazardous area is:

> **"Areas identified as potentially flood-prone based on terrain and hydrological characteristics."**

The project is therefore primarily concerned with the spatial relationship between:

1. Areas that are potentially susceptible to flooding during major rainfall events, based on terrain/hydrological characteristics.
2. Existing and newly developing informal settlement structures ("shacks").
3. The spatial development of informal settlements into potentially hazardous areas.

A central conceptual point is:

> **A hazardous area is not necessarily a problem if people do not occupy it. The important issue is the development or expansion of informal settlements into hazardous areas.**

The project should therefore distinguish between:
- the **existence of hazardous/flood-prone land**, and
- **human exposure created by settlement development in those areas**.

---

## 3. Intended final product

The main spatial product is intended to be a **mapping of hazardous areas in informal settlements in Windhoek and Oshakati**.

The final analysis is intentionally expected to be relatively simple and interpretable. The core idea is a spatial overlay between:

**Hazardous areas**
+
**new development / expansion of informal settlement buildings**
=
**development of informal settlements into hazardous areas**

The result should allow the project to discuss:
- where hazardous areas occur;
- where informal settlements are located relative to those areas;
- whether new settlement development is occurring inside potentially hazardous areas;
- how this differs between Windhoek and Oshakati;
- what this can tell us about the broader challenge of protecting informal settlements from climate change and extreme rainfall.

The spatial analysis itself does **not** need to be technologically or mathematically complex. Its value lies in producing a clear, defensible spatial result that can support a broader academic and planning discussion.

The broader discussion should consider how the findings relate to the challenge of making informal settlements more climate-resilient in Namibia and potentially in other African/global contexts.

**Do not over-engineer the spatial model simply to make it technically impressive.**

---

## 4. Academic scope and level

This is a **20 ECTS MSc project**, not a PhD research project.

The project has limited:
- time,
- personnel,
- computing resources,
- access to high-quality historical data,
- budget.

Therefore:

> **Prioritize simple, robust, transparent, reproducible and defensible methods over highly complex modelling.**

An AI assistant should be methodologically critical, but should also consider feasibility.

A good proposed method should ideally be:
- understandable;
- reproducible;
- achievable within an MSc project;
- based on available/open data where possible;
- spatially meaningful at the scale of informal settlements;
- possible to validate or sanity-check;
- sufficiently robust to support academic discussion.

The project may have a relatively simple spatial analysis but still produce a **large and meaningful discussion** about climate adaptation, informal settlement growth, planning, resilience and the prevention of future exposure to climate-related hazards.

---

## 5. Confirmed analytical concept

The current conceptual workflow is:

```text
DATA ACQUISITION
    ↓
GEE
    ↓
DEM/DSM + satellite imagery + other relevant spatial data
    ↓
EXPORT / LOCAL DATA
    ↓
PYTHON
    ↓
Hydrological / terrain analysis
    ↓
Hazardous-area layer
    ↓
ARCGIS / ARCPY
    ↓
Building / shack analysis and spatial overlay
    ↓
QGIS
    ↓
Final map design / cartography
    ↓
REPORT + SPATIAL PRODUCT
```

This is a **current working architecture**, not a rigid technical requirement.

The team expects:
- **Google Earth Engine (GEE):** primarily data acquisition and potentially lightweight preprocessing.
- **Python:** hydrological and raster/spatial analysis, using PyGIS-style workflows and relevant geospatial libraries.
- **ArcGIS Pro / ArcPy:** likely building/shack analysis and associated GIS processing.
- **QGIS:** final cartographic design and map production.

The exact division between Python, ArcPy and other tools may change.

---

# 6. Hazardous-area analysis

## 6.1 Definition

The operational definition is:

> **Areas identified as potentially flood-prone based on terrain and hydrological characteristics.**

The analysis is currently expected to use terrain/hydrological indicators such as:
- elevation;
- slope;
- flow direction;
- flow accumulation;
- drainage patterns;
- topographic depressions / low-lying areas;
- potentially other simple terrain-derived variables if justified.

The final hazardous-area classification has **not yet been fully designed**.

The project does **not currently plan to use rainfall data as a major modelling input**.

### Important distinction

The absence of rainfall modelling does **not** mean that rainfall is irrelevant to the project. The project context concerns flooding during major/extreme rainfall events, but the current spatial hazard model is intended to identify areas that are **potentially flood-prone based on terrain and hydrological characteristics**, rather than building a full rainfall-runoff or hydraulic flood model.

Do not automatically introduce:
- return-period modelling;
- extreme-value statistics;
- detailed rainfall intensity-duration-frequency analysis;
- complex hydraulic simulation;

unless the researchers explicitly decide that these are needed.

---

## 6.2 Expected hydrological workflow

A likely conceptual workflow is:

```text
DEM / DSM
   ↓
Preprocessing / quality check
   ↓
Slope
   ↓
Flow direction
   ↓
Flow accumulation
   ↓
Drainage / concentrated flow paths
   ↓
Potentially flood-prone areas
   ↓
Hazardous-area layer
```

This is a conceptual starting point, not a fixed algorithm.

The AI should help determine which processing steps are scientifically justified and which are unnecessary.

---

# 7. DSM vs DTM — important open methodological question

The project team is specifically considering the use of a **Digital Surface Model (DSM)** rather than automatically assuming that a bare-earth Digital Terrain Model (DTM) is preferable.

This matters because the informal settlements have a relatively high building density.

A DSM represents the surface including features such as:
- buildings;
- vegetation;
- infrastructure.

A DTM attempts to represent the underlying bare terrain.

For this project, buildings may have two competing interpretations:

1. **Real hydraulic features:** Buildings can physically obstruct, redirect or concentrate surface water.
2. **DEM/DSM artefacts:** At 30 m resolution, individual buildings may create elevation effects that do not accurately represent the actual drainage behaviour of water at settlement scale.

Therefore, the project should **not assume in advance that DSM or DTM is automatically correct**.

The preferred approach is to investigate:
- data characteristics;
- vertical accuracy;
- spatial resolution;
- behaviour in dense informal settlements;
- differences between available DSM/DTM products;
- effects on slope and flow accumulation;
- whether the resulting hazardous areas are sensitive to the elevation dataset.

If feasible, a DSM/DTM comparison could be used as a methodological sensitivity check.

---

# 8. Current elevation-data candidates

The following datasets have been identified in Google Earth Engine.

## 8.1 Copernicus DEM GLO-30 (2024_1)

**Current primary candidate**

- ~30 m spatial resolution
- Digital Surface Model (DSM)
- Global coverage
- Available in GEE

GEE catalogue:
https://developers.google.com/earth-engine/datasets/catalog/COPERNICUS_DEM_GLO30_2024_1

Current thinking:
- Strong candidate for primary terrain/surface analysis.
- Particularly relevant because it is a DSM.
- Must still be assessed for suitability in Windhoek and Oshakati.

Do not treat it as automatically optimal simply because it has 30 m resolution.

---

## 8.2 NASA SRTM 30 m

- ~30 m spatial resolution
- SRTM elevation dataset
- Available in GEE

GEE catalogue:
https://developers.google.com/earth-engine/datasets/catalog/USGS_SRTMGL1_003

Potential use:
- Alternative elevation dataset.
- Potential validation/sensitivity comparison against Copernicus GLO-30.

---

## 8.3 WWF HydroSHEDS 3 arc-second conditioned DEM

- ~3 arc-seconds (~92 m)
- Hydrologically conditioned elevation dataset
- Derived from SRTM
- Designed particularly for hydrological/drainage applications.

GEE catalogue:
https://developers.google.com/earth-engine/datasets/catalog/WWF_HydroSHEDS_03CONDEM

Important warning from the dataset description:
The conditioning process alters the original DEM and can make it unsuitable for applications other than deriving drainage directions.

Potential use:
- Hydrological reference/sanity check.
- Not currently preferred as the primary settlement-scale elevation surface.

---

## 8.4 GMTED2010

- ~7.5 arc-seconds (~232 m) for the relevant product
- Global elevation dataset
- Available in GEE

GEE catalogue:
https://developers.google.com/earth-engine/datasets/catalog/USGS_GMTED2010_FULL

Potential use:
- Regional-scale reference only.
- Currently not considered appropriate as the primary dataset for settlement-scale hazardous-area analysis because of its coarse resolution.

---

# 9. Satellite imagery and building analysis

A second major analytical component is a **building/shack-development study**.

The purpose is to complement the hazardous-area analysis.

The conceptual logic is:

> Hazardous areas can exist without being problematic. The concern is when settlement development occurs inside them.

Therefore, the building analysis should ideally identify:
- existing settlement/building distribution;
- new development over time;
- spatial expansion;
- the relationship between new development and hazardous areas.

---

## 9.1 Two candidate approaches

The project team has **not yet decided** between two broad approaches.

### Candidate A — High-resolution individual shack detection

Use approximately **1–2 m imagery**, where individual shacks may be identifiable.

Potential outputs:
- individual building/shack locations;
- building footprints;
- shack count;
- new shack locations;
- temporal change in individual structures.

ArcGIS Pro has tools/workflows that may assist with building extraction and deep-learning-based image analysis.

However:

> **Do not assume this approach is feasible until appropriate imagery, historical coverage, licensing and spatial resolution have been assessed.**

The most important issue is likely **data availability**, especially for historical dates and for both WDH and OSH.

---

### Candidate B — Lower-resolution built-up / building-mass analysis

Use lower-resolution imagery where individual shacks cannot reliably be identified.

Instead of counting individual shacks, analyse:
- built-up area;
- building density;
- spatial extent of settlement;
- change in building mass over time.

Advantages may include:
- easier data acquisition;
- potentially better historical coverage;
- simpler processing;
- potentially more scalable.

Disadvantage:
- it cannot provide a precise individual shack count.

---

## 9.2 Current satellite-data candidate

**Sentinel-2** is currently being considered in GEE.

Potential uses:
- background imagery;
- built-up area analysis;
- settlement development analysis;
- potentially building-mass change detection.

However, Sentinel-2 is **not assumed to be sufficient for individual shack detection**.

The project team is still looking for better alternatives, particularly for high-resolution and historical imagery.

The AI should actively consider:
- spatial resolution;
- temporal coverage;
- cloud cover;
- historical availability;
- licensing/cost;
- suitability for individual shack detection versus building-mass analysis.

Do not recommend expensive commercial imagery without considering whether it is necessary and whether archive coverage actually exists for the required locations/dates.

---

# 10. Rainfall data

At present:

> **Rainfall data is NOT planned as a major component of the spatial analysis.**

The project has limited time and resources and does not want to spend a large part of the project on rainfall modelling.

Possible datasets such as CHIRPS or GPM may be useful for contextual/background purposes if needed, but they should not automatically be incorporated into the core model.

Do not expand the project into a major precipitation/extreme-event analysis unless explicitly requested.

---

# 11. Fieldwork

Fieldwork is important, but it has a specific role.

Field observations, interviews and surveying are primarily intended to:

- support the interpretation of the spatial analysis;
- validate/sanity-check spatial findings;
- understand local conditions;
- provide local/community knowledge;
- identify issues that may not be visible in remote-sensing/GIS data.

Fieldwork data is **not currently intended to be a direct input layer in the spatial hazard model**.

The project may involve:
- visits to informal settlements;
- interviews/conversations;
- observations;
- handheld GPS;
- surveying equipment;
- documenting settlement layout and flooding-related conditions.

The AI should not assume that field observations are quantitative training data unless explicitly instructed.

---

# 12. Wider academic perspective

The spatial analysis is only one part of the project.

The broader project concerns:
- climate change;
- extreme rainfall;
- informal settlements;
- urban resilience;
- climate adaptation;
- planning;
- vulnerability/exposure;
- prevention of climate-related impacts;
- water management;
- potentially nature-based solutions and urban green infrastructure.

The original project proposal also considered theories/perspectives including:
- urban resilience;
- wicked problems;
- nature-based solutions;
- urban green infrastructure;
- participatory planning;
- Flexible Land Tenure System (FLTS);
- Land Administration for Sustainable Development;
- local and indigenous knowledge.

The original proposal framed the target group as organizations and people working to help residents of urban informal settlements and emphasized that relevant spatial information can be resource-intensive and time-consuming to produce.

The project should therefore aim for a result that is **useful to planners, NGOs and organizations working with informal settlements**, not merely technically interesting.

---

# 13. Important conceptual distinction: hazard, exposure and risk

Use terminology carefully.

### Hazard
A potentially harmful physical process or condition.

For this project:
> **Potential flood-prone areas identified from terrain and hydrological characteristics.**

### Exposure
People, buildings or assets located in the hazardous area.

For this project:
> **Informal settlement development located within potentially hazardous areas.**

### Vulnerability
The degree to which exposed people/buildings are susceptible to harm.

This may be discussed qualitatively but is not currently a core spatial modelling component.

### Risk
Generally combines hazard, exposure and vulnerability.

Therefore, unless the methodology changes, avoid casually calling the output a full **flood-risk map**.

Prefer terms such as:
- flood hazard;
- flood susceptibility;
- potentially flood-prone areas;
- hazardous areas.

---

# 14. Data philosophy

The project should prefer:
1. Open/free data where possible.
2. Data that covers **both Windhoek and Oshakati**.
3. Data with sufficient spatial resolution for the research question.
4. Historical coverage when temporal change is required.
5. Data that can be downloaded/reproduced.
6. Simple datasets that can be processed within the project timeframe.

For every proposed dataset, consider:

```text
Spatial resolution
Temporal resolution
Historical coverage
Geographic coverage
Vertical accuracy (for elevation)
Data type (DSM/DTM/etc.)
Licensing
File size
Processing requirements
Suitability for the actual research question
```

Do not choose a dataset solely because it has the highest nominal resolution.

---

# 15. GEE strategy

The current intention is to use **Google Earth Engine primarily for data acquisition**.

Likely tasks:
- locate datasets;
- filter data;
- clip to WDH/OSH study areas;
- perform lightweight preprocessing if useful;
- export GeoTIFFs or other suitable formats.

The heavy hydrological processing is currently intended for Python.

GEE may still be used for more processing if this:
- substantially simplifies the workflow;
- reduces local data volume;
- is computationally efficient;
- improves reproducibility.

Do not move processing into GEE merely because it is possible.

The team has access to a comparatively large GEE student compute allowance, but computational resources should still be used sensibly.

---

# 16. Python strategy

Python is the current preferred environment for the hydrological analysis.

Potential tasks:
- raster loading/writing;
- reprojection;
- raster preprocessing;
- slope;
- flow direction;
- flow accumulation;
- drainage analysis;
- hydrological conditioning;
- raster classification;
- spatial overlay;
- quantitative analysis;
- reproducible processing pipelines.

Potential libraries/tools may include:
- rasterio;
- GDAL;
- NumPy;
- GeoPandas;
- WhiteboxTools;
- PySheds;
- RichDEM;
- SciPy;
- other appropriate open-source geospatial tools.

**Do not assume a specific library until the method has been selected.**

Prefer well-supported, transparent tools and explain important methodological choices.

---

# 17. ArcGIS / ArcPy strategy

ArcGIS Pro / ArcPy is currently considered particularly useful for:
- building/shack detection workflows;
- high-resolution imagery analysis;
- potential deep-learning building extraction;
- vector/raster GIS processing;
- spatial statistics if needed.

The exact workflow is not yet decided.

If recommending an ArcGIS tool, clearly distinguish:
- what the tool actually does;
- what input data it requires;
- whether it requires an extension;
- whether it requires a GPU;
- whether it can work with the available imagery;
- whether it is appropriate for informal settlement shacks rather than conventional buildings.

Do not assume that a tool designed for conventional building footprints will automatically work well for informal settlement shacks.

---

# 18. QGIS strategy

QGIS is currently intended primarily for:
- final map design;
- cartographic styling;
- map composition;
- visualization;
- final presentation of analytical outputs.

It may also be used for exploratory GIS work and quality control.

---

# 19. Coding-agent behaviour

The AI assistant should behave as a **technical research assistant**, not merely as a code generator.

Before writing substantial code:

1. Understand the research question.
2. Identify the required input data.
3. Check whether the proposed dataset actually exists and is appropriate.
4. Identify spatial resolution and CRS implications.
5. Consider whether the method is feasible within a 20 ECTS MSc project.
6. Identify likely sources of error.
7. Explain important assumptions.
8. Then propose the simplest robust implementation.

### The AI should challenge assumptions

For example:

If asked:

> "Let's calculate flow accumulation from the Copernicus DSM."

The assistant should consider:

- Is the DSM suitable?
- Could buildings create artificial flow barriers?
- What happens at 30 m resolution?
- Should the DSM be compared with a DTM?
- Is hydrological conditioning needed?
- Does the resulting scale match the research question?

The AI should **not blindly implement the request** if there is a clear methodological problem.

---

# 20. Coding principles

When providing code:

### Prefer
- complete runnable examples;
- clear comments;
- modular functions;
- explicit input/output paths;
- reproducible processing;
- sensible error handling;
- diagnostic outputs;
- metadata preservation;
- CRS awareness;
- NoData handling;
- validation steps.

### Avoid
- unnecessary abstraction;
- overly complicated pipelines;
- black-box processing;
- huge scripts when a small script is sufficient;
- silently changing the research methodology;
- assuming unavailable files or datasets;
- inventing dataset properties.

For raster workflows, always think about:
- CRS;
- pixel size;
- extent;
- alignment;
- NoData;
- data type;
- units;
- resampling method;
- edge effects.

---

# 21. Spatial scale is critical

The project operates across multiple spatial scales.

### Regional/city scale
Useful for:
- overall settlement development;
- drainage patterns;
- topography;
- comparison between WDH and OSH.

### Settlement scale
Useful for:
- identifying hazardous areas;
- overlaying building development;
- understanding exposure.

### Individual shack scale
Only appropriate if sufficiently high-resolution imagery is available.

A 30 m DEM/DSM pixel represents approximately:

**30 m × 30 m = 900 m²**

Therefore, a 30 m elevation dataset cannot be interpreted as providing precise flow behaviour between individual shacks.

The AI should always match claims to the spatial resolution of the data.

---

# 22. Temporal analysis

A major interest is **development over time**.

The exact time period has not yet been finalized because it depends strongly on imagery availability.

For the building/shack component, the ideal analysis would compare:
- earlier settlement state;
- later settlement state;
- newly developed areas;
- overlap with hazardous areas.

The AI should therefore treat historical imagery availability as a methodological constraint.

Do not assume that a theoretically ideal time series exists.

---

# 23. Expected outputs

The final project is expected to produce:

### Main spatial product
Maps of potentially hazardous/flood-prone areas in informal settlements in:
- Windhoek
- Oshakati

### Building/settlement development component
Depending on available data:
- individual shack/building locations and counts, OR
- building-mass/built-up-area change.

### Overlay analysis
A map/statistical analysis showing the spatial relationship between:
- hazardous areas;
- existing informal settlements;
- newly developed settlement/building areas.

### Report
Approximately **50 pages**, explaining:
- background;
- literature/theory;
- methodology;
- data;
- processing;
- results;
- limitations;
- discussion;
- implications for climate adaptation and informal settlements.

### Broader discussion
The project should use the spatial findings to discuss:
- settlement expansion;
- exposure to climate-related hazards;
- planning challenges;
- climate adaptation;
- resilience of informal settlements;
- potential prevention/mitigation strategies;
- relevance beyond the two Namibian case cities.

---

# 24. Limitations to keep visible

The following are expected methodological limitations and should not be hidden:

- 30 m elevation data is relatively coarse compared with individual shacks.
- DSMs may contain buildings/vegetation that affect hydrological modelling.
- A hydrological terrain model is not equivalent to a full hydraulic flood simulation.
- No rainfall modelling is currently planned.
- Historical high-resolution imagery may be difficult or expensive to obtain.
- Informal settlement structures may be difficult to distinguish from other objects in satellite imagery.
- Building/shack detection methods may have omission and commission errors.
- Fieldwork is limited in time and geographic extent.
- The final hazard classification will contain methodological assumptions.
- Results should not be presented as precise predictions of actual flood depths or inundation boundaries unless the methodology genuinely supports such claims.

---

# 25. What the AI should NOT assume

Do **not** assume that:

- Copernicus GLO-30 is automatically the final DEM/DSM.
- DSM is automatically better than DTM.
- Individual shack detection is feasible.
- Sentinel-2 can reliably detect individual shacks.
- A full flood-risk model is required.
- Rainfall modelling must be included.
- A hydraulic 2D model is required.
- Fieldwork observations are model-training data.
- The project requires machine learning.
- the final hazardous-area classification has already been decided.
- the building-development methodology has already been decided.
- a complex model is academically better than a simple one.
- historical high-resolution imagery is available for all required dates.
- a GIS tool designed for conventional buildings will perform well on informal settlements without testing.

---

# 26. Current confirmed decisions vs. open questions

## CONFIRMED

- Study areas: **Windhoek and Oshakati**.
- Main topic: **hazardous areas in urban informal settlements**.
- Hazardous area definition: **areas identified as potentially flood-prone based on terrain and hydrological characteristics**.
- Settlement development into hazardous areas is a central concern.
- Final product should include a spatial overlay of hazardous areas and settlement/building development.
- Project is **20 ECTS**.
- Keep methodology feasible and appropriately scoped.
- GEE is primarily for data acquisition.
- Python is intended for hydrological analysis.
- ArcGIS/ArcPy is intended to support building/shack analysis.
- QGIS is intended for final cartographic design.
- Fieldwork supports and validates interpretation rather than serving as a core spatial-model input.
- Rainfall data is currently not intended as a major analytical component.
- Both individual shack detection and building-mass analysis remain open.

## CURRENT CANDIDATES

- Copernicus GLO-30 DSM.
- SRTM 30 m.
- HydroSHEDS as a hydrological reference.
- Sentinel-2 imagery.
- High-resolution commercial imagery for individual shack detection.
- Lower-resolution imagery for building-mass change analysis.
- DSM vs DTM comparison.
- Different Python hydrological libraries/tools.

## OPEN QUESTIONS

1. What is the most appropriate elevation surface for WDH and OSH?
2. How much do buildings in a DSM influence flow accumulation at 30 m?
3. Is a suitable DTM available for comparison?
4. What exact hydrological method should define the hazardous areas?
5. How should "potentially flood-prone" be operationalized?
6. What historical imagery is actually available for WDH and OSH?
7. Is individual shack detection feasible?
8. If not, what is the best building-mass indicator?
9. What temporal period provides the best balance between data availability and research value?
10. What validation can realistically be performed with field observations?
11. How can the final results be expressed without overstating their precision?

---

# 27. Recommended decision-making hierarchy

When helping with the project, prioritize decisions in this order:

```text
Research question
      ↓
What spatial information is actually required?
      ↓
What data are available?
      ↓
What spatial/temporal resolution is required?
      ↓
What method is scientifically defensible?
      ↓
What method is feasible within 20 ECTS?
      ↓
What software/tool is best suited?
      ↓
Write the code
```

**Do not start with the software and work backwards into a research question.**

---

# 28. Useful terminology

Use these terms consistently:

- **urban informal settlements**
- **informal settlement**
- **shack / shacks**
- **hazardous areas**
- **potentially flood-prone areas**
- **flood hazard**
- **flood susceptibility**
- **settlement expansion**
- **settlement development**
- **building mass / built-up area**
- **exposure**
- **climate adaptation**
- **climate resilience**
- **extreme rainfall**
- **major rainfall events**

Avoid using **"slum areas"** as the default project terminology. Prefer **"urban informal settlements"**.

---

# 29. Project philosophy

The project should answer a relatively simple spatial question well:

> **Are informal settlements developing into areas that are potentially hazardous because of their terrain and hydrological characteristics?**

The strength of the project should come from:
- a clear definition;
- appropriate spatial data;
- transparent GIS methods;
- awareness of uncertainty;
- comparison of two Namibian cities;
- temporal settlement-development analysis;
- field-based contextual understanding;
- a strong discussion of climate adaptation.

The objective is **not** to build the most sophisticated flood model possible.

The objective is to produce a **credible, useful and understandable spatial analysis** that can support a broader discussion about how informal settlements can be protected from increasing climate-related hazards.

---

# 30. Source context

The original MSc project proposal described the project as an investigation of climate change and extreme rainfall in urban informal settlements in Namibia. It proposed spatial analysis including overlay analysis, terrain/slope analysis, precipitation remote sensing, and field surveying, alongside qualitative fieldwork/interviews. It also identified urban resilience, wicked problems, nature-based solutions, urban green infrastructure, participatory planning and land administration as relevant perspectives.

The project direction has subsequently been narrowed and refined toward **hazardous areas and settlement development into those areas**, with the current operational definition given above.

The original project timetable states that the Namibia stay and project writing take place from August to November 2026, with a product and an approximately 50-page report, followed by an oral defence in December 2026.

---

# 31. Final instruction to the AI agent

When assisting with this project:

> **Think like a GIS researcher and coding partner working within a 20 ECTS MSc project.**

Before proposing code, make sure the proposed analysis serves the research question.

When there are multiple valid approaches:
1. explain the alternatives;
2. identify the main methodological trade-offs;
3. recommend the simplest defensible approach;
4. clearly state what remains uncertain.

When writing code:
- make it reproducible;
- make assumptions explicit;
- include diagnostic checks;
- avoid unnecessary complexity;
- never silently change the methodology.

When a data limitation is discovered, **do not force the original method**. Instead, explain how the research question can be answered with the available data.

The project should remain scientifically credible while being realistic about the resources, data and time available to two MSc students.
