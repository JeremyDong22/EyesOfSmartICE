# EyesOfSmartICE - AI Agent Visual Inspection System
# v1.0 - Initial project setup (2026-03-24)

## Project Overview

SmartICE AI Agent for autonomous visual inspection in restaurant operations.

### Architecture (New vs Legacy)
- **Legacy**: Local YOLO model → structured data in DB → AI queries DB (limited)
- **New (this project)**: AI Agent directly accesses camera snapshots, autonomously decides what to inspect

### Core Tool
- `get_snapshot(time, camera_ip)` — supports historical timestamps and camera addresses

### Camera System
- Cameras have a mapping table (e.g., ch12=Zone A, ch13=Zone B)
- Masks annotate table numbers on camera feeds

### Agent Skills
- Skills define inspection behaviors (e.g., "absence check" skill: continuously capture cashier/greeter station snapshots for analysis)
- Multi-store support

## Tech Stack
- Python (uv for virtual environment)
- Supabase (via MCP) for data persistence

## Development Rules
- Use `uv` for Python virtual environment management
- Supabase MCP is configured in `.mcp.json`
- Do not commit `.env` files
