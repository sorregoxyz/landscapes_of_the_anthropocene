# Landscapes of the Anthropocene

**Landscapes of the Anthropocene** is a growing visual atlas of places transformed by human activity. Initially, it will be posted on Instagram: https://bit.ly/468RJ4k

It treats satellite imagery as a way of observing the physical traces of extraction, agriculture, energy production, urban growth, water management, waste, infrastructure, and climate change. Each place is recorded as a landscape entry and can become an Instagram carousel: a short visual publication that combines images, orientation, interpretation, and a question.

The project is deliberately built as a small, legible data system. It can be used as a public atlas, an editorial workflow, or a starting point for others who want to create their own place-based visual research archive.

> The landscape is the evidence.

## How the project works

There are two connected layers:

1. **The atlas** records places.
2. **The posts** record the editorial publications made from those places.

One landscape can appear in more than one post. One post can bring together several landscapes.

For example, a standard post may explore one limestone quarry. A comparison post may bring together five quarries in different countries. The places are recorded once in the atlas; the posts simply connect to them.

```text
atlas.csv                 Places and landscape research
        │
        └── post_landscapes.csv ── connects places to posts
                                      │
                                      └── posts.csv
                                          Instagram carousel publications
```

## Folder structure

```text
landscapes-of-the-anthropocene/
├── data/
│   ├── atlas.csv
│   ├── posts.csv
│   ├── post_landscapes.csv
│   ├── taxonomy_category.csv
│   ├── taxonomy_process.csv
│   └── taxonomy_type.csv
├── images/
│   ├── PO001/
│   ├── PO002/
│   └── ...
└── README.md
```

`images/` is optional at the beginning. When it is used, each post receives its own folder, named after its post ID.

## The data files

### `atlas.csv`: the landscape catalogue

One row represents one real landscape, whether or not it has been published on Instagram.

```csv
id,title,place,country,lat,lng,category,process,keywords,description,region,source
```

Example:

```csv
LA001,White Grounds,Faxe,Denmark,55.62,12.13,"extraction,water",quarrying,"limestone,geology,groundwater",A former limestone quarry now partly filled with water,Europe,Google Earth
```

| Field | Meaning |
| --- | --- |
| `id` | A stable landscape ID, such as `LA001`. Do not change it after creating it. |
| `title` | The editorial name of the landscape. |
| `place` / `country` | The location name and country. |
| `lat` / `lng` | Latitude and longitude in decimal degrees. |
| `category` | One or more broad categories from `taxonomy_category.csv`. |
| `process` | One or more specific processes from `taxonomy_process.csv`. |
| `keywords` | Free-form terms used for research and discovery. |
| `description` | A factual, concise description of the landscape. |
| `region` | An optional broad geographical region. |
| `source` | The principal image, map, or research source. |

### `posts.csv`: the publication catalogue

One row represents one Instagram carousel or other editorial publication.

```csv
id,title,type,status,publish_date,statement,question,caption,image_folder
```

Example:

```csv
PO001,White Grounds,landscape,draft,,A mountain that became a lake.,When does a mine become a landscape?,,PO001
```

| Field | Meaning |
| --- | --- |
| `id` | A stable post ID, such as `PO001`. |
| `title` | The title used for the carousel. |
| `type` | An editorial format from `taxonomy_type.csv`. |
| `status` | A workflow state, for example `idea`, `researching`, `draft`, `scheduled`, or `published`. |
| `publish_date` | Publication date in `YYYY-MM-DD` format; leave blank until scheduled. |
| `statement` | The short central statement, normally used early in the carousel. |
| `question` | The question or proposition that closes or punctuates the sequence. |
| `caption` | The longer Instagram caption. |
| `image_folder` | The associated folder under `images/`, for example `PO001`. |

### `post_landscapes.csv`: the connection table

This file connects posts to the landscapes they include.

```csv
post_id,landscape_id,position
```

A standard one-landscape post has one connection:

```csv
PO001,LA001,1
```

A comparative post can connect to several landscapes:

```csv
PO002,LA001,1
PO002,LA014,2
PO002,LA027,3
```

`position` indicates the order in which landscapes are introduced in the post. It is especially useful for comparisons and series.

## The taxonomies

The three taxonomy files provide a controlled vocabulary. They are not additional atlas tables.

```text
atlas.csv
├── category ── taxonomy_category.csv
└── process  ── taxonomy_process.csv

posts.csv
└── type     ── taxonomy_type.csv
```

### `taxonomy_category.csv`

Broad kinds of landscape transformation, such as `extraction`, `agriculture`, `water`, `energy`, or `waste`.

### `taxonomy_process.csv`

Specific forms of transformation, such as `quarrying`, `irrigation`, `dam_construction`, or `solar_generation`.

### `taxonomy_type.csv`

Editorial formats, such as `landscape`, `comparison`, `before_after`, `detail`, `question`, `community`, and `series`.

## Creating the first entry

To publish one standard landscape entry, work in this order:

1. Find and research a place.
2. Add the place to `atlas.csv`, assigning the next `LA` ID.
3. Assign category and process terms only from the taxonomy files. If several values apply, separate them with commas and place the whole cell in quotation marks.
4. Add the intended carousel to `posts.csv`, assigning the next `PO` ID.
5. Connect the post and landscape in `post_landscapes.csv`.
6. Create `images/PO###/` and place the prepared carousel images there.
7. Change the post status as it moves from research to draft, schedule, and publication.

For the first example, the relationship is:

```text
LA001  White Grounds, Faxe
  │
  └── PO001  White Grounds — landscape post
```

## Carousel grammar

The standard post format is a nine-slide micro-publication:

```text
01  Cover
02  Threshold: central statement
03  Image and orientation
04  Image and observation
05  Text plate: interpretation
06  Image and detail
07  Image and context
08  Question or proposition
09  Back cover
```

The images change from post to post; the sequence supplies a consistent editorial rhythm. Other post types can use the same grammar while changing the subject or number of landscapes.

## CSV conventions

- Use lowercase, underscore-separated values for taxonomy terms: `before_after`, `dam_construction`.
- Keep IDs stable and sequential: `LA001`, `LA002`; `PO001`, `PO002`.
- Use `YYYY-MM-DD` for dates.
- Wrap a cell in quotation marks when it contains commas, for example: `"extraction,water"`.
- Keep taxonomy values controlled; keep `keywords` open and exploratory.
- Do not create duplicate atlas rows for the same place solely because it appears in another post.

## Replicating this system

To make an atlas of another subject—coastal infrastructures, disappearing forests, urban heat, or any other spatial question—keep the model and replace the vocabulary:

1. Define the landscapes or sites you want to observe.
2. Create broad categories and specific processes relevant to that subject.
3. Record each site once in `atlas.csv`.
4. Use `posts.csv` to plan and publish your editorial sequences.
5. Use `post_landscapes.csv` whenever a publication draws on one or more sites.

The principle remains the same: **a stable research archive supports many changing editorial interpretations.**

## Status

The project is in its initial catalogue-building stage. The data structure is ready for its first landscape entries and publications.
