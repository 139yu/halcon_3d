# Repository Guidelines

## Project Structure

This repository contains MVTec HALCON 3D machine vision examples organized by topic.

- `hdev/` — Example programs (`.hdev` files), grouped by category:
  - `01简单算子使用` — Basic 3D operator usage
  - `02匹配案例` — Shape-based and surface matching
  - `03特征及分割` — Feature extraction and 3D segmentation
  - `04Blob分析` — Blob analysis with PLY point cloud data
  - `05点云案例处理` — Point cloud processing (fitting, ROI, volume, etc.)
- `func/` — Reusable HALCON procedures (`.hdvp` files) such as plane fitting, depth-to-pointcloud conversion, and 3D volume generation.

Data files (`.tif`, `.om3`, `.ply`) live alongside the corresponding `.hdev` scripts they support.

## Running Scripts

All scripts execute directly in **MVTec HALCON** or **HDevelop**. There is no build step.

To open and run a script: start HDevelop, open the `.hdev` file, and click the run button (F5). Scripts in `05点云案例处理` may depend on shared procedures under `Func/`.

There are no automated test or linting commands for this project.

## Coding Style

- Use **4-space indentation** inside HALCON program blocks.
- Names for directories, scripts, and procedures are written in **Chinese** so the topic of each file is immediately clear. English aliases are acceptable for cross-platform portability but not required.
- Procedure files (`.hdvp`) placed under `func/` should have a clear purpose reflected in their filename, e.g., `cal_plane_angle.hdvp`.
- Avoid long monolithic scripts; split reusable logic into `.hdvp` procedures.
- Keep a consistent camera parameter and pose generation approach — prefer the helpers in `func/gen_cam_par_and_pose.hdvp` and `func/depth_image_to_pointcloud.hdvp` over ad-hoc duplication.

## Testing Guidelines

This project does not use an automated testing framework. Quality is verified by:

- Opening each `.hdev` file in HDevelop and running it end-to-end.
- Confirming the expected 3D model, point cloud, or measurement appears in the graphics window.
- Checking logged numeric results (angles, distances, volumes) for correctness.

When adding new examples, include a matching data file (`.tif`, `.om3`, or `.ply`) so the script is self-contained and runnable immediately.

## Commit & Pull Request Guidelines

Commit messages should be written in **Chinese** and describe the high-level topic, matching the existing history:

```
点云处理案例
点云拟合案例
halcon 3d operator
```

Follow this format for new contributions:

- **Scope** (optional): prefix with `feat`, `fix`, `refactor`, or `docs`
- **Body**: a short Chinese description of what the commit adds or changes

When opening a pull request, include:

- A short title and a one-paragraph description in Chinese (or English if the audience is mixed).
- A note on which HDevelop version the scripts were tested with.
- Any new dependencies on HALCON licenses or libraries.

## Agent-Specific Notes

This repository is designed for **AI coding agents** and human contributors alike. When modifying `.hdev` or `.hdvp` files:

- Read the `README.md` and this file first for orientation.
- Respect the existing directory hierarchy and naming scheme.
- When a helper procedure already exists in `func/`, reuse it instead of inlining its logic.
- Test new scripts in HDevelop before committing.
