# Design Systems

This layer adds a visual aesthetic check on top of the existing structural/correctness rules. DashLint does not judge whether a design is "good" or "beautiful," but rather whether the dashboard spec is internally consistent with a chosen visual identity.

Call `list_design_systems()` to see options, `get_design_system(id)` for full tokens, then pass `designSystem` in your spec to validate against it.

## Rules

- **R-DESIGN-01 (Chart Colors Consistent)**: Every hex in `colors.chartColors` must appear in that system's token palette. (Error if not)
- **R-DESIGN-02 (Background/Surface Match)**: `colors.background` and `surfaceColor` must match that system's declared bg/surface tokens. (Warning if not — flags it, doesn't hard-fail on minor tint variants)
- **R-DESIGN-03 (Typography Stack Match)**: `typography.fontFamily` must match one of that system's declared font stacks. (Warning if not)
