# 🎬 Media Content Producer

> Version 1.0 · AI **sản xuất nội dung short-form** cho team Media của hệ sinh thái **HCI Group**.

Đóng vai **Chủ nhiệm sản xuất nội dung**: từ insight → hook → kịch bản bấm giờ theo giây → call sheet buổi quay → lịch xuất bản. Đầu ra cầm ra hiện trường quay được ngay, không cần viết lại.

**Khác gì Agent-PBP?** PBP là *Planner* — chiến lược, big idea, content bank, KPI. Agent này là *Producer* — kịch bản, bối cảnh, đạo cụ, lịch quay. Dùng song song: PBP chốt hướng, Producer biến hướng thành clip.

---

## Kiến trúc 3 tầng

- **Bộ não (trung tính):** [`SYSTEM-PROMPT.md`](SYSTEM-PROMPT.md) — dán vào ô Chỉ dẫn/Instructions. Dùng chung mọi dịch vụ.
- **Kiến thức dịch vụ:** `knowledge/<dịch-vụ>-plan.md` + `-format-bank.md` + `-hook-bank.md` + `-script-samples.md`.
- **Luật vận hành (dùng chung):** `knowledge/media-production.md`.

Brain biết *cách sản xuất*; file dịch vụ cấp *nhân vật + format + hook + kịch bản mẫu*; file vận hành cấp *quy trình + pháp lý + KPI*.
**Không trộn nhân vật/giọng giữa các dịch vụ.**

---

## Quick start (3 bước)

1. **Instructions:** dán toàn bộ khối giữa hai vạch ▼▲ trong [`SYSTEM-PROMPT.md`](SYSTEM-PROMPT.md) vào ô **Chỉ dẫn** (Gemini) / **Instructions** (ChatGPT) / **Project instructions** (Claude).
2. **Knowledge:** upload 5 file `.md` trong `knowledge/`.
3. **Test:** chạy câu lệnh smoke test bên dưới.

**Câu lệnh đầu tiên để test:**

```
Bạn là ai, làm được gì, đang nạp dịch vụ nào? Liệt kê 4 mode và cho biết
có bao nhiêu nhân vật, bao nhiêu format, bao nhiêu hook trong Tri thức.
```

Đúng thì Agent trả lời: Media Content Producer · dịch vụ Giảm béo đa khoa · 4 mode SCRIPT/BATCH/CALENDAR/HOOK · 5 nhân vật (NV1–NV5) · 17 format (F01–F17) · 86 hook (H01–H86).

---

## Cấu trúc repo

```
SYSTEM-PROMPT.md                    Bộ não Agent (dán vào Instructions)
README.md                           File này
knowledge/
├── giambeo-plan.md                 Trụ cột P1–P5 · Nhân vật NV1–NV5 · Bối cảnh S1–S10
│                                   · Nhân vật phụ NP1–NP4 · Nguyên mẫu khách A1–A5
├── giambeo-format-bank.md          17 format F01–F17: cấu trúc dựng, thời lượng, batch
├── giambeo-hook-bank.md            86 hook H01–H86 theo cụm insight
├── giambeo-script-samples.md       10 kịch bản mẫu KB-01–KB-10 (chuẩn đầu ra)
└── media-production.md             Quy trình 7 bước · lịch batch · call sheet · ekip
                                    · KPI 3 tầng · checklist pháp lý 12 điểm
```

---

## Bốn mode

| Mode | Dùng khi | Đầu ra |
|---|---|---|
| **SCRIPT** | Cần kịch bản quay | Meta đầy đủ → phân cảnh bấm giờ theo giây → chữ trên màn hình → CTA → lưu ý pháp lý |
| **BATCH** | Cần gom clip thành buổi quay | Call sheet theo khung giờ, gom theo bối cảnh, kèm trạng thái consent |
| **CALENDAR** | Cần lịch xuất bản | Bảng phẳng 14 cột, 3 bài/ngày, tự động xuất file |
| **HOOK** | Cần chủ đề mới | Bảng 9 cột theo cụm insight, gợi ý format, trạng thái duyệt |

---

## Công thức ra lệnh

```
[Mode] + [số lượng] + [nhân vật/trụ cột/tầng phễu] + [ràng buộc]
```

**Ví dụ dùng được ngay:**

```
SCRIPT: Viết 3 kịch bản cho NV2 (Dinh dưỡng), trụ cột P2, quay tại S4,
dùng hook trong cụm "Ăn kiêng sai cách". Mỗi clip 30–45s.
```

```
HOOK: Tuần này inbox nhiều câu hỏi "uống thuốc giảm cân có hại gan không".
Sinh 5 hook cho cụm insight này, phân bổ cho NV1 và NV5.
```

```
BATCH: Gom 28 clip cho Batch lớn 2A. Ưu tiên F01/F07 cần khách hàng thật.
Xuất call sheet theo khung giờ.
```

```
CALENDAR: Lập lịch xuất bản tuần 1 tháng 10, 3 bài/ngày, đúng tỷ trọng
trụ cột. Trạng thái mặc định "Chưa quay".
```

---

## Quy trình chuẩn của Agent

1. Làm rõ yêu cầu → xác định dịch vụ + mode
2. Đọc Tri thức, tra hook bank trước khi sáng tác
3. Trình **spec ngắn** trong chat
4. **Dừng chờ "ok"**
5. Triển khai + tự rà theo checklist §17

Yêu cầu sửa nhỏ (đổi 1 hook, 1 phân cảnh, 1 CTA) → làm trực tiếp, bỏ bước spec.

---

## Guardrail then chốt

Agent **không bao giờ**: cam kết số cân/kết quả · dùng "100% / khỏi hoàn toàn / không đau / số 1" · chẩn đoán cá nhân qua bình luận · nêu tên biệt dược hay liều dùng · bịa số liệu, ca bệnh, giá, thông tin bác sĩ · để nhân vật nói ngoài lãnh địa chuyên môn.

Mọi kịch bản y khoa đều gắn dòng **"Cần bác sĩ kiểm duyệt ký duyệt trước khi quay."** Số liệu thiếu → `⚠ Cần xác minh`.

---

## Thêm dịch vụ mới

Chỉ thêm 4 file `knowledge/<dịch-vụ>-plan|format-bank|hook-bank|script-samples.md` theo đúng cấu trúc của bộ `giambeo-*`. **Không sửa `SYSTEM-PROMPT.md`.** File `media-production.md` dùng chung, chỉ sửa khi quy trình vận hành thực sự thay đổi.

---

*Quyết định cuối luôn thuộc người dùng. Không có chữ ký bác sĩ kiểm duyệt thì không bấm máy.*
"# Agent-Media" 
