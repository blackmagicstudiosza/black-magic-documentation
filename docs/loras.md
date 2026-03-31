# Custom LoRAs

---

## Walk LoRA

![Walk LoRA Example](images/lora_walk.png)

RPG-style sprite walking animations.

| Setting | Value |
|---|---|
| **CFG** | `4.0` |
| **Steps** | `30` |
| **Sampler** | `euler_ancestral` |
| **Generation Size** | `1024×1024` |
| **Model Strength** | `0.8–1.0` |

**Trigger prompt:**
```
rpgwalk, simple background, <subject description>
```

**Example:**
```
rpgwalk, simple background, female, demon, purple skin, dark armor, silver bracers, curved horns, purple tail
```

---

## Wang Tileset LoRA

![Wang Tileset LoRA Example](images/lora_wang_tileset.png)

Generates seamlessly tiling Wang tilesets.

| Setting | Value |
|---|---|
| **CFG** | `7.5` |
| **Steps** | `30` |
| **Sampler** | `ddim` |
| **Generation Size** | `768×768` |
| **Model Strength** | `0.8–1.0` |

**Trigger prompt:**
```
tilemap_solid, <description>
```

**Example:**
```
tilemap_solid, volcanic ash ground, lava, light orange areas, ground texture, fine details, warm appearance
```

**Workflow:** Generate at 768×768, then scale the result down to 96×96 in Aseprite, then run the **Wang Tileset Generator** in the Tools tab to produce the final 160×96 tileset.

---

## Wall LoRA

![Wall LoRA Example](images/lora_wall.png)

Tileable wall textures.

| Setting | Value |
|---|---|
| **CFG** | `4.0` |
| **Steps** | `30` |
| **Sampler** | `euler_ancestral` |
| **Generation Size** | `768×576` |
| **Model Strength** | `0.8–1.0` |

**Trigger prompt:**
```
tilemap_wall, <description>
```

**Example:**
```
tilemap_wall, marble, polished surface, white, gold veins, vertical pattern
```

---

## Cliff LoRA

![Cliff LoRA Example](images/lora_cliff.png)

Cliff and rock face tilesets.

| Setting | Value |
|---|---|
| **CFG** | `7.5` |
| **Steps** | `30` |
| **Sampler** | `euler_ancestral` |
| **Generation Size** | `768×768` |
| **Model Strength** | `0.8–1.0` |

**Trigger prompt:**
```
cliffmap_tileset, simple background, <description>
```

**Example:**
```
cliffmap_tileset, simple background, pink petal cliff walls, light pink blossom cliff tops, dark cavern openings, white flower details, delicate bloom texture, soft floral coverage, spring coloring
```

---

## Single Tile LoRA

![Single Tile LoRA Example](images/lora_single_tile.png)

Single seamlessly tiling ground/floor tiles.

| Setting | Value |
|---|---|
| **CFG** | `7.5` |
| **Steps** | `30` |
| **Sampler** | `euler_ancestral` |
| **Generation Size** | `768×768` |
| **Model Strength** | `0.8–1.0` |

**Trigger prompt:**
```
tilemap_single, <description>
```

**Example:**
```
tilemap_single, snow ground, glowing red lava cracks
```

---

## Building LoRA

![Building LoRA Example](images/lora_building.png)

Top-down RPG buildings and structures.

| Setting | Value |
|---|---|
| **CFG** | `7.5` |
| **Steps** | `30` |
| **Sampler** | `euler_ancestral` |
| **Generation Size** | `768×768` |
| **Model Strength** | `0.8–1.0` |

**Trigger prompt:**
```
tilemap_building, simple background, <description>
```

**Example:**
```
tilemap_building, simple background, medieval inn, gable roof, centered, red tiled roof, timber framed
```

---

## Small Items LoRA

![Small Items LoRA Example](images/lora_small_items.png)

Small RPG inventory items and icons.

| Setting | Value |
|---|---|
| **CFG** | `7.5` |
| **Steps** | `30` |
| **Sampler** | `euler_ancestral` |
| **Generation Size** | `768×768` |
| **Model Strength** | `0.8–1.0` |

**Trigger prompt:**
```
item_small, simple background, <description>
```

**Example:**
```
item_small, simple background, flaming metal sword, silver handle
```

---

## Medium Items LoRA

![Medium Items LoRA Example](images/lora_medium_items.png)

Medium-sized RPG items and props.

| Setting | Value |
|---|---|
| **CFG** | `7.5` |
| **Steps** | `30` |
| **Sampler** | `euler_ancestral` |
| **Generation Size** | `768×768` |
| **Model Strength** | `0.8–1.0` |

**Trigger prompt:**
```
item_med, simple background, <description>
```

**Example:**
```
item_med, simple background, glass table, blue tint, transparent, reflective surface, metal legs
```

---

## Large Items LoRA

![Large Items LoRA Example](images/lora_large_items.png)

Large RPG items and props.

| Setting | Value |
|---|---|
| **CFG** | `7.5` |
| **Steps** | `30` |
| **Sampler** | `euler_ancestral` |
| **Generation Size** | `768×768` |
| **Model Strength** | `0.8–1.0` |

**Trigger prompt:**
```
item_large, simple background, <description>
```

**Example:**
```
item_large, simple background, colossal boulder, irregular shape, cracked stone surface, moss patches
```

---

## Portrait LoRA

![Portrait LoRA Example](images/lora_portrait.png)

RPG character portraits on a white background.

| Setting | Value |
|---|---|
| **CFG** | `7.5` |
| **Steps** | `30` |
| **Sampler** | `euler_ancestral` |
| **Generation Size** | `768×768` |
| **Model Strength** | `0.8–1.0` |

**Trigger prompt:**
```
rpgport, <subject>, white background
```

**Example:**
```
rpgport, 1boy, werewolf, gray fur, yellow eyes, torn brown pants, muscular, claws, fangs, snarling, white background
```
