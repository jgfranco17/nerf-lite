# Project Context Sheet

Title: Low-Resource Neural Scene Representation (Compressed NeRF-Like)

## Project Goals

Build a memory- and compute-constrained neural scene representation for small indoor scenes,
inspired by NeRF but explicitly engineered for low-resource hardware.

The objective is engineering feasibility, not photorealism. This is a systems-heavy research
project, emphasizing:

* memory layout
* ray efficiency
* numerical stability
* tradeoff analysis

## Constraints

While implementing this project, keep the following restrictions in mind.

### Hardware & resources

* Single consumer GPU (4-6 GB VRAM)
* Ubuntu Linux for development environment
* Training budget per scene: ≤ 6 hours
* Scene scale: single room or small area
* Batch sizes must remain small (ray-based)

### Rendering & training

* Aggressive ray batching
* Early ray termination
* Mixed precision mandatory
* Gradient checkpointing encouraged
* No volumetric grids exceeding memory limits

## Inputs & Outputs

### Input

* Multi-view RGB images
* Known or precomputed camera poses
* Limited number of views (2050)

### Output

* Continuous neural scene representation
* Novel-view rendering
* Optional depth output

## Dataset Assumptions

Primary:

* LLFF (downsampled)
* Custom phone-captured indoor scenes
* Images resized aggressively (≤ 800px wide)
* Poses assumed reasonably accurate

## Representation Constraints

* MLP-based implicit function
* Total parameters strictly limited
* Encoding must be compressed: truncated Fourier features or hash/grid encoding
* No massive CUDA custom kernels required

## Optimization Priorities

* Memory footprint
* Training stability
* Render speed
* Visual quality (last)

## Evaluation Criteria

### Quantitative

* PSNR (secondary)
* Training time
* VRAM usage

### Qualitative

* Visual coherence
* Temporal consistency during camera fly-through
* Failure modes (float instability, noise)

### Core Engineering Challenges

* Ray sampling strategy
* Encoding compression tradeoffs
* Floating-point precision issues
* Training instability
* Debugging silent failures

## Non-Goals

* No SOTA NeRF reproduction
* No outdoor large-scale scenes
* No multi-GPU scaling
* No production deployment claims

## Deliverables

* Minimal but clean NeRF-like implementation
* Clear memory/performance profiling
* Scene reconstruction demos
* Ablation studies on:
  * encoding size
  * ray count
  * precision
* Written tradeoff analysis

## Success Criteria

* Scene trains within hardware limits
* Rendering is coherent and stable
* Clear documentation of constraints and design choices
* Demonstrated understanding of why each optimization exists
