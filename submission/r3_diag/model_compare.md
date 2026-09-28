# L / R / M

L/R/M là thứ tự box in-scope theo XML của từng frame.

## adasind_006840.jpg
- L3+R1: LR_noM (center)
- L4+R8+M1: LRM (center)
- L8+R9+M11: LRM (edge)
- L2+R7: LR_noM (mid)
- L1+R5+M7: LRM (mid)
- L5+R2+M2: LRM (mid)
- L7+R6: LR_noM (mid)
- L6+R3+M5: LRM (center)
- L9+M12: LM_noR (center)
- L11: L_only (center)
- R4: R_only (center)
- M3: M_only (mid)
- M6: M_only (center)
- M8: M_only (mid)
- M9: M_only (center)
- M10: M_only (mid)
- M13: M_only (center)
## adasind_036720.jpg
- L1+R4: LR_noM (edge)
- L3+R3: LR_noM (center)
- L2+R1: LR_noM (mid)
- L4+R2+M3: LRM (center)
- M1: M_only (edge)
- M2: M_only (edge)
- M4: M_only (center)
- M6: M_only (edge)
## adasind_056040.jpg
- L4+R1+M1: LRM (center)
- L2+R6+M8: LRM (mid)
- L6+R5: LR_noM (center)
- L8+R2: LR_noM (edge)
- L5+R4: LR_noM (center)
- L1+R3+M7: LRM (center)
- L7+R7+M6: LRM (mid)
- L3+M4: LM_noR (mid)
- M2: M_only (edge)
- M3: M_only (edge)
- M5: M_only (center)
- M9: M_only (mid)
- M11: M_only (mid)

## Zone × cell
| zone | LRM | LR_noM | LM_noR | L_only | RM_noL | R_only | M_only |
|---|---|---|---|---|---|---|---|
| center | 5 | 4 | 1 | 1 | 0 | 1 | 5 |
| mid | 4 | 3 | 1 | 0 | 0 | 0 | 5 |
| edge | 1 | 2 | 0 | 0 | 0 | 0 | 5 |
