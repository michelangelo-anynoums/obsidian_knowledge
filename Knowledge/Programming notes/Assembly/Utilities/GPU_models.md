# 🎮 GPU Guide — Brands, Numbers & Differences

> [!abstract] Overview A **GPU (Graphics Processing Unit)** is the processor responsible for graphics, gaming, 3D rendering, AI tasks, and other demanding visual workloads.
> 
> When choosing a graphics card, three things matter most:
> 
> - **Brand:** Who makes the GPU chip?
> - **Model number:** Which generation and performance level?
> - **VRAM:** How much dedicated graphics memory does it have?

---

## 🏭 1. The Main GPU Brands

There are three main companies competing in the consumer GPU market.

### 🟢 NVIDIA — GeForce RTX

- **Strengths:** Ray tracing, AI features, CUDA, and broad software support.
- **Popular for:** Gaming, AI, 3D rendering, and creative work.
- **Examples:** RTX 4060, RTX 4070, RTX 5080.

### 🔴 AMD — Radeon RX

- **Strengths:** Competitive gaming performance and often good value for money.
- **Popular for:** Gaming and general graphics workloads.
- **Examples:** RX 7600, RX 7800 XT, RX 9070 XT.

### 🔵 Intel — Arc

- **Strengths:** Competitive budget options and modern graphics features.
- **Popular for:** Budget gaming and everyday graphics workloads.
- **Examples:** Arc A750, Arc B580.

> [!tip] Important distinction NVIDIA, AMD, and Intel design the GPU chips. Companies such as ASUS, MSI, Gigabyte, Sapphire, and Zotac manufacture or sell specific graphics card models using those chips.
> 
> For example, an **ASUS GeForce RTX 4070** uses an NVIDIA GPU chip, but ASUS makes that particular graphics card.

---

## 🔢 2. What Do the Numbers Mean?

Let's decode a graphics card name.

### Example: NVIDIA GeForce RTX 4070

|Part|Meaning|
|---|---|
|**GeForce**|NVIDIA's consumer graphics card family|
|**RTX**|Product family with ray tracing and AI features|
|**40**|40-series generation|
|**70**|Performance tier within that generation|

In general, within the same generation:

- **50 / 60** → Entry-level or mainstream
- **70** → Upper-mainstream
- **80** → High-end
- **90** → Enthusiast flagship

These tiers are approximate, and naming conventions can change between generations.

### Example: AMD Radeon RX 9070 XT

|Part|Meaning|
|---|---|
|**Radeon RX**|AMD's consumer graphics family|
|**90**|Part of AMD's newer 9000-series naming|
|**70**|Model tier|
|**XT**|Higher-performance variant of this model|

AMD's numbering system differs from NVIDIA's, so an RX 9070 XT is **not automatically equivalent** to an RTX 9070 or RTX 5070. Compare actual performance instead.

### Example: Intel Arc B580

|Part|Meaning|
|---|---|
|**Arc**|Intel's graphics brand|
|**B**|Battlemage architecture generation|
|**580**|Specific model within that product family|

Intel uses a different naming system, so direct number comparisons with NVIDIA or AMD are not meaningful.

---

## 📅 3. How to Estimate a GPU's Generation and Release Year

> [!abstract] The basic rule Each GPU brand uses its own naming system. The model number can help identify its generation, but **the number itself does not reliably encode the release year**.

---

### 🟢 NVIDIA GeForce RTX

For modern NVIDIA RTX cards, the first two digits usually identify the series.

|Series|Example|Approx. launch year|
|---|---|---|
|RTX 20|RTX 2080|2018|
|RTX 30|RTX 3080|2020|
|RTX 40|RTX 4080|2022|
|RTX 50|RTX 5080|2025|

**How to read RTX 4070:**

- `40` → 40-series generation
- `70` → Performance tier
- `2022` → Year the generation launched

**Memory trick:** 20 → 2018 · 30 → 2020 · 40 → 2022 · 50 → 2025.

---

### 🔴 AMD Radeon RX

AMD uses a different numbering system. In many modern Radeon RX models, the first digit or digits indicate the series, while the remaining digits help identify the product tier.

|Series|Example|Approx. launch year|
|---|---|---|
|RX 5000|RX 5700 XT|2019|
|RX 6000|RX 6800 XT|2020|
|RX 7000|RX 7800 XT|2023|
|RX 9000|RX 9070 XT|2025|

**How to read RX 7800 XT:**

- `7` → 7000-series generation
- `800` → Model and performance tier within the series
- `XT` → Variant designation
- `2023` → Approximate launch year for the RX 7800 XT model

**Memory trick:** RX 5000 → 2019 · RX 6000 → 2020 · RX 7000 → 2022–2023 · RX 9000 → 2025.

> [!note] AMD exception The RX 7000 series launched across multiple years. The RX 7900 XT arrived in 2022, while the RX 7800 XT launched in 2023. Always check the individual model's launch date when accuracy matters.

---

### 🔵 Intel Arc

Intel uses letters to identify its Arc GPU generations, rather than encoding the year in the first two digits.

|Series|Example|Generation name|Approx. launch year|
|---|---|---|---|
|Arc A-series|Arc A770|Alchemist|2022|
|Arc B-series|Arc B580|Battlemage|2024|
|Arc C-series|—|Celestial|Planned generation; check release status|
|Arc D-series|—|Druid|Planned generation; check release status|

**How to read Arc B580:**

- `B` → Battlemage generation
- `580` → Specific model and its position within the lineup
- `2024` → Announcement year; the B580 became available in December 2024

**Memory trick:** A → 2022 · B → 2024 (approximate generation introduction dates).

> [!warning] Intel exception Intel's letter identifies the GPU generation, but the number `580` does not mean 2025 or 5800-series. Check the specific product's launch date.

---

### 🧠 Quick Comparison

|Brand|What identifies the generation?|Can you calculate the year directly?|
|---|---|---|
|NVIDIA|Series digits, e.g. RTX **40**70|No — use the series launch-year reference|
|AMD|Series digits, e.g. RX **7**800 XT|No — check the specific model|
|Intel|Generation letter, e.g. Arc **B**580|No — check the generation launch history|

> [!tip] Golden rule **GPU model numbers identify product families and performance tiers, not exact years.** Use the series as a clue, then verify the launch date if you need to know the GPU's age.


---
## 🧠 3. What Do the Extra Letters Mean?

Letters can indicate a more powerful version, a different design, or a mobile GPU.

|Suffix|Typical meaning|
|---|---|
|**Ti**|NVIDIA model with a different, often faster configuration|
|**SUPER**|NVIDIA refresh or revised model, often with improved performance|
|**XT**|AMD variant, often faster than the non-XT version|
|**XTX**|AMD's higher-tier variant in certain product families|
|**M**|Sometimes used for mobile graphics products, depending on the brand and generation|

> [!warning] Don't judge by letters alone These suffixes are not universal performance guarantees. Always compare the specific models and their benchmarks.

---

## 💾 4. What Is VRAM?

**VRAM** is the dedicated memory used by the graphics card to store textures, graphics data, and other resources.

|VRAM|General guidance|
|---|---|
|**4–6 GB**|Basic graphics and lighter gaming|
|**8 GB**|Mainstream gaming, with some limitations in demanding modern games|
|**12 GB**|A useful balance for many modern gaming workloads|
|**16 GB**|More room for high-resolution textures, demanding games, and creative workloads|
|**24 GB+**|Useful for certain professional, AI, and very memory-intensive workloads|

These are guidelines, not strict requirements. VRAM needs depend on the game, resolution, settings, and workload.

> [!important] More VRAM doesn't automatically mean a faster GPU. A powerful GPU with 12 GB can outperform a weaker GPU with 16 GB. Processing power, memory bandwidth, architecture, and software support also matter.

---

## ⚡ 5. What Actually Makes a GPU Faster?

Don't judge a graphics card by its model number alone.

- **Architecture:** The underlying GPU design and its capabilities.
- **Performance:** How well it performs in real games and applications.
- **VRAM capacity:** How much graphics data it can store.
- **Memory bandwidth:** How quickly it can move data.
- **Power consumption:** How much electricity it uses and how much cooling it needs.
- **Features:** Ray tracing, upscaling, frame generation, and software support.
- **Price:** How much performance you get for your money.

---
