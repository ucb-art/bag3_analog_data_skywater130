# Summary of Guard Ring Rules from Sky130 LatchUp Document

1. Divide your layout into n block(s), i.e. row(s) of nmos, and p block(s), i.e. row(s) of pmos.
2. Put a **ntap** outer guard ring and a **ptap** inner guard ring around the n block(s).
3. Put a **ptap** outer guard ring and a **ntap** inner guard ring around the p block(s).

# BAG example:
Look at `gen.yaml` and `gen_gr.yaml` to see how the yaml is modified to put a guard ring in this cell. Specifically, note the extra guard ring rows in the `core_tile`, and the extra `ngr` and `pgr` tiles.
Important points:
1. `ngr` tile has `mos_type=ntap`; `pgr` tile has `mos_type=ptap`.
2. The way to specify that a substrate row is a guard ring row is by including `options: {guard_ring: True}` in the `row_specs`. (See `gen_gr.yaml` for an example.)
3. The way to specify that a row has parts of a guard ring column is by including `options: {guard_ring_col: True}` in the `row_specs`. (See `gen_gr.yaml` for an example.)
4. In `MOSBase`, use `self.gr_sub_sep_col` for number of columns between substrate column and guard ring column to satisfy spacing requirement in the horizontal direction.
