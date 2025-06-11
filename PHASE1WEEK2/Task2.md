### Task 2 – Top-Level Orientation

1. **Major sub-modules inside `vsdcaravel`:**
   1. chip_io / padframe
   2. caravel_core / chip_core
   3. copyright_block
   4. caravel_logo
   5. caravel_motto
   6. open_source
   7. user_id_textblock

2. **Signals crossing `mgmt_protect` boundary**

| Direction | Net name          | Purpose |
|-----------|-------------------|---------|
| out → user | mprj_wb_clk      | Wishbone clock |
| out → user | mprj_wb_rst      | Wishbone reset |
| out → user | mprj_iena_wb     | WB enable |
| out → user | mprj_cyc_o_core  | WB cycle |
| out → user | mprj_stb_o_core  | WB strobe |
| out → user | mprj_we_o_core   | Write-enable |
| out → user | mprj_sel_o_core  | Byte select |
| out → user | mprj_adr_o_core  | 32-bit address |
| out → user | mprj_dat_o_core  | Data CPU → user |
|  in ← user | mprj_ack_i_core  | WB acknowledge |
|  in ← user | mprj_dat_i_core  | Data user → CPU |
|  in ← user | mprj_irq         | User interrupt |
| out → user | user_clk         | Dedicated user clock |
| out → user | user_rst         | Dedicated user reset |

3. **First reset/clock synchroniser**  
   File `rtl/caravel_clocking.v`, lines 50–65 — two-FF sync on `pll_clk`.
