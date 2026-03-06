# confluence-data-model-docs

Utility package for auto-generating Confluence documentation from Fuuz data model definitions. Connects to the Confluence REST API to create or update wiki pages describing each data model's fields, types, and relationships directly from the platform schema.

> **Note:** This is a standalone utility tool, not an application accelerator. It integrates with an Atlassian Confluence space to keep data model documentation in sync with the live platform schema.

## Package Metadata

| Field | Value |
|---|---|
| Package Name | `Confluence Data Model Documentation` |
| Version | `1.0.0` |
| Platform Version | `2023.10.0` |
| Type | Utility / Documentation Tool |

## Components

| Type | Count |
|---|---|
| Data Flows | 2 |
| Screens | 1 |
| Seed Data | 3 tables |

## Overview

This package provides a Fuuz-native documentation pipeline. It queries the Fuuz GraphQL System API to enumerate data models and their field definitions, then pushes formatted wiki pages into a Confluence space via the Confluence REST API. Teams using Confluence as their internal knowledge base can use this to eliminate manual documentation maintenance — the documentation regenerates on demand from the live platform schema.

## Data Flows

| Flow | Description |
|---|---|
| `Generate Confluence Data Model Documentation` | Main orchestration flow. Queries all data models from the Fuuz System API, formats each model's fields into structured Confluence storage-format markup, and creates or updates pages within a designated Confluence space. |
| `Get Pages in Confluence Space` | Helper flow. Retrieves existing page inventory from a Confluence space, enabling the documentation generator to determine whether to create new pages or update existing ones. |

## Screens

| Screen | Description |
|---|---|
| `Confluence Data Model Documenter` | Single-screen UI for triggering documentation generation. Provides connection status, space configuration, and a run button for initiating the documentation push. |

## Seed Data / Configuration

| Type | Details |
|---|---|
| `ApplicationConfiguration` | `Confluence Documentation Integration` — stores Confluence base URL, space key, and auth settings |
| `Module` | `Confluence` |
| `ModuleGroup` | `Documentation` |

## Usage Notes

- Requires a Confluence Cloud or Server instance with REST API access enabled
- Authentication credentials (API token + base URL) must be configured in the `Confluence Documentation Integration` application configuration record before running
- The `Get Pages in Confluence Space` flow is called internally by the main generator to check for existing pages and avoid duplicates
- Designed to be run on demand or scheduled; does not require a trigger event from the MES/WMS application
- Compatible with platform version 2023.10.0 and later

## Package Structure

```
confluence-data-model-docs/
  data/             (seed configuration records)
  dataFlows/        (2 unique flows, 4 files total)
  definition.json
  manifest.json
  package-data.json
  screens/          (1 unique screen, 2 files total)
```
