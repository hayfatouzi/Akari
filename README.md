# 💡 AKARI — Intelligent Road Lighting

**An interactive, radar-inspired smart street-lighting simulator built for the KIZUNA hackathon.**

AKARI explores how adaptive street lighting could reduce electricity consumption and operating costs by increasing illumination when vehicles approach and reducing it during low-traffic periods—subject to road-safety requirements.

The demonstration models a **500 m candidate road section in Jaâfar–Raoued, Ariana, Tunisia**. The exact installation site, existing equipment and traffic counts have **not** been verified in the field.

> **Naming:** AKARI is the project name. **KIZUNA** is the hackathon name.
>
> **Project status:** Browser-based proof of concept. **No physical radar, streetlight or municipal system is connected.** Performance and costs are modeled estimates, not measured results or safety certification.

## 🚀 Run the demo

**[Launch AKARI](./index.html)** *(download the repository and open `index.html` in a browser; the link is relative to the repository)*

1. Download or clone the repository.
2. Open `index.html` in **Chrome** or **Edge**.
3. The simulation starts automatically. No installation, server, login, build process or Internet connection is required.
4. Use the navigation bar to open **Road Simulation**, **Special Events** or **Analytics Dashboard**.

To clone after publishing your repository, use its actual GitHub URL:

```bash
git clone https://github.com/<OWNER>/<REPOSITORY>.git
cd <REPOSITORY>
```

Then open `index.html` locally. Replace the placeholders with the actual repository owner/name; no public GitHub URL has been assigned in this package.

## ✨ Main features

| Section | What it demonstrates |
|---|---|
| 🚗 **Road Simulation** | Animated vehicles, three virtual radars, five lighting zones per traffic direction, and brightness adjustments |
| 🌙 **Nighttime profiles** | Winter and summer nighttime-only hour selection; automatic clock progression and editable hourly vehicle counts |
| 🚦 **Traffic scenarios** | Empty Road, One Car, Normal Traffic, Heavy Traffic; Pause/Resume and Reset |
| ⚠️ **Special Events** | A vehicle stops → protective 100% lighting; a radar fails → protective lighting and a health alert |
| 📝 **Radar health report** | One downloadable report for the selected winter or summer night, with a checkpoint for each nighttime hour and red radar-failure indicators |
| ⚡ **Energy Analytics** | Fixed lighting before AKARI compared with adaptive lighting after AKARI; hourly and annual energy estimates |
| 💰 **Financial Analytics** | Installation components and costs, maintenance, electricity savings (DT) alongside energy savings (kWh) |
| 📈 **50-year outlook** | Configurable long-term simulation of energy, electricity prices, equipment replacement and cumulative finances; CSV export |

### Road simulation

AKARI models a two-way **500 m** road as **five 100 m sections per direction** (10 directional lighting groups). The baseline demonstration uses **three virtual radars**, an assumed **130 m useful range**, and an adjustable **20% standby** level.

Four demonstration modes are available:

- **Empty Road:** no cars enter; lighting returns toward standby.
- **One Car:** one vehicle passes for an easy-to-follow demonstration.
- **Normal Traffic:** random vehicle arrivals use the selected hourly seasonal profile.
- **Heavy Traffic:** random arrivals use **five times** the selected normal traffic profile as a stress-test setting, **not** a measured forecast.

**Pause/Resume** and **Reset** are the main simulation controls. The simulation clock advances automatically unless paused. You may also jump to a particular available nighttime hour.

### Winter and summer profiles

| Season | Modeled darkness | Hourly checkpoints |
|---|---|---:|
| ❄️ Winter | 17:00–05:00 | 12 |
| ☀️ Summer | 20:15–05:00 | 9, including the partial 20:15–21:00 slot |

The vehicle counts are **editable illustrative assumptions**, not official traffic data for Jaâfar–Raoued. The hour selector offers only dark hours for the selected season. These darkness periods are simplified seasonal approximations, not date-specific astronomical calculations.

## ⚠️ Special Events and safety behavior

The separate **Special Events** page intentionally contains only two scenarios:

| Scenario | Simulated response | Maintenance anomaly? |
|---|---|---|
| **Vehicle Stops** | Lights increase to a protective **100%** | **No** — a stopped vehicle is not a radar defect or a confirmed accident |
| **Radar Failure** | Protective **100%** fallback and a radar-health fault | **Yes** — highlighted in red in the radar-health report |

The radar layout in this visualization is an idealized illustration. The actual coverage, sensing reliability, appropriate lighting level and real safety response require independent engineering validation.

## 📝 Downloadable radar-health report

There is **no separate Reports page**.

- On **Road Simulation**, **Download report** creates a **full simulated night** for the **currently selected season**.
- In **Special Events**, the report section and download control are shown **only for Radar Failure**, not Vehicle Stops.
- Each nighttime hour has a status checkpoint for radar **R1, R2 and R3**.
- **Radar failures are the only anomalies**; affected rows are **red**, with simulated fault and recovery times where applicable.
- Normal car movements and vehicle stops **do not** appear as anomalies.
- The report is generated and downloaded locally as **HTML**; it is **not emailed or transmitted**.

For a future real installation, each radar would require a device-health signal/heartbeat and an **immediate fault alert**, with hourly checkpoints retained for routine reporting. Such telemetry and automatic emails **are not implemented** in this prototype.

## ⚡ Energy and 💰 financial analysis

The primary business comparison is:

**Before AKARI:** existing luminaires modeled at fixed output during darkness.

**After AKARI:** luminaires modeled with adaptive brightness based on traffic assumptions, plus control-system electricity usage.

The dashboard displays **kWh and DT side by side** for the selected time and annual projections, along with editable installation and operating costs. A simplified timer baseline may also appear in the technical energy analysis, but **Fixed vs AKARI** is the central project comparison.

### Initial modeling assumptions

| Input | Demonstration assumption |
|---|---:|
| Road length | 500 m |
| Luminaires | 40 existing LED units |
| Nominal power per luminaire | 120 W |
| Radar count | 3 virtual radars |
| Radar useful range | 130 m (assumed) |
| Standby lighting | 20% (assumed) |
| Electricity tariff | 0.261 DT/kWh (editable model input) |
| Installation budget | Approximately 12,000 DT (illustrative, editable) |

**Simplified calculation:**

```text
Fixed electricity (kWh) = total installed power (kW) × modeled dark hours

Energy saving (kWh) = fixed-lighting electricity − AKARI electricity
Gross electricity saving (DT) = energy saving (kWh) × tariff (DT/kWh)
Net operating saving (DT) = gross electricity saving − maintenance − service expenses
```

The **animated road** and the **annual projection** are not direct measurements of the same trial: the animation displays moving virtual vehicles, while annual outputs use a separate simplified traffic/lighting model based on seasonal hourly assumptions. Treat annual results as **scenario estimates**, not verified field savings.

### Long-term projection (50 years)

The financial section also contains an optional **50-year scenario model**, with adjustable electricity-price and maintenance changes, traffic growth, radar/gateway and controller replacement intervals, and a discount rate.

The cumulative financial graph can **drop in replacement years** because replacement expenses are deducted. Cumulative saved kWh do not disappear when equipment is replaced. This long-term analysis is **not a guarantee** that a given installation, price or road configuration will remain unchanged for five decades.

> **Important:** Electricity-bill savings for a municipality or road operator are **not automatically revenue or profit for AKARI's business**. Vendor income would depend on commercial contracts, pricing and actual operating costs.

## 🧩 How it works (conceptual architecture)

```text
Simulated vehicles + editable hourly profiles
                   │
                   ▼
            Virtual mmWave radars
                   │
                   ▼
        Local lighting-control logic
                   │
                   ▼
        10 directional lighting groups
                   │
            ┌──────┴────────┐
            ▼               ▼
    Live road view      Energy / finance
                              dashboard

Radar health states ──► Hourly report download
                     └─► 100% protective mode on modeled failure
```

Everything currently runs **in the browser**. The project has no connected sensors, database, email service, backend API or user authentication.

## 🗂️ Repository structure

```text
AKARI/
├── index.html      # Standalone application: road, Special Events and Analytics
├── README.md       # GitHub overview, setup, functionality, assumptions
└── .gitignore      # Local editor/system file exclusions
```

The project intentionally has **no external package dependencies**. Contributors can work directly in `index.html` and test in a modern browser.

## 🎤 Suggested hackathon demo

1. Open **Road Simulation → Empty Road** to show low-power standby.
2. Choose **One Car** to demonstrate lighting response to traffic.
3. Select **Normal Traffic** and change a winter/summer nighttime hour.
4. Open **Special Events → Vehicle Stops** and show protective 100% lighting (no radar-fault report).
5. Choose **Radar Failure** and demonstrate fail-safe illumination and a red-highlighted health report.
6. Return to **Road Simulation**, select a season and download its hourly report.
7. Open **Analytics Dashboard** to present the installation budget, modeled kWh and DT savings, and optional 50-year outlook.

## 🔬 What needs validation before a real pilot?

- Identify and obtain permission for an **exact** 500 m road segment in Jaâfar–Raoued.
- Measure nighttime vehicle, motorcycle, pedestrian and side-road movements.
- Inspect actual lamp quantity, power, wiring, LED drivers and dimming compatibility.
- Measure radar range, mounting geometry, field of view, missed detections and latency.
- Establish compliant lighting design and a tested safe fallback under applicable road standards. **20% is not an approved safety level.**
- Obtain supplier quotations in Tunisia, with electrical protections, installation, connectivity, maintenance and taxation.
- Connect a real controller and physical sensors, implement heartbeat monitoring, secure telemetry and a backend for alerts/reports if AKARI progresses to field trials.

## 🛠️ Project status and contribution

**Current stage:** interactive hackathon proof of concept.

Future work includes physical validation, measured energy performance, user-safety review, verified costs and real deployment authorization. Contributions can be proposed through GitHub Issues and Pull Requests after the repository is published. Please describe the scenario being changed, the expected effect and how it was tested.

**License:** No open-source license has been assigned. A repository owner should choose and add a `LICENSE` file if public reuse or modification is intended.

---

**AKARI** — Adaptive lighting when it is needed; measurable energy savings where it is justified. 💡
