# Guideline patch

- **Rule mới đề xuất:** `R05b — edge_zone: bật edge_zone=true khi tâm box nằm ở r/R ≥ 0.6 so với vòng kính của frame (cùng ngưỡng zone edge trong docs/05-taxonomy-vi.md), đo trên ảnh gốc; không bật theo cảm giác "gần mép". Box có tâm ở r/R < 0.6 để false, kể cả khi một phần box chạm vùng edge. Annotator có thể kiểm bằng vòng kính trong assets/frames.csv.`
- **Áp dụng cho:** `attribute edge_zone của cả 6 class box (Car, Bus, Truck, ThreeWheeler, Bike, Pedestrian); không áp dụng cho ignore_region.`
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** `labels.json có attribute edge_zone nhưng rules v1.0.0 không có luật nào nói khi nào bật. Ở adasind_310008.jpg bốn người đi bộ (L1–L4, zone edge) đều bị báo mismatching_attributes: reference đặt edge_zone=true, mình để false (findings r3_diag L1+R3+M1, E2_guideline_gap). Hai người làm đúng theo cách hiểu của mình vẫn ra kết quả khác nhau, nên đây là khoảng trống luật, không phải lỗi annotator.`
- **`rules_version` mới:** `v1.0.0 → v1.1.0`
- **Hiệu lực từ:** `round rework trở đi (và mọi slice gán mới); các bản đã khóa trước v1.1.0 không tính edge_zone khi so với reference.`
