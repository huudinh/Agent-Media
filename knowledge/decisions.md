# KNOWLEDGE — SỔ QUYẾT ĐỊNH (DECISION REGISTRY)

> **File này là nơi con người ký, không phải nơi Agent viết.**
> Agent ĐỌC file này trước mọi tác vụ và tuân theo. Agent **không được tự sửa file này**.
> Mỗi mục là một chỗ mà Tri thức chưa nói rõ hoặc nói mâu thuẫn — nghĩa là một chỗ **phải có người chọn**.

---

## Cách dùng — 3 câu

1. **Xem còn nợ gì:** gõ `TRẠNG THÁI QUYẾT ĐỊNH` → Agent in bảng dưới đây kèm ảnh hưởng.
2. **Chốt một điểm:** gõ `DP04 = B` (thêm lý do nếu muốn: `DP04 = B vì ngân sách quý này không thêm format mới`).
3. **Người phụ trách repo** cập nhật dòng tương ứng ở đây: trạng thái 🟢, điền lựa chọn, tên người chốt, ngày.

Khi một điểm **chưa chốt**, Agent vẫn chạy được — nhưng phải dùng đúng **Mặc định khung** ghi trong mục đó, gắn nhãn `[MẶC ĐỊNH KHUNG · DPxx · chưa ai chốt]`, và liệt kê ở **Khối lựa chọn** cuối đầu ra. Agent **không được im lặng chọn giùm**.

---

## Bảng trạng thái

| Mã | Điểm quyết định | Ảnh hưởng tới | Mặc định khung | Trạng thái | Đã chốt là | Người chốt | Ngày |
|---|---|---|---|---|---|---|---|
| DP01 | Nguồn chân lý của Tri thức: workbook hay file `.md`? | Toàn bộ | A | 🔴 Chưa chốt | | | |
| DP02 | Trụ cột đi theo Format hay theo Hook? (21 hook lệch) | CALENDAR · SCRIPT · HOOK | A | 🔴 Chưa chốt | | | |
| DP03 | Cột "Sản lượng/tháng" là trần, hạn mức hay gợi ý? | CALENDAR · BATCH | A | 🔴 Chưa chốt | | | |
| DP04 | Trụ cột P3 cần 18 clip/tháng nhưng trần chỉ 8–12 | CALENDAR | C | 🔴 Chưa chốt | | | |
| DP05 | Chuẩn kịch bản: nâng 10 mẫu lên §12 hay nới §12? | SCRIPT | A | 🔴 Chưa chốt | | | |
| DP06 | Có làm mẫu chuẩn cho BATCH · CALENDAR · HOOK không? | 3 mode | A | 🔴 Chưa chốt | | | |
| DP07 | Quy tắc luân phiên kênh theo khung giờ | CALENDAR | A | 🔴 Chưa chốt | | | |
| DP08 | Bối cảnh S7 thuộc nhân vật nào? | SCRIPT · BATCH | A | 🔴 Chưa chốt | | | |
| DP09 | SLA trả lời bình luận: 30 hay 60 phút? | Vận hành | B | 🔴 Chưa chốt | | | |
| DP10 | Ngưỡng tự động của Agent — khi nào được chạy không hỏi | Toàn bộ | A | 🔴 Chưa chốt | | | |

**Đang nợ: 10/10.** Không điểm nào chặn Agent chạy, nhưng DP02 và DP04 làm **mode CALENDAR không thể đúng tỷ trọng** cho tới khi được chốt.

---

# Chi tiết

## DP01 — Nguồn chân lý của Tri thức

- **Ảnh hưởng:** toàn bộ · **Mặc định khung: A**
- **Vấn đề:** `knowledge/*.md` là bản chép lại từ `documents/KEHOACH_TRUST_CONTENT_GIAMBEO_DAKHOA.xlsx` (12 sheet: `01_HUONG_DAN` … `11_CHECKLIST_PHAP_LY`) và Google Docs trong `documents/link.txt`. Hiện **không có quy tắc nào nói bản nào thắng khi hai bên lệch nhau**. Đã đối chiếu: 86/86 hook khớp — nhưng không có gì đảm bảo lần sửa sau vẫn khớp.

| PA | Nội dung | Được gì | Mất gì |
|---|---|---|---|
| **A** | `knowledge/*.md` là **bản chuẩn**. Workbook & Google Docs là tài liệu nguồn/lịch sử, chỉ đọc. | Agent chỉ đọc một nơi. Diff xem được trên git. | Team quen Excel phải sửa file `.md`. |
| B | Workbook là **bản chuẩn**. Mỗi lần đổi thì xuất lại `.md`. | Team làm việc trên công cụ quen thuộc. | Cần người/kịch bản xuất lại; `.md` dễ lỗi thời; git diff khó đọc. |
| C | Song song, có **quy trình đồng bộ hằng tuần** + người chịu trách nhiệm. | Cả hai bên đều dùng được. | Tốn công nhất, dễ trôi nhất. Cần thêm 1 vai. |

- **Đề xuất: A** — Agent chỉ có thể đọc file được nạp vào Knowledge; giữ đúng một nơi là cách rẻ nhất để không bao giờ sai nguồn.
- **Hệ quả nếu chọn A:** thêm một dòng vào đầu mỗi file `knowledge/*.md`: *"Bản chuẩn. Nguồn gốc: workbook … ngày …"*. Workbook chuyển vào `documents/` như kho lưu (đã đúng vị trí).
- **Chốt:** `DP01 = ___` · Người chốt: ________ · Ngày: ________

---

## DP02 — Trụ cột đi theo Format hay theo Hook?

- **Ảnh hưởng:** CALENDAR · SCRIPT · HOOK · mọi báo cáo tỷ trọng · **Mặc định khung: A**
- **Vấn đề:** `SYSTEM-PROMPT §6` bắt mỗi clip thuộc **đúng 1 trụ cột và đúng 1 format**. Nhưng format bank gán cứng mỗi format một trụ cột, còn hook bank gán trụ cột khác cho **21/86 hook**. Đã đối chiếu workbook gốc: **lệch y hệt** → đây là chủ ý/điểm bỏ ngỏ của kế hoạch gốc, không phải lỗi chép.

| Hook | Trụ cột ở hook bank | Format gợi ý | Trụ cột của format |
|---|---|---|---|
| H10, H12, H16 | P1 | F16 | P2 |
| H77 | P4 | F16 | P2 |
| H11, H19, H22 | P1 | F01 | P2 |
| H17, H48 | P1 | F07 | P2 |
| H26, H31, H33, H35, H37, H41, H45 | P1 | F04 | P2 |
| H27 | P4 | F02 | P1 |
| H57 | P1 | F12 | P4 |
| H65, H68, H71 | P1 | F13 | P4 |

| PA | Nội dung | Được gì | Mất gì |
|---|---|---|---|
| **A** | **Trụ cột đi theo FORMAT.** Sửa cột `Trụ cột` của 21 hook cho khớp. | Tỷ trọng tính được bằng máy, không tranh cãi. Đúng §6. | Mất sắc thái: H31 "đổi thứ tự chị ăn" vốn là bài *giải mã cơ thể* (P1) sẽ bị tính là *bằng chứng & chỉ số* (P2). |
| B | **Trụ cột đi theo HOOK.** Bỏ cột `Trụ cột` cứng trong format bank, để "linh hoạt". | Giữ đúng ý đồ nội dung của từng hook. | Format bank mất một trục phân loại; khó ước lượng tỷ trọng khi lên lịch batch. |
| C | **Tách hai khái niệm.** `Trụ cột nội dung` (theo hook, dùng để báo cáo & tính tỷ trọng) và `Trụ cột sản xuất` (theo format, dùng để gom buổi quay). | Không mất gì về mặt ý nghĩa. Phản ánh đúng thực tế. | Thêm 1 cột vào CALENDAR (15 cột) và vào hook bank. Người xem bảng phải hiểu hai khái niệm. |

- **Đề xuất: A** cho quý đầu — đơn giản, chạy được ngay, không đổi schema 14 cột. Cân nhắc chuyển sang **C** từ quý 2 nếu team thấy báo cáo tỷ trọng bị méo.
- **Chốt:** `DP02 = ___` · Người chốt: ________ · Ngày: ________

---

## DP03 — Cột "Sản lượng/tháng" nghĩa là gì?

- **Ảnh hưởng:** CALENDAR · BATCH · **Mặc định khung: A**
- **Vấn đề:** Cộng cột `Sản lượng/tháng` của F01–F17 ra **113–151 clip/tháng**, trong khi kế hoạch chốt **90 video/tháng**. Không có chỗ nào nói đây là trần hay hạn mức.

| PA | Nội dung | Hệ quả khi lên lịch |
|---|---|---|
| **A** | **Trần** — không được vượt, không bắt buộc lấp đầy. | Agent lấp 90 slot bằng cách phân bổ theo **tỷ trọng trụ cột**, dùng cột này chỉ để chặn trên. |
| B | **Hạn mức phải lấp** — mỗi format phải ra đúng số đó. | Không khả thi: tổng tối thiểu đã là 113 > 90. Phải viết lại toàn bộ dải. |
| C | **Chỉ là gợi ý tham khảo**, không ràng buộc. | Agent tự do hơn nhưng mất một hàng rào chống lạm dụng format rẻ (F10, F02). |

- **Đề xuất: A** — giữ nguyên bảng hiện có, chỉ cần thêm một dòng chú thích vào `giambeo-format-bank.md`.
- **Chốt:** `DP03 = ___` · Người chốt: ________ · Ngày: ________

---

## DP04 — Trụ cột P3 không đạt được tỷ trọng

- **Ảnh hưởng:** CALENDAR · **Mặc định khung: C**
- **Vấn đề:** P3 (Hành trình người thật) = 20% = **18 clip/tháng**. Nhưng chỉ **F08** phục vụ P3, trần **8–12 clip/tháng**. Thiếu tối thiểu **6 clip/tháng**, không format nào lấp được.

| Trụ cột | Trần format/tháng | Chỉ tiêu kế hoạch | Chênh |
|---|---|---|---|
| P1 | 48–62 | 27 | Thừa |
| P2 | 32–42 | 22 | Thừa |
| **P3** | **8–12** | **18** | 🔴 **Thiếu ≥ 6** |
| P4 | 17–25 | 14 | Thừa |
| P5 | 8–10 | 9 | Vừa khít |

| PA | Nội dung | Được gì | Mất gì |
|---|---|---|---|
| A | **Thêm format `F18 — Lời nhắn của khách`** (15–20s, khách tự quay bằng điện thoại sau buổi tái khám, batch rất cao, 6–10 clip/tháng). | Giữ đúng 20% P3 — trụ cột nuôi chuyển đổi mạnh nhất. Chi phí sản xuất gần bằng 0. | Phải viết thêm 1 format vào bank; cần mẫu consent riêng cho clip khách tự quay. |
| B | **Nâng trần F08 lên 18–20/tháng.** | Không đổi cấu trúc bank. | F08 là docu 60–90s, tốn hậu kỳ nhất; 18 clip/tháng vượt năng lực 2 editor hiện có. |
| C | **Hạ tỷ trọng P3 xuống 12%** (≈11 clip), chia 8% dôi ra cho P1 và P4. | Khớp ngay năng lực thật, không cần thêm gì. | Giảm trọng số trụ cột gần khách nhất; lệch kế hoạch gốc — cần người ký. |

- **Đề xuất: A** nếu quý này còn ngân sách quay bám; **C** nếu không. Mặc định khung để **C** vì nó là phương án duy nhất chạy được ngay mà không cần thêm nguồn lực.
- **Chốt:** `DP04 = ___` · Người chốt: ________ · Ngày: ________

---

## DP05 — Chuẩn kịch bản: nâng mẫu hay nới template?

- **Ảnh hưởng:** SCRIPT · **Mặc định khung: A**
- **Vấn đề:** `SYSTEM-PROMPT §12` yêu cầu 9 phần và bảng meta 7 trường. Nhưng **10/10 kịch bản mẫu** — vốn là "chuẩn đầu ra" — đều thiếu:

| Thiếu gì | Ở đâu |
|---|---|
| Phần **"Cần xác minh"** | KB-01 → KB-10 (0/10 có) |
| Cột **"Tầng phễu"** trong bảng meta | KB-01 → KB-10 (0/10 có) |
| Dòng **"Cần bác sĩ kiểm duyệt ký duyệt trước khi quay."** | KB-01 → KB-10 (0/10 có) |
| Gán 2 format cho 1 clip (`F07 + F14`) — trái §6 | KB-07 |
| Gán 2 hook cho 1 clip (`H43 + H44`, `H74 + H67`) — trái "1 hook = 1 video" | KB-07, KB-10 |

Agent bắt chước mẫu → lỗi lan sang mọi kịch bản mới. Đây là **mâu thuẫn giữa luật và ví dụ**; phải chọn bên nào thắng.

| PA | Nội dung | Được gì | Mất gì |
|---|---|---|---|
| **A** | **Luật thắng.** Cập nhật cả 10 mẫu cho đủ §12. | Một chuẩn duy nhất, Agent không phải đoán. | ~2 giờ sửa 10 file mẫu. |
| B | **Ví dụ thắng.** Nới §12: "Cần xác minh" và "Tầng phễu" thành tuỳ chọn. | Không phải sửa mẫu. | Mất hai hàng rào chống bịa số (đây chính là chỗ Agent hay bịa nhất). Không khuyến nghị. |
| C | Giữ mẫu, đánh dấu rõ là **"mẫu rút gọn"**, viết thêm **1 mẫu đầy đủ** làm chuẩn vàng. | Rẻ, nhanh. | Agent có hai chuẩn để bắt chước — vẫn còn chỗ trôi dạt. |

- **Đề xuất: A.** "Cần xác minh" là cơ chế chống bịa số liệu — bỏ nó là bỏ hàng rào an toàn quan trọng nhất của mode SCRIPT.
- **Chốt:** `DP05 = ___` · Người chốt: ________ · Ngày: ________

---

## DP06 — Mẫu chuẩn cho BATCH · CALENDAR · HOOK

- **Ảnh hưởng:** 3/4 mode · **Mặc định khung: A**
- **Vấn đề:** chỉ mode SCRIPT có gold standard (`giambeo-script-samples.md`). Ba mode còn lại không có mẫu nào trong Tri thức → đầu ra trôi dạt mỗi phiên một khác. Bản mẫu tạm đang nằm ở `README.md` mục *Ví dụ mẫu đầu ra*, nhưng **Agent không đọc được README** (không nằm trong Knowledge).

| PA | Nội dung | Được gì | Mất gì |
|---|---|---|---|
| **A** | Tách thành `knowledge/giambeo-output-samples.md` và **upload vào Knowledge**. | Agent đọc được → 3 mode ổn định như SCRIPT. | Thêm 1 file phải upload (6 file thay vì 5). |
| B | Nhúng mẫu thẳng vào `SYSTEM-PROMPT.md`. | Không thêm file. | Phình system prompt; và mẫu là *của dịch vụ*, không trung tính — trái kiến trúc 3 tầng. |
| C | Để nguyên ở README, chấp nhận trôi dạt. | Không tốn gì. | 3/4 mode không có chuẩn nghiệm thu thật. |

- **Đề xuất: A.**
- **Chốt:** `DP06 = ___` · Người chốt: ________ · Ngày: ________

---

## DP07 — Quy tắc luân phiên kênh

- **Ảnh hưởng:** CALENDAR · **Mặc định khung: A**
- **Vấn đề:** `§14` yêu cầu "Kênh luân phiên **theo tài liệu dịch vụ**", nhưng `giambeo-plan.md` chỉ ghi *"TikTok + Reels · Facebook Page/Group"* mà không nói slot nào lên kênh nào → Agent buộc phải tự bịa, mỗi phiên một khác.

| PA | 07:00 | 12:15 | 20:00 | Lý do |
|---|---|---|---|---|
| **A** | Facebook Page | TikTok | Reels + TikTok | Sáng là khung đọc của nhóm 35+ trên Facebook; tối là khung short-form mạnh nhất. |
| B | TikTok | Facebook Page | Reels + TikTok | Ưu tiên TikTok khung sáng để bắt trend sớm. |
| C | Đăng cả 3 kênh mọi khung giờ | | | Tối đa tiếp cận, nhưng loãng và không đo được kênh nào thắng. |

- **Đề xuất: A** — và **đo lại sau 30 ngày** rồi chốt bằng dữ liệu thật thay vì phỏng đoán.
- **⚠ Cần xác minh:** phòng khám hiện có Reels riêng hay dùng chung Facebook Page?
- **Chốt:** `DP07 = ___` · Người chốt: ________ · Ngày: ________

---

## DP08 — Bối cảnh S7 thuộc nhân vật nào?

- **Ảnh hưởng:** SCRIPT · BATCH · **Mặc định khung: A**
- **Vấn đề:** Bảng bối cảnh ghi S7 (Phòng máy công nghệ giảm béo) dùng cho NV1/NV5/NV4, và format F11 dùng S6/S7. Nhưng **S7 không xuất hiện ở dòng "Bối cảnh quay" của bất kỳ nhân vật nào** trong character bible → Agent do dự hoặc gán bừa.

| PA | Nội dung |
|---|---|
| **A** | Thêm S7 vào "Bối cảnh quay" của **NV1, NV4, NV5** (khớp bảng bối cảnh và F11). |
| B | Chỉ **NV4** sở hữu S7 (người trực tiếp vận hành máy trị liệu/công nghệ). |
| C | Bỏ S7 khỏi F11, chỉ dùng S6 — nếu phòng máy chưa sẵn sàng để quay. |

- **Đề xuất: A.**
- **Chốt:** `DP08 = ___` · Người chốt: ________ · Ngày: ________

---

## DP09 — SLA trả lời bình luận

- **Ảnh hưởng:** vận hành (không ảnh hưởng đầu ra Agent) · **Mặc định khung: B**
- **Vấn đề:** `media-production.md` B7 ghi *"trực bình luận **60 phút** đầu"*; bảng ekip ghi *"trả lời bình luận trong **30 phút**"*.

| PA | Nội dung |
|---|---|
| A | 30 phút cho mọi bình luận. |
| **B** | Hai chỉ số khác nhau, không mâu thuẫn: **trực 60 phút đầu** sau khi đăng (giai đoạn quyết định phân phối) · **trả lời trong 30 phút** cho bình luận đến ngoài khung đó. Ghi rõ lại cho hết hiểu nhầm. |
| C | Nới cả hai lên 60 phút. |

- **Đề xuất: B** — nhiều khả năng đây là ý ban đầu, chỉ diễn đạt chưa rõ.
- **Chốt:** `DP09 = ___` · Người chốt: ________ · Ngày: ________

---

## DP10 — Ngưỡng tự động của Agent

- **Ảnh hưởng:** toàn bộ cách làm việc · **Mặc định khung: A**
- **Vấn đề:** Đây là điểm quyết định về **chính cái khung này**: bạn muốn Agent hỏi nhiều hay chạy nhiều?

| PA | Nội dung | Hợp khi |
|---|---|---|
| **A** | **Như §4 hiện tại:** việc lớn → trình spec, dừng chờ "ok". Việc nhỏ (đổi 1 hook, 1 phân cảnh, 1 CTA) → làm thẳng. | Mặc định. Cân bằng giữa tốc độ và kiểm soát. |
| B | **Luôn hỏi** trước mọi đầu ra, kể cả sửa nhỏ. | Giai đoạn đầu, team chưa tin Agent, nội dung y khoa nhạy cảm. |
| C | **Chạy hết, chỉ dừng khi chạm §11** (y khoa · pháp lý · số liệu · consent). | Khi team đã chạy trơn và cần sản lượng. |

- **Lưu ý:** dù chọn PA nào, **4 việc ở §19.4 luôn chặn cứng** — không có mặc định, không có ngoại lệ: nội dung y khoa chưa ký duyệt · số liệu/giá/ca bệnh · consent · sửa file Tri thức.
- **Đề xuất: A** cho 30 ngày đầu, xem lại ở mốc cuối tháng 1.
- **Chốt:** `DP10 = ___` · Người chốt: ________ · Ngày: ________

---

# Phụ lục — Sửa kỹ thuật (KHÔNG cần ai quyết)

Những mục dưới đây là lỗi rõ ràng, chỉ có một cách đúng. **Chưa áp dụng** vì phụ thuộc `DP01` — cần biết sửa vào `knowledge/*.md` hay vào workbook gốc trước đã.

| Mã | Lỗi | Vị trí | Cách sửa | Căn cứ |
|---|---|---|---|---|
| SK01 | Ghi "checklist **8 điểm**" | `media-production.md` dòng 24 và 90 | Đổi thành **12 điểm** | Sheet `11_CHECKLIST_PHAP_LY` trong workbook gốc ghi rõ *"Số điểm đã đạt: 0 / 12"*, và §7 liệt kê đủ L01–L12 |
| SK02 | Lặp dòng tiêu đề bảng tra nhanh 2 lần | `giambeo-format-bank.md` dòng 8–10 | Xoá dòng thừa | Lỗi dựng bảng |
| SK03 | Sót khối template rỗng `### Mã — Tên format` với nội dung placeholder | `giambeo-format-bank.md` dòng 31–36 | Xoá cả khối | Lỗi sinh file |
| SK04 | Lặp dòng tiêu đề bảng KPI 2 lần | `media-production.md` dòng 114–116 | Xoá dòng thừa | Lỗi dựng bảng |
| SK05 | Bullet hỏng `- **________________:**` + trùng bullet "Chữ trên màn hình" | `giambeo-script-samples.md` KB-10, dòng ~277 và 281 | Xoá bullet rỗng, gộp 2 bullet trùng | Lỗi soạn thảo |
| SK06 | Trỏ tới sheet `05_NGAN_HANG_HOOK` · `06_LICH_NOI_DUNG` · `10_KPI_THEO_DOI` · `11_CHECKLIST_PHAP_LY` mà không nói ở đâu | `media-production.md` dòng 21, 23, 24, 27 | Ghi rõ: *"sheet … trong `documents/KEHOACH_TRUST_CONTENT_GIAMBEO_DAKHOA.xlsx`"* | Các sheet **có thật** trong workbook; chỉ thiếu đường dẫn. Lưu ý tên thật là `06_LICH_NOI_DUNG_90N` |

> Sau khi chốt `DP01`, gõ `ÁP DỤNG SK` để người phụ trách repo thực hiện cả 6 mục.

---

# Nhật ký quyết định

| Ngày | Mã | Từ → Thành | Người chốt | Lý do |
|---|---|---|---|---|
| | | | | |

> Mỗi lần đổi một quyết định đã chốt, thêm một dòng ở đây. Không xoá dòng cũ — lý do cũ là thứ giúp không quay lại tranh luận đã xong.
