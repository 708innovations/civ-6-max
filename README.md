# Max - Civilization VI Mod

A custom Civilization VI mod introducing **Max** as a playable leader, complete with unique civilization traits, an unorthodox economic engine based on district heists and silverware hoarding, culinary growth mechanics, high-risk urban planning, and specialized units.

---

## Table of Contents

- [Leader: Max](#leader-max)
  - [Leader Ability: Kleptomania](#leader-ability-kleptomania)
  - [Unique Action: Pocket Silverware](#unique-action-pocket-silverware)
  - [Product Sets & Amenities](#product-sets--amenities)
- [Civilization Ability: Soupmeister](#civilization-ability-soupmeister)
  - [Unique Project: Make Egg Drop Soup](#unique-project-make-egg-drop-soup)
- [Unique District: The Dylan](#unique-district-the-dylan)
- [Unique Units](#unique-units)
  - [Naked Homeless Man](#naked-homeless-man)
  - [Nuclear Satellite](#nuclear-satellite)
- [Unique Improvements](#unique-improvements)
  - [Soup Kitchen](#soup-kitchen)
  - [Shitbucks Coffee](#shitbucks-coffee)

---

## Leader: Max

### Leader Ability: Kleptomania

- Each **City Center** starts with **+5 Product Slots** by default.

- Product capacity expands further with standard economic buildings:
  - Constructing a **Seaport** grants **+3 Product Slots**.
  - Constructing a **Stock Exchange** grants **+3 Product Slots**.

### Unique Action: Pocket Silverware

- **Exclusive Unit:** Usable only by **Naked Homeless Man** units.

- **Requirements:** Unit must be located in any foreign district.
- **Mechanics:**
  - Pillages **1 level** of the target district.
  - **Does not consume** a unit charge.
  - Steals and awards one of three random silverware products to the civilization:

| Product | Yield / Effect |
| :--- | :--- |
| **Fork** | +2 Culture |
| **Spoon** | +2 Science |
| **Plate** | +1 Culture, +1 Science |

### Product Sets & Amenities

Storing complete silverware services within the same city unlocks tiered **Amenity** bonuses:

| Tier | Required Silverware in City | Amenity Bonus |
| :--- | :--- | :--- |
| **Loaded** | 1 Fork, 1 Spoon, 1 Plate | **+1 Amenity** |
| **Fully Loaded** | 2 Forks, 2 Spoons, 2 Plates | **+2 Amenities** |
| **Overloaded** | 3 Forks, 3 Spoons, 3 Plates | **+3 Amenities** |

---

## Civilization Ability: Soupmeister

### Unique Project: Make Egg Drop Soup

Unlocks the exclusive City Center district project **Make Egg Drop Soup**.

- **Production Cost:** Standard district project production.
- **Completion Rewards:**
  - **+1 Population** in the host city.
  - **+1 Amenity** in the host city for 6 turns.
  - **+10% Food** for 6 turns across all friendly cities within a **6-tile radius** (boosted to **+20%** if the city has a Soup Kitchen).

### Granary Synergy & Project Discount

- **Permanent Granary Growth:** Every completion of *Make Egg Drop Soup* permanently adds **+1 Food** to the host city's **Granary** (stacks up to a maximum of **+3 Food**).

- **Speed Milestone:** Once the Granary bonus reaches **+3 Food**, the *Make Egg Drop Soup* project production cost is permanently halved (requires only **50% standard production** to complete).

---

## Unique District: The Dylan

*Replaces the standard Neighborhood district.*

- **Housing:** **+200 Housing** (virtually unlimited urban capacity).
- **Amenities:** **-2 Amenities** (extreme urban unrest).
- **Hazard:** Upon completion, immediately spawns **3 Barbarian Tanks** around The Dylan.

---

## Unique Units

### Naked Homeless Man

*A scaling, immortal melee-infiltrator unit available throughout history.*

- **Availability & Capacity:**
  - Gain **+1 Homeless Man capacity** at the start of each Era (starting in the **Ancient Era**).
- **Immortality & Respawn:**
  - If defeated in combat, the unit does **not perish**.
  - Respawns with **1 HP** at the nearest **Soup Kitchen** or capital **City Center**.
- **Combat & Movement Scaling:**
  - Automatically matches the **Combat Strength**, **Movement**, and **Visibility** of the highest infantry unit owned by your civilization.
  - Uses the standard **Infantry (Melee)** promotion tree.
  - Can freely cross **closed borders**.
- **Passive Stench:**
  - Deals **5 damage every turn** to all adjacent units (both **enemy and friendly**) within a 1-tile radius.
- **Projectile Assault (Ranged Attack):**
  - Can consume an available silverware product (Fork, Spoon, or Plate) to perform a ranged attack with **+20 Ranged Strength**.
  - Throwing reduces your stored silverware inventory by 1 per attack.
  - Suffers **-40 Bombard Strength** penalty against district defenses.
- **Urban Disruption Charges:**
  - Comes with **2 charges** per unit (using charges does not consume the unit).
  - Activating a charge inside a foreign City Center:
    - Adds **100 Grievances** against your civilization from the target player.
    - Permanently removes **1 Appeal** from every tile belonging to that city.

---

### Nuclear Satellite

*Replaces the Observation Balloon.*

- **Class:** Support-class air unit (immune to standard surface attacks; can only be targeted by air combat or anti-air defenses).
- **Prerequisites:** Unlocked with **Astronomy**.
- **Maintenance:** **10 Gold** per turn (requires **no strategic resources**).
- **Deployment:** Can be constructed in either an **Aerodrome** or an **Encampment** district.
- **Reconnaissance:**
  - Massive **Sight range of 9**.
  - Sight is **completely unobscured** by terrain features (hills, mountains, woods, rainforest).
- **Siege Support:**
  - Grants **+1 Range** to all adjacent bombard-class siege units.

---

## Unique Improvements

### Soup Kitchen

*Unlocked with the **Craftsmanship** civic.*

- **Unit Buffs:**
  - **+30% Production** towards constructing Naked Homeless Men.
  - Naked Homeless Men receive **+50 EXP** upon being built.
- **Respawn Point:** Serves as a valid resurrection anchor for defeated Naked Homeless Men (respawn with 1 HP).
- **Project Synergy:** Enhances the *Make Egg Drop Soup* project:
  - Cities within a 6-tile radius receive **+20% Food** for 6 turns upon project completion (replacing the base +10%).

---

### Shitbucks Coffee

*Unlocked with the **Capitalism** civic.*

- **Commercial Transit Buff:**
  - Any military unit (**both friendly and enemy**) that enters a Shitbucks Coffee tile can spend **10 Gold** to receive **+2 Movement** for **10 turns**.
- **Amenity Synergy:**
  - If the host city owns an improved **Coffee** resource, Shitbucks Coffee provides **+1 additional Amenity**.
