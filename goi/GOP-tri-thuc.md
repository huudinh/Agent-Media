# TRI THỨC — Media Content Producer (HCI Group)
> File này gộp **6 module tri thức** từ `knowledge/`. Sinh tự động ngày 2026-10-22 bằng `python tools/gop-tham-khao.py`.
> ⛔ **Không sửa file này** — sửa ở bản rời trong thư mục nguồn rồi chạy lại lệnh trên.

**Cách đọc:** mỗi phần bắt đầu bằng dòng `===== tên file =====` và là **một đơn vị tri thức riêng**. Tham chiếu dạng `[[tên-file]]` trong văn bản trỏ tới **phần cùng tên ngay trong file này**, không phải file bên ngoài.

## MỤC LỤC

| # | File | Cỡ |
|---|---|---|
| 1 | `decisions.md` | 18.4 KB |
| 2 | `giambeo-format-bank.md` | 12.1 KB |
| 3 | `giambeo-hook-bank.md` | 18.4 KB |
| 4 | `giambeo-plan.md` | 16.7 KB |
| 5 | `giambeo-script-samples.md` | 19.6 KB |
| 6 | `media-production.md` | 22.5 KB |


===== decisions.md =====

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


===== giambeo-format-bank.md =====

# KNOWLEDGE — NGÂN HÀNG FORMAT (17 khuôn nội dung)

> Format là khuôn lặp lại được. Toàn bộ 270 slot trong 90 ngày đều lấp bằng 17 khuôn này — **không có video "sáng tạo tự do"**.
> Khi viết kịch bản, Agent BẮT BUỘC chọn 1 mã format và bám đúng "Cấu trúc dựng" của format đó.

## Bảng tra nhanh

| Mã | Tên format | Thời lượng | Nhân vật | Bối cảnh | Trụ cột | Sản lượng/tháng | Khả năng batch |
|---|---|---|---|---|---|---|---|
| Mã | Tên format | Thời lượng | Nhân vật | Bối cảnh | Trụ cột | Sản lượng/tháng | Khả năng quay batch |
| F01 | ĐỌC CHỈ SỐ | 45–60s | NV1 | S1/S2 | P2 | 8–10/tháng | Cao |
| F02 | SỰ THẬT HAY LỜI ĐỒN | 20–30s | Tất cả | S10 | P1 | 16–20/tháng | Rất cao — trục batch |
| F03 | BÁC SĨ PHẢN ỨNG | 30–45s | NV1, NV5 | S10 | P1 | 6–8/tháng | Cao |
| F04 | BỮA ĂN THẬT | 30–45s | NV2 | S4 | P2 | 10–12/tháng | Rất cao |
| F05 | ĐI CHỢ CÙNG CHUYÊN GIA | 60–90s | NV2 | Ngoại cảnh | P2 | 2–4/tháng | Trung bình — chi phí sản xuất cao |
| F06 | SỬA 1 LỖI TẬP | 20–30s | NV3 | S5 | P1 | 8–10/tháng | Rất cao |
| F07 | TEST TẠI CHỖ | 30–45s | NV1, NV3, NV4 | S2/S5 | P2 | 8–10/tháng | Rất cao — chỉ số lưu cao nhất |
| F08 | HÀNH TRÌNH 90 NGÀY | 60–90s | Tất cả + KH thật | Đa bối cảnh | P3 | 8–12/tháng (2–3 nhân vật song song) | Cao — nuôi chuyển đổi |
| F09 | NGÀY ĐẦU TIÊN | 60s | NP1 dẫn | S9→S2→S1 | P4 | 2–3/tháng | Cao |
| F10 | HỎI NHANH ĐÁP GỌN | 15–20s | Tất cả | S10 | P1 | 12–16/tháng | Rất cao — rẻ nhất, quay 15 clip/giờ |
| F11 | TRONG PHÒNG MÁY | 30–45s | NV1, NV4, NV5 | S6/S7 | P4 | 4–6/tháng | Trung bình |
| F12 | HỘI CHẨN ĐA KHOA | 60–90s | 2–3 nhân vật | S1 (bàn hội chẩn) | P4 | 3–4/tháng | Rất cao — khác biệt lớn nhất so với đối thủ |
| F13 | TRƯỚC KHI BẠN QUYẾT ĐỊNH | 45–60s | NV5 | S8/S1 | P4 | 4–6/tháng | Cao — chuyển đổi BOF |
| F14 | GỠ ĐAU ĐỂ TẬP ĐƯỢC | 30–45s | NV4, NV3 | S6/S5 | P1 | 6–8/tháng | Cao |
| F15 | HẬU TRƯỜNG & MINH BẠCH | 20–30s | Tất cả | S3/S8/S9 | P4 | 4–6/tháng | Trung bình — nhưng quyết định niềm tin |
| F16 | CON SỐ BIẾT NÓI | 20–30s | NV1, NV2 | S10 | P2 | 4–6/tháng | Trung bình |
| F17 | ĐỜI THƯỜNG PHÒNG KHÁM | 15–30s | Tất cả | Bất kỳ | P5 | 8–10/tháng | Rất cao — quay bằng điện thoại |

## Chi tiết từng format

### Mã — Tên format

- **Thời lượng:** Thời lượng · **Nhân vật:** Nhân vật · **Bối cảnh:** Bối cảnh · **Trụ cột:** Trụ cột
- **Sản lượng/tháng:** Sản lượng/tháng · **Khả năng quay batch:** Khả năng quay batch
- **Mô tả:** Mô tả
- **Cấu trúc dựng:** Cấu trúc dựng

### F01 — ĐỌC CHỈ SỐ

- **Thời lượng:** 45–60s · **Nhân vật:** NV1 · **Bối cảnh:** S1/S2 · **Trụ cột:** P2
- **Sản lượng/tháng:** 8–10/tháng · **Khả năng quay batch:** Cao
- **Mô tả:** Bác sĩ đọc kết quả InBody/xét nghiệm của một khách hàng thật ngay trước mặt họ, chỉ ra 1 phát hiện bất ngờ.
- **Cấu trúc dựng:** Hook = con số lạ (3s) → chỉ vào màn hình (10s) → giải thích cơ chế (25s) → điều sẽ làm tiếp (10s) → CTA

### F02 — SỰ THẬT HAY LỜI ĐỒN

- **Thời lượng:** 20–30s · **Nhân vật:** Tất cả · **Bối cảnh:** S10 · **Trụ cột:** P1
- **Sản lượng/tháng:** 16–20/tháng · **Khả năng quay batch:** Rất cao — trục batch
- **Mô tả:** Một câu đồn phổ biến hiện lên màn hình, chuyên gia bác bỏ hoặc xác nhận trong 20 giây.
- **Cấu trúc dựng:** Câu đồn (3s) → 'Sai/Đúng một nửa' (2s) → lý do (15s) → câu chốt

### F03 — BÁC SĨ PHẢN ỨNG

- **Thời lượng:** 30–45s · **Nhân vật:** NV1, NV5 · **Bối cảnh:** S10 · **Trụ cột:** P1
- **Sản lượng/tháng:** 6–8/tháng · **Khả năng quay batch:** Cao
- **Mô tả:** Xem và phản ứng với quảng cáo giảm cân, mẹo trên mạng, hoặc câu hỏi cực đoan từ 'người hoài nghi' (NP4).
- **Cấu trúc dựng:** Cắt clip nguồn (5s, che nhãn hiệu) → biểu cảm (2s) → phân tích (25s) → lời khuyên thay thế

### F04 — BỮA ĂN THẬT

- **Thời lượng:** 30–45s · **Nhân vật:** NV2 · **Bối cảnh:** S4 · **Trụ cột:** P2
- **Sản lượng/tháng:** 10–12/tháng · **Khả năng quay batch:** Rất cao
- **Mô tả:** Dựng một khay ăn thật theo phác đồ, đối chiếu với bữa ăn 'healthy' phổ biến.
- **Cấu trúc dựng:** Đối chiếu 2 khay (3s) → cân từng món (20s) → con số calo/protein (10s) → cách áp dụng

### F05 — ĐI CHỢ CÙNG CHUYÊN GIA

- **Thời lượng:** 60–90s · **Nhân vật:** NV2 · **Bối cảnh:** Ngoại cảnh · **Trụ cột:** P2
- **Sản lượng/tháng:** 2–4/tháng · **Khả năng quay batch:** Trung bình — chi phí sản xuất cao
- **Mô tả:** Đi siêu thị/chợ với ngân sách cụ thể, chọn đồ cho 3 ngày ăn theo phác đồ.
- **Cấu trúc dựng:** Ngân sách (3s) → chọn & giải thích (50s) → tổng kết giỏ hàng + hoá đơn (15s)

### F06 — SỬA 1 LỖI TẬP

- **Thời lượng:** 20–30s · **Nhân vật:** NV3 · **Bối cảnh:** S5 · **Trụ cột:** P1
- **Sản lượng/tháng:** 8–10/tháng · **Khả năng quay batch:** Rất cao
- **Mô tả:** Một lỗi kỹ thuật, quay split-screen sai/đúng trên chính khách hàng.
- **Cấu trúc dựng:** '90% người tập sai điều này' (3s) → sai (7s) → đúng (10s) → khác biệt cảm nhận

### F07 — TEST TẠI CHỖ

- **Thời lượng:** 30–45s · **Nhân vật:** NV1, NV3, NV4 · **Bối cảnh:** S2/S5 · **Trụ cột:** P2
- **Sản lượng/tháng:** 8–10/tháng · **Khả năng quay batch:** Rất cao — chỉ số lưu cao nhất
- **Mô tả:** Một bài test đo được, làm ngay trên khách hàng: InBody, test bàn chân bẹt, test sức mạnh, test xa cách cơ bụng.
- **Cấu trúc dựng:** 'Bạn tự làm được ở nhà trong 20 giây' (3s) → demo (20s) → đọc kết quả (15s) → ý nghĩa

### F08 — HÀNH TRÌNH 90 NGÀY

- **Thời lượng:** 60–90s · **Nhân vật:** Tất cả + KH thật · **Bối cảnh:** Đa bối cảnh · **Trụ cột:** P3
- **Sản lượng/tháng:** 8–12/tháng (2–3 nhân vật song song) · **Khả năng quay batch:** Cao — nuôi chuyển đổi
- **Mô tả:** Docu-series bám 1 khách hàng: ngày 0, tuần 2, tuần 4 (chững lại), tuần 8, ngày 90.
- **Cấu trúc dựng:** Nhắc lại điểm xuất phát (5s) → chuyện tuần này (40s) → chỉ số mới (10s) → điều đang lo

### F09 — NGÀY ĐẦU TIÊN

- **Thời lượng:** 60s · **Nhân vật:** NP1 dẫn · **Bối cảnh:** S9→S2→S1 · **Trụ cột:** P4
- **Sản lượng/tháng:** 2–3/tháng · **Khả năng quay batch:** Cao
- **Mô tả:** POV một người lần đầu đến khám: từ lễ tân đến khi cầm phác đồ. Gỡ nỗi sợ 'không biết vào đó sẽ bị gì'.
- **Cấu trúc dựng:** 'Đây là điều xảy ra trong 90 phút đầu' (3s) → 6 chặng, mỗi chặng 8s → chi phí & thời gian

### F10 — HỎI NHANH ĐÁP GỌN

- **Thời lượng:** 15–20s · **Nhân vật:** Tất cả · **Bối cảnh:** S10 · **Trụ cột:** P1
- **Sản lượng/tháng:** 12–16/tháng · **Khả năng quay batch:** Rất cao — rẻ nhất, quay 15 clip/giờ
- **Mô tả:** Trả lời trực tiếp một bình luận có thật (chụp màn hình bình luận, che tên).
- **Cấu trúc dựng:** Đọc bình luận (4s) → trả lời (12s) → 'câu hỏi tiếp theo để dưới bình luận'

### F11 — TRONG PHÒNG MÁY

- **Thời lượng:** 30–45s · **Nhân vật:** NV1, NV4, NV5 · **Bối cảnh:** S6/S7 · **Trụ cột:** P4
- **Sản lượng/tháng:** 4–6/tháng · **Khả năng quay batch:** Trung bình
- **Mô tả:** Mở một thiết bị ra, giải thích nó làm gì với mô mỡ/cơ/khớp, và ai KHÔNG dùng được.
- **Cấu trúc dựng:** 'Máy này giá gần X trăm triệu — nó làm gì?' (3s) → cơ chế (20s) → ai không dùng được (10s)

### F12 — HỘI CHẨN ĐA KHOA

- **Thời lượng:** 60–90s · **Nhân vật:** 2–3 nhân vật · **Bối cảnh:** S1 (bàn hội chẩn) · **Trụ cột:** P4
- **Sản lượng/tháng:** 3–4/tháng · **Khả năng quay batch:** Rất cao — khác biệt lớn nhất so với đối thủ
- **Mô tả:** Cùng một ca, ba chuyên khoa đưa ba hướng khác nhau và tranh luận công khai trước khi chốt.
- **Cấu trúc dựng:** Giới thiệu ca (8s) → mỗi chuyên khoa 15s → bất đồng (15s) → phương án cuối

### F13 — TRƯỚC KHI BẠN QUYẾT ĐỊNH

- **Thời lượng:** 45–60s · **Nhân vật:** NV5 · **Bối cảnh:** S8/S1 · **Trụ cột:** P4
- **Sản lượng/tháng:** 4–6/tháng · **Khả năng quay batch:** Cao — chuyển đổi BOF
- **Mô tả:** Bác sĩ ngoại khoa nói về chống chỉ định, ca từ chối, rủi ro — chủ động nói điều bất lợi.
- **Cấu trúc dựng:** 'Tuần này tôi từ chối 4 ca' (3s) → lý do từng ca (35s) → ai thì phù hợp (15s)

### F14 — GỠ ĐAU ĐỂ TẬP ĐƯỢC

- **Thời lượng:** 30–45s · **Nhân vật:** NV4, NV3 · **Bối cảnh:** S6/S5 · **Trụ cột:** P1
- **Sản lượng/tháng:** 6–8/tháng · **Khả năng quay batch:** Cao
- **Mô tả:** Xử lý một cơn đau cản trở vận động ở người thừa cân, kèm bài tự tập tại nhà.
- **Cấu trúc dựng:** Triệu chứng quen thuộc (3s) → nguyên nhân cơ học (12s) → thao tác trị liệu (15s) → bài tự tập (10s)

### F15 — HẬU TRƯỜNG & MINH BẠCH

- **Thời lượng:** 20–30s · **Nhân vật:** Tất cả · **Bối cảnh:** S3/S8/S9 · **Trụ cột:** P4
- **Sản lượng/tháng:** 4–6/tháng · **Khả năng quay batch:** Trung bình — nhưng quyết định niềm tin
- **Mô tả:** Quy trình vô khuẩn, cách lưu hồ sơ bệnh án, giấy phép hoạt động, bảng giá bóc tách.
- **Cấu trúc dựng:** Câu hỏi khách hay hỏi thầm (3s) → mở ra cho xem (20s) → cam kết cụ thể

### F16 — CON SỐ BIẾT NÓI

- **Thời lượng:** 20–30s · **Nhân vật:** NV1, NV2 · **Bối cảnh:** S10 · **Trụ cột:** P2
- **Sản lượng/tháng:** 4–6/tháng · **Khả năng quay batch:** Trung bình
- **Mô tả:** Một thống kê từ chính dữ liệu phòng khám (đã ẩn danh): tỷ lệ khách có kháng insulin, tuổi trung bình, cân nặng trung bình...
- **Cấu trúc dựng:** Con số (3s) → nó nghĩa là gì (15s) → điều bạn nên làm

### F17 — ĐỜI THƯỜNG PHÒNG KHÁM

- **Thời lượng:** 15–30s · **Nhân vật:** Tất cả · **Bối cảnh:** Bất kỳ · **Trụ cột:** P5
- **Sản lượng/tháng:** 8–10/tháng · **Khả năng quay batch:** Rất cao — quay bằng điện thoại
- **Mô tả:** Bữa trưa của bác sĩ, ca trực muộn, khách mang quà đến, ngày sinh nhật ekip.
- **Cấu trúc dựng:** Không hook kiến thức — dùng khoảnh khắc thật, chữ trên màn hình kể chuyện

## Quy tắc dùng format

- Format có khả năng batch **Rất cao** (F02, F04, F06, F07, F10, F16) là trục sản lượng — ưu tiên khi cần lấp lịch nhanh.
- F05 (ngoại cảnh) và F08 (docu) chi phí cao → giới hạn đúng sản lượng/tháng đã định, không tăng tuỳ tiện.
- Hai nhân vật cùng nói một chủ đề → BẮT BUỘC dùng F12 Hội chẩn đa khoa (phải có xung đột quan điểm và có kết luận).
- Format phải khớp nhân vật: đề xuất format ngoài "Format sở trường" của nhân vật → phải nêu lý do.


===== giambeo-hook-bank.md =====

# KNOWLEDGE — NGÂN HÀNG HOOK (86 chủ đề)

> Hook là 3 giây đầu, **đọc nguyên văn** trên hình. Agent LUÔN tra bảng này trước khi sáng tác hook mới.
> 1 hook = 1 video. Hook đã dùng → đánh dấu trong lịch xuất bản, không tái sử dụng trong cùng 90 ngày.
> Trạng thái duyệt: **Xanh** (quay ngay) · **Vàng** (sửa góc) · **Đỏ** (loại — ghi lý do để không lặp lại).

| Mã | Cụm insight / nỗi đau | NV | Trụ cột | Phễu | HOOK (3 giây đầu — đọc nguyên văn) | Góc triển khai | Format | Trạng thái |
|---|---|---|---|---|---|---|---|---|
| H01 | Thất bại lặp lại | NV1 | P1 | TOF | Bạn không thiếu ý chí. Bạn thiếu một tờ xét nghiệm. | Liệt kê 5 nguyên nhân sinh học khiến nỗ lực bị vô hiệu hoá | F02 | Chờ duyệt |
| H02 | Thất bại lặp lại | NV1 | P1 | TOF | Giảm 8kg rồi tăng lại 10kg — y học gọi đây là hiệu ứng bập bênh | Giải thích chuyển hoá cơ bản tụt sau ăn kiêng cực đoan | F02 | Chờ duyệt |
| H03 | Thất bại lặp lại | NV2 | P1 | TOF | Mỗi lần bạn nhịn ăn, cơ thể học được cách tiêu ít đi | Vì sao ăn ít mãi rồi vẫn không giảm | F02 | Chờ duyệt |
| H04 | Thất bại lặp lại | NV1 | P2 | MOF | Ba lần giảm cân thất bại — lần thứ tư tôi bắt chị làm việc này trước | Quy trình 90 phút khám đầu tiên | F01 | Chờ duyệt |
| H05 | Thất bại lặp lại | NV1 | P2 | MOF | Cân nặng đứng yên nhưng mỡ giảm 4kg — chị ấy suýt bỏ cuộc vì nhìn nhầm chỉ số | Đọc InBody: cân nặng vs khối mỡ vs khối cơ | F01 | Chờ duyệt |
| H06 | Thất bại lặp lại | NV3 | P1 | TOF | Tuần thứ 4 luôn là tuần chững. Đây là lý do sinh học | Plateau và cách vượt qua mà không cắt thêm calo | F02 | Chờ duyệt |
| H07 | Nguyên nhân nội tiết | NV1 | P1 | TOF | Béo bụng mà tay chân vẫn gầy? Hãy đi kiểm tra cortisol | Stress mạn tính và phân bố mỡ trung tâm | F02 | Chờ duyệt |
| H08 | Nguyên nhân nội tiết | NV1 | P1 | TOF | Nếu bạn thèm ngọt đúng 3 giờ chiều mỗi ngày, đó không phải thói xấu | Dao động đường huyết sau bữa trưa nhiều tinh bột | F02 | Chờ duyệt |
| H09 | Nguyên nhân nội tiết | NV1 | P1 | TOF | Tuyến giáp có thể khiến bạn tăng 5kg mà không ăn thêm gì | Suy giáp và chuyển hoá — dấu hiệu nên đi khám | F02 | Chờ duyệt |
| H10 | Nguyên nhân nội tiết | NV1 | P1 | MOF | Kháng insulin: máu đầy đường nhưng tế bào vẫn đói | Cơ chế kháng insulin bằng mô hình trực quan | F16 | Chờ duyệt |
| H11 | Nguyên nhân nội tiết | NV1 | P1 | MOF | Buồng trứng đa nang làm giảm cân khó hơn — nhưng không phải không giảm được | Phác đồ điều chỉnh cho khách PCOS | F01 | Chờ duyệt |
| H12 | Nguyên nhân nội tiết | NV1 | P1 | TOF | Ngủ dưới 6 tiếng, hormone báo đói tăng lên. Đây là biểu đồ | Leptin – ghrelin và giấc ngủ | F16 | Chờ duyệt |
| H13 | Nguyên nhân nội tiết | NV1 | P2 | MOF | Đây là 5 xét nghiệm tôi luôn chỉ định trước khi nói bất cứ điều gì về cân nặng của bạn | Danh mục xét nghiệm & lý do từng cái | F01 | Chờ duyệt |
| H14 | Nguyên nhân nội tiết | NV1 | P1 | TOF | Tuổi 40 trở đi, cùng chế độ ăn nhưng cơ thể xử lý khác hẳn | Thay đổi nội tiết tuổi trung niên | F02 | Chờ duyệt |
| H15 | Bệnh lý đi kèm | NV1 | P2 | TOF | Gan nhiễm mỡ độ 2 ở tuổi 32 — và anh ấy không uống một giọt rượu | Gan nhiễm mỡ không do rượu ở người thừa cân | F01 | Chờ duyệt |
| H16 | Bệnh lý đi kèm | NV1 | P1 | MOF | Giảm 7% cân nặng có thể đưa men gan về bình thường | Mục tiêu giảm cân theo y học, không theo thẩm mỹ | F16 | Chờ duyệt |
| H17 | Bệnh lý đi kèm | NV1 | P1 | TOF | Vòng bụng nam trên 90cm: con số y học quan tâm hơn cả cân nặng | Đo vòng bụng đúng cách — demo tại chỗ | F07 | Chờ duyệt |
| H18 | Bệnh lý đi kèm | NV1 | P1 | TOF | Ngáy to và buồn ngủ ban ngày có thể là ngưng thở khi ngủ do thừa cân | Mối liên hệ cân nặng – đường thở | F02 | Chờ duyệt |
| H19 | Bệnh lý đi kèm | NV1 | P1 | MOF | Tiền tiểu đường là giai đoạn duy nhất còn quay đầu được | Ngưỡng chỉ số và can thiệp sớm | F01 | Chờ duyệt |
| H20 | Bệnh lý đi kèm | NV1 | P2 | TOF | Mỡ nội tạng không nhìn thấy bằng gương. Chỉ thấy bằng máy này | Demo InBody đo mỡ nội tạng | F07 | Chờ duyệt |
| H21 | Bệnh lý đi kèm | NV4 | P1 | MOF | Mỗi 1kg giảm đi, đầu gối bạn bớt chịu vài kg khi bước xuống cầu thang | Cơ học tải trọng khớp gối | F14 | Chờ duyệt |
| H22 | Bệnh lý đi kèm | NV1 | P1 | MOF | Huyết áp của anh ấy về bình thường trước khi anh ấy giảm hết số cân đặt ra | Cải thiện chỉ số đi trước cải thiện ngoại hình | F01 | Chờ duyệt |
| H23 | Thuốc & lời đồn | NV1 | P1 | TOF | Trà giảm cân làm bạn nhẹ 2kg sau một đêm. Đó là nước, không phải mỡ | Cơ chế lợi tiểu/nhuận tràng và rủi ro | F02 | Chờ duyệt |
| H24 | Thuốc & lời đồn | NV1 | P1 | TOF | Thuốc giảm cân bán trên mạng — tôi đọc bảng thành phần này cho bạn nghe | Đọc nhãn, chỉ ra hoạt chất bị cấm | F03 | Chờ duyệt |
| H25 | Thuốc & lời đồn | NV1 | P1 | MOF | Có nhóm thuốc giảm cân thật, được cấp phép. Nhưng nó không dành cho tất cả mọi người | Chỉ định – chống chỉ định, cần bác sĩ kê đơn | F02 | Chờ duyệt |
| H26 | Thuốc & lời đồn | NV2 | P1 | TOF | Detox 7 ngày: thứ bạn mất là cơ, không phải mỡ | Phân tích thành phần cơ thể trước/sau detox | F04 | Chờ duyệt |
| H27 | Thuốc & lời đồn | NV1 | P4 | TOF | Nếu ai đó cam kết bạn giảm 10kg trong một tháng, hãy hỏi họ đúng một câu này | Dạy khách cách tự sàng lọc cơ sở | F02 | Chờ duyệt |
| H28 | Thuốc & lời đồn | NV5 | P1 | TOF | Bác sĩ phản ứng: quảng cáo 'giảm béo cấp tốc không cần ăn kiêng' | Bóc tách thủ pháp quảng cáo sai sự thật | F03 | Chờ duyệt |
| H29 | Thuốc & lời đồn | NV2 | P1 | TOF | Cà phê giảm cân, kẹo giảm cân, giấm táo — cái nào có bằng chứng? | Xếp hạng 3 mức: có bằng chứng / yếu / không | F02 | Chờ duyệt |
| H30 | Ăn uống | NV2 | P2 | TOF | Bữa sáng này 420 kcal. Bữa sáng 'healthy' bạn hay ăn: 780 kcal | Cân trực tiếp hai khay ăn | F04 | Chờ duyệt |
| H31 | Ăn uống | NV2 | P1 | TOF | Tôi không cấm chị ăn cơm. Tôi đổi thứ tự chị ăn | Rau – đạm – tinh bột và đường huyết sau ăn | F04 | Chờ duyệt |
| H32 | Ăn uống | NV2 | P2 | MOF | Ăn rau trước: đường huyết sau ăn khác biệt thế nào | Demo với máy đo đường huyết liên tục | F07 | Chờ duyệt |
| H33 | Ăn uống | NV2 | P1 | TOF | Bún riêu, phở, bánh mì — chọn thế nào để vẫn giảm cân | Bảng gọi món cho dân văn phòng Hà Nội | F04 | Chờ duyệt |
| H34 | Ăn uống | NV2 | P1 | TOF | Đi ăn cưới mà không phá phác đồ: 3 quy tắc | Ứng xử với bữa tiệc, rượu bia | F02 | Chờ duyệt |
| H35 | Ăn uống | NV2 | P1 | TOF | Một ly trà sữa bằng một tiếng chạy bộ. Nhưng tôi không bắt bạn bỏ nó | Quy tắc đánh đổi có kiểm soát | F04 | Chờ duyệt |
| H36 | Ăn uống | NV2 | P2 | TOF | Đi chợ cùng tôi: 200.000đ cho 3 ngày ăn theo phác đồ | Giỏ hàng thật, hoá đơn thật | F05 | Chờ duyệt |
| H37 | Ăn uống | NV2 | P1 | MOF | Protein: đây là lượng thật sự bạn cần, tính theo cân nặng của bạn | Công thức g/kg và cách chia bữa | F04 | Chờ duyệt |
| H38 | Ăn uống | NV2 | P1 | MOF | Nhịn ăn gián đoạn không hợp với nhóm người này | Chống chỉ định IF | F02 | Chờ duyệt |
| H39 | Ăn uống | NV2 | P2 | MOF | Chị ăn rất ít mà không giảm — vì ba thứ chị không tính vào | Calo ẩn: nước chấm, dầu, đồ uống | F04 | Chờ duyệt |
| H40 | Ăn uống | NV2 | P2 | TOF | Đây là khay ăn của một ngày 1.400 kcal. Nhìn có ít không? | Phá định kiến 'ăn kiêng là đói' | F04 | Chờ duyệt |
| H41 | Ăn uống | NV2 | P1 | TOF | Nấu một lần ăn ba bữa: hộp cơm tôi hay hướng dẫn khách mang đi làm | Meal-prep cho người bận | F04 | Chờ duyệt |
| H42 | Ăn uống | NV2 | P1 | TOF | Đọc nhãn 'ít béo' — và đây là lượng đường trong đó | Dạy đọc nhãn dinh dưỡng | F02 | Chờ duyệt |
| H43 | Sau sinh | NV4 | P1 | MOF | Sau sinh 6 tháng chưa giảm: đừng ăn kiêng, hãy kiểm tra cơ bụng và sàn chậu trước | Xa cách cơ thẳng bụng | F14 | Chờ duyệt |
| H44 | Sau sinh | NV4 | P2 | TOF | Tự kiểm tra xa cách cơ bụng tại nhà trong 20 giây | Test 2 ngón tay — demo trên khách thật | F07 | Chờ duyệt |
| H45 | Sau sinh | NV2 | P1 | MOF | Đang cho con bú vẫn giảm cân được, nhưng không được xuống dưới mức này | Ngưỡng calo an toàn cho mẹ cho bú | F04 | Chờ duyệt |
| H46 | Sau sinh | NV3 | P1 | TOF | Mẹ bỉm tập bụng sai cách sẽ làm bụng to hơn | Vì sao gập bụng làm nặng thêm diastasis | F06 | Chờ duyệt |
| H47 | Sau sinh | NV1 | P1 | MOF | Sau sinh, hormone chưa về chỗ cũ — đây là mốc thời gian thực tế | Kỳ vọng đúng theo từng mốc tháng | F02 | Chờ duyệt |
| H48 | Vận động | NV3 | P1 | TOF | Bạn không cần chạy bộ. Bạn cần đi bộ ở vùng nhịp tim này | Vùng nhịp tim đốt mỡ — demo với máy đo | F07 | Chờ duyệt |
| H49 | Vận động | NV3 | P1 | TOF | 10.000 bước không phải con số y học. Đây mới là con số | Nguồn gốc marketing của 10.000 bước | F02 | Chờ duyệt |
| H50 | Vận động | NV3 | P1 | MOF | Nặng 90kg mà chạy bộ: đầu gối chịu tải gấp nhiều lần | Vì sao bắt đầu bằng đi bộ/đạp xe/bơi | F06 | Chờ duyệt |
| H51 | Vận động | NV3 | P1 | TOF | Ba bài tập cho người mới, làm được ngay cạnh giường | Bài không dụng cụ cho người 80kg+ | F06 | Chờ duyệt |
| H52 | Vận động | NV3 | P1 | MOF | Tập tạ không làm bạn to ra. Nó giữ cho bạn không tăng lại | Giữ khối cơ khi thâm hụt calo | F02 | Chờ duyệt |
| H53 | Vận động | NV3 | P1 | TOF | Bạn tập một tiếng mỗi ngày nhưng ngồi mười tiếng — đây mới là vấn đề | NEAT và hoạt động ngoài buổi tập | F02 | Chờ duyệt |
| H54 | Vận động | NV3 | P1 | TOF | Squat sai ở 90% người tập. Chỉ cần sửa một điểm này | Split-screen sai/đúng | F06 | Chờ duyệt |
| H55 | Vận động | NV3 | P1 | TOF | Không có thời gian? Đây là 12 phút có bằng chứng | Bài tập ngắt quãng cường độ vừa | F06 | Chờ duyệt |
| H56 | Vận động | NV3 | P2 | MOF | Tôi đo sức mạnh của chị trước khi thiết kế bài tập. Đây là lý do | Test thể lực nền — demo tại phòng gym | F07 | Chờ duyệt |
| H57 | Vận động | NV3 | P1 | MOF | Giảm cân xong da chảy xệ: phần nào tập được, phần nào không | Ranh giới nội khoa – ngoại khoa | F12 | Chờ duyệt |
| H58 | Trị liệu vận động | NV4 | P1 | TOF | Đau gối nên nghỉ hay nên tập? Câu trả lời làm nhiều người ngạc nhiên | Vận động có kiểm soát cho thoái hoá khớp | F14 | Chờ duyệt |
| H59 | Trị liệu vận động | NV4 | P1 | MOF | Thừa cân kèm đau lưng: gỡ đau trước, giảm cân sau | Thứ tự can thiệp trong phác đồ đa khoa | F14 | Chờ duyệt |
| H60 | Trị liệu vận động | NV4 | P2 | TOF | Bàn chân bẹt khiến bạn không đi bộ được lâu — test ngay tại chỗ | Test dấu chân ướt, đế chỉnh hình | F07 | Chờ duyệt |
| H61 | Trị liệu vận động | NV4 | P3 | MOF | Sau ba buổi trị liệu, chị ấy đi bộ được 30 phút không đau. Rồi mới bắt đầu giảm cân | Ca thật, có consent | F08 | Chờ duyệt |
| H62 | Trị liệu vận động | NV4 | P1 | TOF | Vai gù, cổ rùa ở người thừa cân — và bài tập gỡ | Tư thế và hô hấp | F14 | Chờ duyệt |
| H63 | Trị liệu vận động | NV4 | P4 | MOF | Máy sóng xung kích làm gì trong cơ thể bạn? Tôi mở máy cho bạn xem | Cơ chế + ai không dùng được | F11 | Chờ duyệt |
| H64 | Trị liệu vận động | NV4 | P1 | TOF | Đau không phải là dấu hiệu bạn tập đúng | Phân biệt mỏi cơ và đau tổn thương | F02 | Chờ duyệt |
| H65 | Ngoại khoa | NV5 | P1 | TOF | Hút mỡ không phải phương pháp giảm cân. Tôi nói lại lần nữa | Hút mỡ là tạo hình đường nét, không phải giảm cân | F13 | Chờ duyệt |
| H66 | Ngoại khoa | NV5 | P4 | MOF | Đây là bốn trường hợp tôi từ chối hút mỡ trong tuần này | Bốn lý do chống chỉ định thực tế | F13 | Chờ duyệt |
| H67 | Ngoại khoa | NV5 | P4 | MOF | Trên ngưỡng BMI này, tôi hoãn phẫu thuật và chuyển bạn sang khoa nội tiết | Quy trình chuyển tuyến nội bộ đa khoa | F12 | Chờ duyệt |
| H68 | Ngoại khoa | NV5 | P1 | MOF | Mỡ có quay lại sau khi hút không? Câu trả lời thật | Tế bào mỡ, phân bố lại mỡ | F13 | Chờ duyệt |
| H69 | Ngoại khoa | NV5 | P4 | BOF | Trước khi ký cam kết phẫu thuật, hãy hỏi bác sĩ năm câu này | Danh sách câu hỏi khách nên hỏi | F13 | Chờ duyệt |
| H70 | Ngoại khoa | NV5 | P4 | BOF | Xét nghiệm tiền phẫu — tôi cho bạn xem toàn bộ danh mục | Minh bạch quy trình an toàn | F15 | Chờ duyệt |
| H71 | Ngoại khoa | NV5 | P1 | MOF | Tạo hình thành bụng khác hút mỡ ở chỗ nào? | So sánh hai kỹ thuật, ai hợp cái nào | F13 | Chờ duyệt |
| H72 | Ngoại khoa | NV5 | P4 | BOF | Biến chứng là có thật. Đây là cách chúng tôi phòng và xử lý | Quy trình an toàn, ekip gây mê, hồi sức | F15 | Chờ duyệt |
| H73 | Ngoại khoa | NV5 | P3 | BOF | Ngày thứ ba sau hút mỡ trông như thế nào — không lọc, không che | Hồi phục theo ngày, có consent | F08 | Chờ duyệt |
| H74 | Minh bạch | Đa nhân vật | P4 | MOF | Hội chẩn ca này: ba chuyên khoa, ba ý kiến khác nhau. Mời bạn xem chúng tôi tranh luận | Hội chẩn thật, có bất đồng | F12 | Chờ duyệt |
| H75 | Minh bạch | NP1 | P4 | MOF | Chi phí một liệu trình — tôi bóc từng khoản cho bạn | Bảng giá minh bạch, không giấu phụ phí | F15 | Chờ duyệt |
| H76 | Minh bạch | NV1 | P4 | TOF | Đây là giấy phép hoạt động và phạm vi chuyên môn của phòng khám | Tuân thủ quy định quảng cáo dịch vụ KCB | F15 | Chờ duyệt |
| H77 | Minh bạch | NV1 | P4 | MOF | Mỗi tháng chúng tôi từ chối bao nhiêu khách? Con số thật | Từ chối là bằng chứng của chuẩn mực | F16 | Chờ duyệt |
| H78 | Minh bạch | NP1 | P4 | TOF | Hồ sơ bệnh án của bạn được lưu thế nào — đi cùng tôi 60 giây | Bảo mật dữ liệu khách hàng | F15 | Chờ duyệt |
| H79 | Minh bạch | NV1 | P4 | MOF | Một ca không đạt mục tiêu — chúng tôi làm gì tiếp theo? | Chính sách khi phác đồ không hiệu quả | F12 | Chờ duyệt |
| H80 | Minh bạch | NP1 | P4 | TOF | Đây là toàn bộ 90 phút đầu tiên của bạn tại phòng khám | POV ngày đầu tiên | F09 | Chờ duyệt |
| H81 | Con người | NV2 | P5 | TOF | Bữa trưa thật của chuyên gia dinh dưỡng — không dàn dựng | Đời thường, tạo gần gũi | F17 | Chờ duyệt |
| H82 | Con người | NV3 | P5 | TOF | Chuyên gia vận động cũng có ngày lười. Đây là cách tôi xử lý | Nhân hoá, giảm khoảng cách | F17 | Chờ duyệt |
| H83 | Con người | NV1 | P5 | TOF | Câu hỏi khiến tôi nhớ nhất trong 10 năm khám béo phì | Kể chuyện, cảm xúc | F17 | Chờ duyệt |
| H84 | Con người | NV5 | P5 | TOF | Ca cuối ngày kết thúc lúc 21 giờ. Vì sao tôi vẫn ở lại | Hậu trường ekip | F17 | Chờ duyệt |
| H85 | Con người | NP1 | P5 | TOF | Khách cũ quay lại mang theo hộp bánh — và một con số mới | Khoảnh khắc thật | F17 | Chờ duyệt |
| H86 | Con người | NV4 | P5 | TOF | Bàn tay của một kỹ thuật viên trị liệu sau 8 năm làm nghề | Cận cảnh, kể bằng hình | F17 | Chờ duyệt |

## Cụm insight — tra cứu nhanh

- **Thất bại lặp lại** — 6 hook (H01–H06)
- **Nguyên nhân nội tiết** — 8 hook (H07–H14)
- **Bệnh lý đi kèm** — 8 hook (H15–H22)
- **Thuốc & lời đồn** — 7 hook (H23–H29)
- **Ăn uống** — 13 hook (H30–H42)
- **Sau sinh** — 5 hook (H43–H47)
- **Vận động** — 10 hook (H48–H57)
- **Trị liệu vận động** — 7 hook (H58–H64)
- **Ngoại khoa** — 9 hook (H65–H73)
- **Minh bạch** — 7 hook (H74–H80)
- **Con người** — 6 hook (H81–H86)

## Quy tắc sinh hook mới

1. Hook mới phải thuộc **một cụm insight có thật** (bình luận, inbox, câu hỏi tại quầy tư vấn, dữ liệu hiệu suất) — không bịa nỗi đau.
2. Hook phải nằm đúng **lãnh địa nội dung của nhân vật**; sai lãnh địa → đổi nhân vật, không đổi lãnh địa.
3. Cấm trong hook: cam kết số cân, "100%", "khỏi hoàn toàn", "không đau", "số 1", "duy nhất", doạ bệnh, hạ thấp cơ sở khác.
4. Hook mới luôn xuất với trạng thái **Chờ duyệt** + gợi ý format + tầng phễu.
5. Mã hook mới đánh tiếp từ **H87**.
6. Mỗi hook phải trả lời được: người xem hiểu thêm điều gì dùng được ngay, kể cả khi không bao giờ đến phòng khám?


===== giambeo-plan.md =====

# KNOWLEDGE — KẾ HOẠCH TRUST CONTENT: PHÒNG KHÁM GIẢM BÉO ĐA KHOA

Thương hiệu: Phòng khám Giảm béo Đa khoa — hệ sinh thái Kangnam (HCI Group)
Kênh: TikTok + Reels (short-form) · Facebook Page/Group
Sản lượng: **90 video/tháng — 270 video/90 ngày** (3 bài/ngày, khung 07:00 · 12:15 · 20:00)
Nguồn: Kế hoạch sản xuất Trust Content v1.0 — 21/08/2026 · Nguyễn Bá Uy

---

## 0. NGUYÊN TẮC TRUNG TÂM

**Không bán kết quả — bán năng lực chẩn đoán.** Mỗi video phải để lại cho người xem một hiểu biết dùng được ngay, kể cả khi họ không bao giờ đến phòng khám.

Bốn quyết định nền tảng của kế hoạch:
1. Năm nhân vật chuyên gia có **lãnh địa nội dung riêng, không chồng lấn** — mỗi người sở hữu một nhóm chủ đề và một tầng phễu.
2. Một **"Studio Trust" (S10)** cố định trong phòng khám để quay gộp 28 clip/ngày — điều kiện kỹ thuật bắt buộc để đạt 90 video/tháng.
3. Lấy **chỉ số đo được** làm đơn vị kể chuyện: InBody, vòng bụng, men gan, góc gập khớp — thay cho tính từ và lời hứa.
4. Biến **minh bạch** thành một trụ cột riêng chiếm 15% sản lượng: ca từ chối, chống chỉ định, bóc tách chi phí, hội chẩn có bất đồng.

Chỉ số thật của Trust Content không phải lượt xem, mà là **tỷ lệ khách đến phòng khám và nói "Tôi xem video của bác sĩ X" ≥ 30% sau 90 ngày**.

---

## 1. NĂM TRỤ CỘT NỘI DUNG

| Mã | Trụ cột | Tỷ trọng | Video/tháng | Nội dung cốt lõi | Điều khách hàng nghĩ sau khi xem |
|---|---|---|---|---|---|
| P1 | GIẢI MÃ CƠ THỂ | 30% | ~27 | Kiến thức chuyên môn biến nỗi hoang mang thành hiểu biết: vì sao bạn béo, cơ thể bạn đang bị gì. | Khách nghĩ: 'Hoá ra không phải mình lười. Có nguyên nhân, và có người đọc được nó.' |
| P2 | BẰNG CHỨNG & CHỈ SỐ | 25% | ~22 | Mọi khẳng định đều gắn với một con số đo được tại phòng khám: InBody, xét nghiệm, vòng đo, ảnh chuẩn hoá. | Khách nghĩ: 'Ở đây người ta nói bằng số, không nói bằng cảm tính.' |
| P3 | HÀNH TRÌNH NGƯỜI THẬT | 20% | ~18 | Bám theo khách hàng thật từ buổi đầu đến mốc 30/60/90 ngày, kể cả những tuần chững lại. | Khách nghĩ: 'Người giống mình đã đi con đường này và họ vẫn ở đó.' |
| P4 | MINH BẠCH | 15% | ~14 | Quy trình, giá, chống chỉ định, ca từ chối, giấy phép, hậu trường — những thứ đối thủ giấu. | Khách nghĩ: 'Họ dám nói cả điều bất lợi cho họ.' |
| P5 | CON NGƯỜI | 10% | ~9 | Ekip ngoài chuyên môn: bữa trưa của bác sĩ, ca trực, những khoảnh khắc đời thường trong phòng khám. | Khách nghĩ: 'Đây là những người thật, mình muốn gặp họ.' |

**Mọi video phải thuộc đúng MỘT trụ cột.** Vì sao MINH BẠCH tới 15%: đây là phần đối thủ không dám làm. Một video "tuần này tôi từ chối bốn ca hút mỡ" tạo nhiều niềm tin hơn mười video khoe kết quả — và nó cũng là hàng rào pháp lý, vì nội dung nói về chống chỉ định không bao giờ vi phạm quy định cấm cam kết kết quả.

---

## 2. HỆ NHÂN VẬT — CHARACTER BIBLE

| Mã | Vai | Định vị | Tầng phễu | Tỷ trọng |
|---|---|---|---|---|
| NV1 | Bác sĩ Nội tiết | Người đọc vị cơ thể bạn | TOF + MOF (dẫn dắt niềm tin toàn hệ) | 35% |
| NV2 | Chuyên gia Dinh dưỡng | Người dạy bạn ăn mà vẫn giảm | TOF (kéo view lớn nhất) + MOF | 25% |
| NV3 | Chuyên gia Vận động | Người thiết kế bài tập vừa sức bạn | TOF (viral) + MOF | 15% |
| NV4 | Chuyên gia Trị liệu Vận động (VLTL–PHCN) | Người gỡ cơn đau để bạn tập được | MOF (chuyển đổi cao, view vừa) | 10% |
| NV5 | Bác sĩ Ngoại khoa — Phẫu thuật tạo hình & hút mỡ | Người nói KHÔNG nhiều hơn nói CÓ | BOF (chuyển đổi giá trị cao) | 15% |

### NV1 — Bác sĩ Nội tiết: "Người đọc vị cơ thể bạn"

| Yếu tố | Chi tiết |
|---|---|
| Lãnh địa nội dung | Nguyên nhân nội tiết – chuyển hoá của béo phì; đọc chỉ số & xét nghiệm; bệnh lý đi kèm (gan nhiễm mỡ, mỡ máu, tiền tiểu đường, tuyến giáp, PCOS); bóc trần thuốc/trà giảm cân; chỉ định phác đồ tổng thể. |
| Tính cách & cách nói | Điềm đạm, nói chậm, không doạ. Luôn mở đầu bằng một con số hoặc một câu hỏi. Không bao giờ hứa kết quả — chỉ mô tả cơ chế. |
| Trang phục / hình ảnh | Blouse trắng, bảng tên, ống nghe treo cổ (không dùng khi ngồi đọc kết quả). Bàn làm việc gọn, 1 màn hình lớn hiển thị kết quả. |
| Đạo cụ bắt buộc | Phiếu xét nghiệm, kết quả InBody in giấy, mô hình mỡ nội tạng, bút highlight, màn hình biểu đồ. |
| Câu cửa miệng | "Mình đọc con số trước, rồi hãy nói chuyện cân nặng." |
| Bối cảnh quay | S1 Phòng khám nội tiết · S2 Phòng InBody · S3 Khu xét nghiệm · S10 Studio Trust |
| Format sở trường | F01, F02, F03, F07, F12, F16 |
| Chỉ số đo riêng | Tỷ lệ xem hết >45%; comment hỏi chuyên môn/1.000 view; số KH nhắc tên khi đến khám |

> **ĐIỀU CẤM:** Không chẩn đoán cá nhân qua bình luận; không nói 'khỏi hoàn toàn'; không nêu tên biệt dược cụ thể; không doạ bệnh.

### NV2 — Chuyên gia Dinh dưỡng: "Người dạy bạn ăn mà vẫn giảm"

| Yếu tố | Chi tiết |
|---|---|
| Lãnh địa nội dung | Phác đồ ăn theo chỉ số; khẩu phần món Việt (phở, bún, cơm văn phòng, trà sữa); đi chợ & nấu theo ngân sách; dinh dưỡng sau sinh, cho con bú; nhịn ăn gián đoạn — ai hợp ai không; đọc nhãn thực phẩm. |
| Tính cách & cách nói | Ấm, thực tế, không cấm đoán. Câu cửa miệng: 'không cấm — chỉ đổi cách'. Luôn cầm đồ ăn thật trên tay. |
| Trang phục / hình ảnh | Áo blouse ngắn hoặc đồng phục màu sáng, tạp dề khi ở bếp demo. Tay không đeo trang sức khi cầm thực phẩm. |
| Đạo cụ bắt buộc | Khay ăn chuẩn, cân điện tử tiểu ly, hộp meal-prep, bảng đổi món, nhãn thực phẩm thật, ly trà sữa (đạo cụ đối chiếu). |
| Câu cửa miệng | "Tôi không cấm chị ăn cơm. Tôi đổi thứ tự chị ăn." |
| Bối cảnh quay | S4 Bếp dinh dưỡng · S2 Phòng InBody · S9 Hành lang (walk & talk) · Ngoại cảnh: siêu thị/chợ |
| Format sở trường | F04, F05, F02, F10, F08, F16 |
| Chỉ số đo riêng | Lượt lưu (save) — chỉ số chính; share; 3s retention |

> **ĐIỀU CẤM:** Không quảng cáo nhãn hàng thực phẩm chưa ký hợp đồng; không gọi thực phẩm là 'thuốc'; không đưa mức calo dưới 1.200 kcal lên nội dung đại chúng.

### NV3 — Chuyên gia Vận động: "Người thiết kế bài tập vừa sức bạn"

| Yếu tố | Chi tiết |
|---|---|
| Lãnh địa nội dung | Thiết kế bài tập theo InBody & thể lực; đi bộ/nhịp tim vùng đốt mỡ; tập cho người 80–100kg không hại khớp; giữ cơ khi giảm cân; sửa lỗi kỹ thuật; bài tập 12 phút tại nhà/văn phòng. |
| Tính cách & cách nói | Năng lượng cao nhưng không hô hào. Luôn demo trực tiếp trên chính khách hàng, không demo trên người mẫu. |
| Trang phục / hình ảnh | Đồng phục thể thao có logo phòng khám, giày tập, đồng hồ đo nhịp tim hiển thị rõ trên khung hình. |
| Đạo cụ bắt buộc | Dây kháng lực, tạ nhẹ, bục step, máy đo nhịp tim, màn hình hiển thị vùng nhịp tim, thảm. |
| Câu cửa miệng | "Bài tập tốt nhất là bài tập bạn làm được đến tuần thứ 12." |
| Bối cảnh quay | S5 Phòng gym trị liệu · S9 Hành lang · S10 Studio Trust |
| Format sở trường | F06, F07, F14, F02, F08 |
| Chỉ số đo riêng | Share & lưu; watch-time; tỷ lệ hoàn thành video >30s |

> **ĐIỀU CẤM:** Không ra bài tập cho người có bệnh lý qua bình luận; không dùng nhạc/khẩu hiệu kiểu 'no pain no gain'.

### NV4 — Chuyên gia Trị liệu Vận động (VLTL–PHCN): "Người gỡ cơn đau để bạn tập được"

| Yếu tố | Chi tiết |
|---|---|
| Lãnh địa nội dung | Đau gối/lưng/vai do thừa cân; bàn chân bẹt, dáng đi; xa cách cơ thẳng bụng & sàn chậu sau sinh; phục hồi sau phẫu thuật hút mỡ; máy trị liệu (sóng xung kích, laser cường độ cao, kéo giãn). |
| Tính cách & cách nói | Tay chạm nhiều hơn miệng nói. Giải thích bằng cách sờ và chỉ trực tiếp trên cơ thể khách hàng. |
| Trang phục / hình ảnh | Đồng phục kỹ thuật viên, găng tay khi cần, thao tác dứt khoát. |
| Đạo cụ bắt buộc | Giường trị liệu, máy sóng xung kích, thước đo góc, con lăn, đế chỉnh hình, mô hình khớp gối/cột sống. |
| Câu cửa miệng | "Đau không phải là dấu hiệu bạn tập đúng." |
| Bối cảnh quay | S6 Phòng vật lý trị liệu · S5 Phòng gym trị liệu |
| Format sở trường | F14, F11, F07, F12, F08 |
| Chỉ số đo riêng | Tỷ lệ inbox/1.000 view (cao nhất hệ); lượt lưu |

> **ĐIỀU CẤM:** Không hứa 'hết đau sau 1 buổi'; không quay cận cảnh vùng nhạy cảm; luôn có người thứ ba trong phòng khi quay khách nữ.

### NV5 — Bác sĩ Ngoại khoa — Phẫu thuật tạo hình & hút mỡ: "Người nói KHÔNG nhiều hơn nói CÓ"

| Yếu tố | Chi tiết |
|---|---|
| Lãnh địa nội dung | Chỉ định & chống chỉ định hút mỡ/tạo hình thành bụng; xét nghiệm tiền phẫu; biến chứng và cách phòng; hồi phục theo ngày; mỡ có quay lại không; khi nào nên nội khoa thay vì ngoại khoa. |
| Tính cách & cách nói | Thẳng, tiết chế, không bán. Uy tín đến từ số ca từ chối chứ không phải số ca đã làm. |
| Trang phục / hình ảnh | Blouse hoặc scrub xanh, bảng tên, khu tiền phẫu phía sau. |
| Đạo cụ bắt buộc | Hồ sơ tiền phẫu, bút vẽ định vị, mô hình lớp mỡ dưới da, ảnh chuẩn hoá (đã có consent), danh mục xét nghiệm. |
| Câu cửa miệng | "Hút mỡ không phải phương pháp giảm cân. Tôi sẽ nói lại điều này mỗi tuần." |
| Bối cảnh quay | S8 Khu tiền phẫu · S1 Phòng tư vấn ngoại khoa · S10 Studio Trust |
| Format sở trường | F13, F02, F15, F12, F03 |
| Chỉ số đo riêng | Lượt xem hết; số lịch hẹn tư vấn ngoại khoa; giá trị hợp đồng trung bình |

> **ĐIỀU CẤM:** Tuyệt đối không quay hình ảnh phẫu thuật gây phản cảm; không so sánh với cơ sở khác; không đăng ảnh trước–sau thiếu consent hoặc thiếu chú thích mốc thời gian.

### Nhân vật phụ & tuyến bổ trợ

| Mã | Nhân vật | Vai trò | Cách dùng |
|---|---|---|---|
| NP1 | Điều dưỡng / Care Manager "Chị Care" | Người đồng hành hằng ngày — nhắc lịch, hỏi thăm, ghi nhật ký cân nặng. | Cầu nối cảm xúc; xuất hiện ở P3 & P5; là người dẫn POV 'Ngày đầu tiên tại phòng khám'. |
| NP2 | Khách hàng thật (5 nguyên mẫu) | Nhân vật chính của trụ cột Hành trình. | Mỗi quý ký hợp đồng đồng hành với 3–5 khách, quay bám 90 ngày. |
| NP3 | Máy móc như một nhân vật | InBody, máy phân tích chuyển hoá, máy sóng xung kích, thiết bị giảm béo công nghệ cao, phòng lab. | Không quay máy như ảnh catalogue: luôn có bàn tay chuyên gia + màn hình kết quả + một câu giải thích cơ chế. |
| NP4 | Người thách thức ("anh chàng hoài nghi") | Một biên tập viên nội bộ đóng vai người không tin, hỏi câu khó. | Dùng trong F03 và F12 để tạo xung đột hợp lý, tránh nội dung một chiều. |

### Năm nguyên mẫu khách hàng (casting cho mọi kịch bản)

| Mã | Nguyên mẫu | Bối cảnh & nỗi đau | Tuyến chuyên gia | Hướng phác đồ |
|---|---|---|---|---|
| A1 | Chị văn phòng 34 tuổi | Béo bụng, gan nhiễm mỡ độ 1, ngồi 9 tiếng/ngày, đã thử 3 phương pháp | NV1 → NV2 → NV3 | Nội khoa + dinh dưỡng |
| A2 | Mẹ bỉm sau sinh 8 tháng | +14kg, xa cách cơ thẳng bụng, yếu sàn chậu, không có thời gian | NV4 → NV2 → NV3 | Trị liệu + dinh dưỡng |
| A3 | Anh quản lý 45 tuổi | Vòng bụng 102cm, mỡ máu, tiền tiểu đường, ngại đến phòng khám | NV1 → NV3 | Nội khoa chuyển hoá |
| A4 | Bạn nữ 26 tuổi | Cân nặng bình thường, mỡ khu trú bụng dưới & đùi, tập mãi không xuống | NV1 → NV5 | Công nghệ / ngoại khoa |
| A5 | Cô 55 tuổi tiền mãn kinh | Tăng 9kg trong 2 năm, đau gối hai bên, huyết áp cao | NV1 → NV4 → NV2 | Nội khoa + phục hồi |

**Quy tắc nhân vật (bắt buộc khi viết kịch bản):**
- Mỗi kịch bản chỉ định sẵn nguyên mẫu khách hàng cần mời (A1–A5).
- Hai nhân vật cùng nói một chủ đề → BẮT BUỘC format F12 Hội chẩn đa khoa, phải có xung đột quan điểm và có kết luận.
- Không để nhân vật phát ngôn ngoài lãnh địa của mình. Sai lãnh địa → đổi nhân vật.
- NP3 (máy móc): không quay như ảnh catalogue — luôn có bàn tay chuyên gia + màn hình kết quả + một câu giải thích cơ chế.

---

## 3. MƯỜI BỐI CẢNH QUAY TRONG PHÒNG KHÁM

Phòng khám đã là một trường quay. Việc cần làm là chuẩn hoá mười góc quay có sẵn.

| Mã | Bối cảnh | Cần có trong khung hình | Nhân vật | Lưu ý quay | Tần suất |
|---|---|---|---|---|---|
| S1 | Phòng khám / tư vấn bác sĩ | Bàn làm việc, màn hình 27" hiển thị kết quả, kệ sách chuyên môn, cây xanh | NV1, NV5 | Đèn key 45° cửa sổ giả + fill mềm; máy đặt ngang tầm mắt | Cao — quay hằng ngày |
| S2 | Phòng đo InBody & chỉ số | Máy InBody, thước đo, huyết áp kế, bảng ghi chỉ số | NV1, NV2, NV3 | Quay 2 góc: toàn cảnh máy + cận màn hình kết quả (che thông tin cá nhân) | Cao |
| S3 | Khu xét nghiệm / lab | Bàn lấy máu, máy phân tích, tủ mẫu | NV1 | Chỉ quay khi không có bệnh nhân khác trong khung; không quay nhãn tên mẫu | Trung bình |
| S4 | Bếp dinh dưỡng / quầy demo | Bàn đảo sáng màu, cân tiểu ly, khay ăn chuẩn, tủ mát trưng bày | NV2 | Đèn từ trên xuống + phản sáng; góc 45° và góc top-down cho khay ăn | Cao |
| S5 | Phòng gym trị liệu | Thảm, dây kháng lực, tạ nhẹ, máy đo nhịp tim, gương | NV3, NV4 | Tránh gương phản chiếu ekip; quay ngược sáng cửa sổ có tản sáng | Cao |
| S6 | Phòng vật lý trị liệu | Giường trị liệu, máy sóng xung kích, laser, thước đo góc | NV4 | Máy quay đặt thấp, cận bàn tay; luôn có người thứ ba khi quay khách nữ | Trung bình |
| S7 | Phòng máy công nghệ giảm béo | Thiết bị giảm mỡ không xâm lấn, màn hình thông số | NV1, NV5, NV4 | Cận thông số máy + phản ứng khách; không quay logo hãng nếu chưa được phép | Trung bình |
| S8 | Khu tiền phẫu / hành lang phòng mổ | Cửa phòng mổ, khu thay đồ, bảng quy trình vô khuẩn | NV5 | Chỉ quay góc an toàn, không quay ca mổ; ưu tiên kể quy trình chứ không kể hình ảnh | Thấp |
| S9 | Lễ tân & hành lang | Quầy lễ tân, biển tên khoa, khu chờ | Tất cả | Dùng cho POV, walk & talk, mở đầu series 'Ngày đầu tiên' | Cao |
| S10 | Studio Trust (góc cố định) | Phông nền một màu + logo mờ, ghế cao, đèn 3 điểm dựng sẵn | Tất cả | Set dựng cố định KHÔNG tháo — cho phép quay batch 20+ clip trong 2 tiếng | Rất cao — xương sống batch |

> **S10 — Studio Trust** là hạng mục đầu tư quan trọng nhất tháng đầu: một góc ~6m², phông nền một màu, ba đèn dựng cố định, **không tháo dỡ**. F02, F10, F16 (gần 40% sản lượng) quay tại đây theo lô. Nếu phải dựng lại đèn mỗi lần quay thì mục tiêu 90 video/tháng không khả thi.


===== giambeo-script-samples.md =====

# KNOWLEDGE — 10 KỊCH BẢN MẪU CHUẨN (Giảm béo đa khoa)

> Đây là **chuẩn đầu ra** của mode SCRIPT. Mọi kịch bản mới phải đạt cùng mức chi tiết: meta đầy đủ, phân cảnh bấm giờ theo giây, chữ trên màn hình, CTA, lưu ý khi quay.

**Template 4 khối bắt buộc:** HOOK (0–3s) → BỐI CẢNH (3–8s) → LÕI (8–40s) → CHỐT & CTA (40–55s).
Kịch bản không chia được thành 4 khối này → trả lại biên kịch.


---

## KB-01 — "Chị ăn rất ít mà không giảm — vì ba thứ chị không tính vào"

| Nhân vật | Format | Bối cảnh | Thời lượng | Trụ cột | Mã hook |
|---|---|---|---|---|---|
| NV2 — Chuyên gia Dinh dưỡng | F04 Bữa ăn thật | S4 Bếp dinh dưỡng | 42 giây | P2 Bằng chứng & chỉ số | H39 |

**Diễn viên: NV2 + khách hàng nguyên mẫu A1 (chị văn phòng 34 tuổi)**

**Đạo cụ: Khay ăn thật của khách chụp lại, cân tiểu ly, chai dầu ăn, bát nước mắm, ly cà phê sữa, bảng ghi calo**

### Phân cảnh theo giây

| Giây | Khối | Nội dung & thoại |
|---|---|---|
| 0–3s | HOOK | Cận cảnh NV2 cầm chai dầu ăn, rót vào thìa. Thoại: "Chị ăn đúng như chị kể. Nhưng ba thứ này chị không tính vào — và nó bằng nguyên một bữa." |
| 3–8s | BỐI CẢNH | Cắt rộng: khách hàng thật ngồi đối diện, trên bàn là ảnh chụp bữa ăn ba ngày của chị. Thoại: "Đây là nhật ký ăn ba ngày của chị Hà." |
| 8–20s | LÕI 1 | Đặt lên cân: 2 thìa dầu xào rau = con số hiện trên màn hình cân. Chữ hiện: "Dầu ăn". NV2: "Rau luộc thì ít, nhưng rau xào thì đây." |
| 20–30s | LÕI 2 | Bát nước chấm + nước mắm chan cơm lên cân. Chữ: "Nước chấm & nước dùng". Rồi ly cà phê sữa buổi sáng. Chữ: "Đồ uống có đường". |
| 30–38s | CHỐT SỐ | Ba con số cộng lại hiện lên màn hình. NV2 nhìn khách: "Chị không ăn nhiều. Chị uống và chấm nhiều." Khách bật cười, gật đầu. |
| 38–42s | CTA | NV2: "Nếu chị đang ăn ít mà không giảm, hãy chụp lại đúng ba thứ này trong ba ngày rồi để dưới bình luận. Tôi đọc." |

- **Chữ trên màn hình:** Chữ lớn theo từng con số; phụ đề toàn bộ; cuối video hiện tên – địa chỉ – số giấy phép phòng khám.
- **CTA:** Bình luận ảnh nhật ký ăn 3 ngày → đội CSKH mời khám InBody + tư vấn dinh dưỡng.
- **LƯU Ý KHI QUAY:** Không nêu con số calo tuyệt đối như một 'chuẩn' — luôn kèm 'với thể trạng của chị'. Khách phải ký consent trước khi quay.


---

## KB-02 — "Đi chợ cùng tôi: 200.000đ cho ba ngày ăn theo phác đồ"

| Nhân vật | Format | Bối cảnh | Thời lượng | Trụ cột | Mã hook |
|---|---|---|---|---|---|
| NV2 — Chuyên gia Dinh dưỡng | F05 Đi chợ cùng chuyên gia | Ngoại cảnh — siêu thị/chợ dân sinh gần phòng khám | 75 giây | P2 Bằng chứng & chỉ số | H36 |

**Diễn viên: NV2 (mặc đồng phục có logo, không blouse ngoài phòng khám)**

**Đạo cụ: Giỏ hàng, tờ tiền 200.000đ cầm trên tay ở cảnh mở, điện thoại tính tiền, hoá đơn cuối**

### Phân cảnh theo giây

| Giây | Khối | Nội dung & thoại |
|---|---|---|
| 0–4s | HOOK | NV2 giơ tờ tiền trước ống kính giữa lối đi siêu thị: "Hai trăm nghìn. Ba ngày ăn. Đi cùng tôi." |
| 4–20s | QUẦY ĐẠM | Chọn ức gà / cá / trứng. Mỗi món dừng 4 giây, nói lượng đạm và giá. Chữ hiện chạy tổng tiền góc phải. |
| 20–40s | QUẦY RAU | Chọn 3 loại rau theo mùa. NV2: "Không cần rau nhập khẩu. Rau chợ đủ chất hơn nhiều người nghĩ." |
| 40–55s | BẪY THƯỜNG GẶP | Dừng ở kệ 'thực phẩm ăn kiêng'. Cầm một gói ngũ cốc 'ít béo', lật nhãn, chỉ vào dòng đường. "Ít béo. Nhưng đây." Đặt lại xuống kệ. |
| 55–68s | TỔNG KẾT | Quầy thanh toán, cận hoá đơn thật. Tổng tiền hiện lên. NV2 chỉ vào giỏ: "Ba ngày. Chín bữa. Đủ đạm." |
| 68–75s | CTA | "Muốn thực đơn ba ngày với đúng giỏ này, comment CHỢ. Tôi gửi bản in." |

- **Chữ trên màn hình:** Bộ đếm tiền chạy ở góc phải suốt video — yếu tố giữ chân mạnh nhất của format này.
- **CTA:** Comment từ khoá → gửi thực đơn PDF → dẫn về đặt lịch tư vấn dinh dưỡng.
- **LƯU Ý KHI QUAY:** Che hoặc tránh logo thương hiệu bán lẻ và nhãn hàng chưa có hợp đồng. Không chê đích danh sản phẩm nào — chỉ đọc nhãn.


---

## KB-03 — "Cân nặng đứng yên nhưng mỡ giảm 4kg — chị ấy suýt bỏ cuộc"

| Nhân vật | Format | Bối cảnh | Thời lượng | Trụ cột | Mã hook |
|---|---|---|---|---|---|
| NV1 — Bác sĩ Nội tiết | F01 Đọc chỉ số | S2 Phòng InBody → S1 Phòng khám | 55 giây | P2 Bằng chứng & chỉ số | H05 |

**Diễn viên: NV1 + khách hàng thật (đã có consent) + màn hình kết quả InBody hai lần đo**

**Đạo cụ: Hai bản in kết quả InBody (ngày 0 và ngày 45), bút highlight, màn hình 27"**

### Phân cảnh theo giây

| Giây | Khối | Nội dung & thoại |
|---|---|---|
| 0–3s | HOOK | Cận NV1 đặt hai tờ kết quả cạnh nhau, gõ bút vào ô cân nặng: "Cùng một con số. Nhưng đây là hai cơ thể khác nhau." |
| 3–10s | BỐI CẢNH | Rộng: khách ngồi cạnh, hơi căng thẳng. Thoại khách: "Em định bỏ vì cân không xuống." |
| 10–30s | LÕI | NV1 highlight ba dòng trên màn hình: khối mỡ giảm, khối cơ tăng, mỡ nội tạng giảm. Giải thích: mỡ và cơ khác nhau về khối lượng riêng nên cân không phản ánh. |
| 30–45s | Ý NGHĨA | NV1 quay sang khách: "Cái cân là dụng cụ tệ nhất để đánh giá việc chị đang làm. Chỉ số này mới là cái quyết định gan và đường huyết của chị." Khách thở phào. |
| 45–55s | CTA | NV1 nói vào ống kính: "Nếu bạn đang giảm cân mà cân không nhúc nhích trong ba tuần, đừng bỏ. Hãy đi đo thành phần cơ thể trước đã." |

- **Chữ trên màn hình:** Che toàn bộ tên, ngày sinh, mã hồ sơ trên bản in. Chỉ để lộ các chỉ số đã được đồng ý công bố.
- **CTA:** Mời đo InBody + tư vấn đọc chỉ số tại phòng khám.
- **LƯU Ý KHI QUAY:** Không nói 'chị sẽ giảm được X kg'. Không kết luận bệnh lý trên video. Cuối video gắn thông tin cơ sở theo Nghị định 342/2025.


---

## KB-04 — "Trà giảm cân làm bạn nhẹ 2kg sau một đêm. Đó là nước."

| Nhân vật | Format | Bối cảnh | Thời lượng | Trụ cột | Mã hook |
|---|---|---|---|---|---|
| NV1 — Bác sĩ Nội tiết | F02 Sự thật hay lời đồn | S10 Studio Trust | 28 giây | P1 Giải mã cơ thể | H23 |

**Diễn viên: NV1 (một mình — clip batch)**

**Đạo cụ: Một ly nước, một hộp trà (đã bóc nhãn/che thương hiệu), bảng viết kính**

### Phân cảnh theo giây

| Giây | Khối | Nội dung & thoại |
|---|---|---|
| 0–3s | HOOK | NV1 nhìn thẳng ống kính: "Uống trà giảm cân, sáng dậy nhẹ hai cân. Tôi tin bạn. Nhưng hai cân đó là nước." |
| 3–10s | CƠ CHẾ | Viết lên bảng kính hai chữ: LỢI TIỂU / NHUẬN TRÀNG. "Hai cơ chế này làm bạn mất nước và mất phân. Không mất mỡ." |
| 10–20s | BẰNG CHỨNG | "Một cân mỡ mất đi cần thâm hụt năng lượng của nhiều ngày. Không có cơ chế nào làm việc đó qua một đêm." |
| 20–25s | RỦI RO | "Dùng dài ngày thì rối loạn điện giải, tổn thương ruột. Tôi đã gặp." |
| 25–28s | CHỐT | "Uống nước lọc rẻ hơn, và trung thực hơn." |

- **Chữ trên màn hình:** Chữ SAI đóng dấu đỏ ở giây thứ 3. Phụ đề toàn bộ.
- **CTA:** Không CTA bán hàng — đây là clip xây niềm tin thuần. CTA duy nhất: "Theo dõi để không bị lừa lần sau."
- **LƯU Ý KHI QUAY:** Che mọi nhãn hiệu sản phẩm. Không nêu tên thương hiệu cụ thể để tránh rủi ro pháp lý.


---

## KB-05 — "Bạn không cần chạy bộ. Bạn cần đi bộ ở vùng nhịp tim này."

| Nhân vật | Format | Bối cảnh | Thời lượng | Trụ cột | Mã hook |
|---|---|---|---|---|---|
| NV3 — Chuyên gia Vận động | F07 Test tại chỗ | S5 Phòng gym trị liệu | 40 giây | P1 Giải mã cơ thể | H48 |

**Diễn viên: NV3 + khách hàng nguyên mẫu A3 (anh 45 tuổi, vòng bụng lớn)**

**Đạo cụ: Máy chạy bộ, đai đo nhịp tim, màn hình hiển thị nhịp tim theo thời gian thực**

### Phân cảnh theo giây

| Giây | Khối | Nội dung & thoại |
|---|---|---|
| 0–3s | HOOK | Cận màn hình nhịp tim đang nhảy số. NV3 ngoài khung: "Con số này quan trọng hơn tốc độ của bạn." |
| 3–12s | SET-UP | Khách đeo đai, bước lên máy chạy đi bộ. NV3 chỉ vào màn hình: "Đây là nhịp tim nghỉ của anh." |
| 12–25s | TEST | Tăng dốc dần. Nhịp tim leo lên. NV3 dừng đúng vùng mục tiêu, khoanh tròn trên màn hình. "Đây. Anh nói chuyện được nhưng không hát được. Đó là vùng của anh." Khách thử nói một câu — hơi đứt quãng. |
| 25–35s | GIẢI THÍCH | "Chạy nhanh hơn không đốt nhiều mỡ hơn với người mới. Nó chỉ làm anh bỏ cuộc sớm hơn và đau gối hơn." |
| 35–40s | CTA | "Ngày mai đi bộ và thử nói một câu dài. Nói được mà hơi hụt là đúng vùng. Lưu lại video này." |

- **Chữ trên màn hình:** Số nhịp tim hiển thị lớn suốt video; khoanh vùng mục tiêu bằng đồ hoạ.
- **CTA:** Lưu video + mời test thể lực tại phòng khám.
- **LƯU Ý KHI QUAY:** Không đưa công thức nhịp tim như chỉ định y khoa cho người có bệnh tim mạch — thêm dòng chữ "Người có bệnh tim mạch cần được bác sĩ đánh giá trước khi tập".


---

## KB-06 — "Squat sai ở 90% người tập. Chỉ cần sửa một điểm này."

| Nhân vật | Format | Bối cảnh | Thời lượng | Trụ cột | Mã hook |
|---|---|---|---|---|---|
| NV3 — Chuyên gia Vận động | F06 Sửa một lỗi tập | S5 Phòng gym trị liệu | 25 giây | P1 Giải mã cơ thể | H54 |

**Diễn viên: NV3 + khách hàng thật (không dùng người mẫu)**

**Đạo cụ: Gương, thảm, một chiếc ghế, dây kháng lực**

### Phân cảnh theo giây

| Giây | Khối | Nội dung & thoại |
|---|---|---|
| 0–3s | HOOK | Split-screen: bên trái động tác sai (gối đổ vào trong), bên phải đúng. Chữ: SAI / ĐÚNG. NV3: "Nhìn hai đầu gối." |
| 3–10s | LỖI | Quay chậm động tác sai, khoanh đỏ vùng gối. "Gối đổ vào trong — đây là lý do gối anh đau sau ba buổi." |
| 10–18s | SỬA | NV3 đặt dây kháng lực quanh đùi, yêu cầu đẩy gối ra ngoài. Khách làm lại. Khoanh xanh. |
| 18–25s | CẢM NHẬN | Hỏi khách: "Anh thấy khác ở đâu?" — "Mông siết hơn, gối nhẹ." NV3 nhìn ống kính: "Đúng rồi. Sửa một điểm thôi." |

- **Chữ trên màn hình:** Split-screen bắt buộc; quay chậm 0.5x ở đoạn lỗi.
- **CTA:** "Gửi video bạn tập vào inbox, tôi soi giúp một lỗi." — đây là cầu chuyển đổi mạnh nhất của NV3.
- **LƯU Ý KHI QUAY:** Khách phải ký consent. Không quay cận vùng nhạy cảm. Có thể quay 6–8 clip cùng dạng trong một buổi batch.


---

## KB-07 — "Sau sinh 6 tháng chưa giảm: kiểm tra cơ bụng trước khi ăn kiêng"

| Nhân vật | Format | Bối cảnh | Thời lượng | Trụ cột | Mã hook |
|---|---|---|---|---|---|
| NV4 — Chuyên gia Trị liệu Vận động | F07 Test tại chỗ + F14 | S6 Phòng vật lý trị liệu | 45 giây | P1 Giải mã cơ thể | H43 + H44 |

**Diễn viên: NV4 (nữ) + khách hàng nguyên mẫu A2 (mẹ bỉm) + điều dưỡng đứng trong phòng**

**Đạo cụ: Giường trị liệu, mô hình cơ bụng, thước đo**

### Phân cảnh theo giây

| Giây | Khối | Nội dung & thoại |
|---|---|---|
| 0–4s | HOOK | Cận bàn tay NV4 đặt hai ngón lên bụng khách (khách mặc áo tập, che kín). "Hai ngón tay. Hai mươi giây. Bạn tự làm được ở nhà." |
| 4–14s | TEST | Hướng dẫn khách nằm gập gối, nhấc đầu. NV4 ấn dọc đường giữa bụng, đếm số ngón lọt vào. Chữ hiện: kết quả. |
| 14–28s | GIẢI THÍCH | Cầm mô hình cơ bụng, tách hai bên ra. "Hai dải cơ này giãn ra khi mang thai. Chưa khép lại thì bụng vẫn nhô, dù mỡ đã giảm." |
| 28–40s | HẬU QUẢ NẾU LÀM SAI | "Đây là lúc gập bụng làm mọi thứ tệ hơn." Demo động tác nên tránh và động tác thay thế (thở cơ hoành, siết cơ ngang bụng). |
| 40–45s | CTA | "Tự test rồi nhắn cho tôi kết quả. Nếu trên hai ngón, đừng tự tập — đi khám." |

- **Chữ trên màn hình:** Đồ hoạ minh hoạ hai dải cơ tách ra; phụ đề toàn bộ.
- **CTA:** Inbox kết quả test → mời khám phục hồi chức năng sau sinh.
- **LƯU Ý KHI QUAY:** BẮT BUỘC có người thứ ba trong phòng khi quay khách nữ. Khung hình chỉ lấy từ ngang hông trở lên, khách mặc áo tập kín. Consent riêng cho nội dung sau sinh.


---

## KB-08 — "Thừa cân kèm đau lưng: gỡ đau trước, giảm cân sau"

| Nhân vật | Format | Bối cảnh | Thời lượng | Trụ cột | Mã hook |
|---|---|---|---|---|---|
| NV4 — Chuyên gia Trị liệu Vận động | F14 Gỡ đau để tập được | S6 Phòng vật lý trị liệu | 40 giây | P1 Giải mã cơ thể | H59 |

**Diễn viên: NV4 + khách hàng nguyên mẫu A5 (cô 55 tuổi, đau gối/lưng)**

**Đạo cụ: Giường trị liệu, mô hình cột sống, máy sóng xung kích, thước đo góc**

### Phân cảnh theo giây

| Giây | Khối | Nội dung & thoại |
|---|---|---|
| 0–3s | HOOK | Khách đứng dậy khỏi ghế một cách khó nhọc. NV4 ngoài khung: "Cô này được bảo là phải đi bộ 10.000 bước. Cô ấy không đi nổi 500 bước." |
| 3–12s | VẤN ĐỀ | NV4 đo góc gập của lưng và gối, đọc số. "Đây là lý do. Không phải cô lười." |
| 12–25s | CAN THIỆP | Thao tác trị liệu tay + máy. Cận bàn tay. NV4 giải thích ngắn gọn cơ chế giảm đau. |
| 25–34s | SAU CAN THIỆP | Đo lại góc. Số cải thiện hiện lên cạnh số cũ. Khách đứng lên dễ hơn. |
| 34–40s | THÔNG ĐIỆP | NV4 nhìn ống kính: "Ở phòng khám này, người đau được gỡ đau trước. Giảm cân là bước sau, không phải bước đầu." |

- **Chữ trên màn hình:** Hai con số góc đo đặt cạnh nhau — bằng chứng thị giác của cải thiện.
- **CTA:** Mời khám phục hồi chức năng; nhấn mạnh mô hình đa khoa phối hợp.
- **LƯU Ý KHI QUAY:** Không hứa 'hết đau sau một buổi'. Ghi rõ đây là kết quả tức thời sau can thiệp, cần liệu trình. Kèm dòng "Kết quả khác nhau tuỳ thể trạng".


---

## KB-09 — "Tuần này tôi từ chối bốn ca hút mỡ"

| Nhân vật | Format | Bối cảnh | Thời lượng | Trụ cột | Mã hook |
|---|---|---|---|---|---|
| NV5 — Bác sĩ Ngoại khoa | F13 Trước khi bạn quyết định | S8 Khu tiền phẫu / S1 Phòng tư vấn | 55 giây | P4 Minh bạch | H66 |

**Diễn viên: NV5 (một mình)**

**Đạo cụ: Bốn tập hồ sơ đặt trên bàn (che toàn bộ thông tin cá nhân), mô hình lớp mỡ dưới da**

### Phân cảnh theo giây

| Giây | Khối | Nội dung & thoại |
|---|---|---|
| 0–4s | HOOK | NV5 đặt bốn tập hồ sơ xuống bàn, từng tập một. "Bốn người. Tuần này. Tôi nói không với cả bốn." |
| 4–16s | CA 1 | "Người thứ nhất: BMI quá cao. Hút mỡ ở mức này rủi ro gây mê tăng lên và kết quả không như bạn tưởng. Tôi chuyển sang khoa nội tiết." |
| 16–28s | CA 2 | "Người thứ hai: đường huyết chưa ổn định. Vết mổ lâu lành. Chờ ba tháng." |
| 28–38s | CA 3 & 4 | "Người thứ ba muốn giảm 20kg bằng hút mỡ — đó không phải việc của kỹ thuật này. Người thứ tư đang cho con bú." |
| 38–48s | THÔNG ĐIỆP | NV5 nhìn thẳng: "Hút mỡ là tạo hình đường nét cho người đã ở gần cân nặng mục tiêu. Nó không phải phương pháp giảm cân. Tôi sẽ nói lại câu này mỗi tuần." |
| 48–55s | CTA | "Nếu ai đó đồng ý mổ cho bạn ngay trong buổi đầu mà không xét nghiệm gì, hãy đi về." |

- **Chữ trên màn hình:** Đánh số 01–04 khi kể từng ca; toàn bộ hồ sơ che kín thông tin.
- **CTA:** Không CTA bán. Đây là clip trụ cột niềm tin — chuyển đổi đến sau, ở clip khác.
- **LƯU Ý KHI QUAY:** Không nêu chi tiết nhận dạng ca bệnh. Không so sánh với cơ sở khác. Duyệt pháp chế bắt buộc.


---

## KB-10 — Hội chẩn đa khoa: "Cùng một khách, ba chuyên khoa, ba hướng khác nhau"

| Nhân vật | Format | Bối cảnh | Thời lượng | Trụ cột | Mã hook |
|---|---|---|---|---|---|
| NV1 + NV2 + NV5 (NV3/NV4 luân phiên) | F12 Hội chẩn đa khoa | S1 Bàn hội chẩn | 85 giây | P4 Minh bạch | H74 + H67 |

**Diễn viên: Ba nhân vật + màn hình chiếu hồ sơ ẩn danh**

**Đạo cụ: Bàn hội chẩn, màn hình lớn hiển thị chỉ số, ba tập hồ sơ**

### Phân cảnh theo giây

| Giây | Khối | Nội dung & thoại |
|---|---|---|
| 0–5s | HOOK | Ba người ngồi quanh bàn, không khí căng. NV1: "Tôi không đồng ý." Cắt đen. Chữ: HỘI CHẨN CA SỐ 12. |
| 5–18s | GIỚI THIỆU CA | NV1 tóm tắt ẩn danh: nữ 29 tuổi, BMI trong ngưỡng, mỡ khu trú bụng dưới, đã tập 8 tháng không cải thiện vùng đó. |
| 18–35s | Ý KIẾN NGOẠI KHOA | NV5: "Đây đúng là chỉ định của tôi — mỡ khu trú, cân nặng ổn định. Nhưng tôi cần loại trừ nguyên nhân nội tiết trước." |
| 35–52s | Ý KIẾN NỘI TIẾT | NV1: "Cortisol của bạn ấy cao. Nếu mổ mà không xử lý nguyên nhân, ba năm nữa quay lại đúng chỗ cũ." |
| 52–68s | Ý KIẾN DINH DƯỠNG | NV2: "Bạn ấy đang ngủ 5 tiếng và ăn tối lúc 10 giờ đêm. Tôi xin ba tháng." |
| 68–80s | CHỐT | NV1 tổng hợp: "Phương án: ba tháng nội khoa và dinh dưỡng trước. Đo lại. Nếu vùng mỡ đó vẫn còn, chuyển ngoại khoa." NV5 gật: "Tôi đồng ý." |

- **Chữ trên màn hình:** "Đa khoa nghĩa là có người dám nói KHÔNG với đồng nghiệp." + thông tin phòng khám.
- **Chữ trên màn hình:** Tên và chức danh từng người hiện khi họ nói; hồ sơ luôn ẩn danh.
- **CTA:** Đặt lịch hội chẩn đa khoa — sản phẩm dịch vụ riêng, giá công khai.
- **LƯU Ý KHI QUAY:** Đây là format khác biệt nhất so với đối thủ. Quay 2 máy: một máy toàn cảnh bàn, một máy cận từng người. Không dàn dựng bất đồng giả — chọn ca có bất đồng thật.
- **________________:**


===== media-production.md =====

# KNOWLEDGE — VẬN HÀNH SẢN XUẤT MEDIA

Áp dụng cho mọi dịch vụ. Đây là **luật vận hành** của Agent: quy trình, lịch batch, call sheet, ekip, KPI, pháp lý.

---

## 1. BA DÒNG SẢN XUẤT SONG SONG

| Dòng | Nhịp | Sản lượng | Đặc điểm |
|---|---|---|---|
| Batch lớn | 2 buổi/tháng, cả ngày 08:00–17:30 | 25–30 clip/buổi | Đủ 5 nhân vật, nhiều bối cảnh, có khách hàng thật, cần consent trước 48h |
| Batch nhanh | Mỗi thứ Tư 12:00–13:30 | 8–10 clip/buổi | Chỉ tại S10 với teleprompter, 1–2 nhân vật, ekip 2 người, chỉ F02/F10/F16 |
| Quay bám (docu) + quay cơ hội | Theo lịch khám / hằng ngày | 10 + 15 clip/tháng | Bám 3 khách hàng 90 ngày; quay cơ hội bằng điện thoại theo SOP |

---

## 2. QUY TRÌNH BẢY BƯỚC — CHU KỲ MỘT TUẦN

| Bước | Thời điểm | Ai tham gia | Việc phải làm | Đầu ra |
|---|---|---|---|---|
| B1 | Thứ Hai — Họp Insight (45 phút) | Content Lead + Quản trị kênh + 1 nhân vật luân phiên + đại diện tổng đài/CSKH | Gom 3 nguồn: bình luận & inbox tuần trước, câu hỏi thật tại quầy tư vấn, dữ liệu hiệu suất video. Chốt 20–25 hook cho tuần. | Danh sách hook đã xếp hạng trong sheet 05_NGAN_HANG_HOOK |
| B2 | Thứ Hai — Duyệt hook (RAG) | Content Lead + Bác sĩ kiểm duyệt | Gắn nhãn Xanh (quay ngay) / Vàng (sửa góc) / Đỏ (loại). Hook Đỏ phải ghi lý do để không lặp lại. | Cột 'Trạng thái duyệt' được cập nhật |
| B3 | Thứ Ba–Tư — Viết kịch bản | Biên kịch | Template 4 khối bắt buộc: HOOK 0–3s / BỐI CẢNH 3–8s / LÕI 8–40s / CTA 40–55s. Mỗi kịch bản ghi rõ bối cảnh, đạo cụ, khách hàng cần mời. | File kịch bản + dòng tương ứng trong 06_LICH_NOI_DUNG |
| B4 | Thứ Tư — Duyệt y khoa (BẮT BUỘC) | Bác sĩ kiểm duyệt + Pháp chế (với nội dung ngoại khoa/thuốc) | Checklist 8 điểm ở sheet 11_CHECKLIST_PHAP_LY. Không có chữ ký duyệt thì không lên lịch quay. | Kịch bản có trạng thái ĐÃ DUYỆT |
| B5 | Trước quay 48 giờ — Tiền kỳ | Điều phối sản xuất | Gửi call sheet cho toàn ekip và nhân vật; mời & xác nhận khách hàng; thu bản đồng ý ghi hình đã ký; chuẩn bị đạo cụ; đặt lịch phòng. | Call sheet + tệp consent đã ký |
| B6 | Ngày quay — Batch | Toàn ekip | Batch lớn 2 buổi/tháng (25–30 clip/buổi) + Batch nhanh mỗi thứ Tư 12:00–13:30 (8–10 clip) + quay cơ hội hằng ngày bằng điện thoại theo SOP. | Footage đã sao lưu + bảng kiểm clip đã quay |
| B7 | Hậu kỳ & Đăng tải | Editor → Content Lead duyệt vòng 2 → Quản trị kênh | Dựng trong 48h; phụ đề 100%; chèn thông tin bắt buộc (tên, địa chỉ, số giấy phép) ở cuối video hoặc mô tả; đăng đúng khung giờ; trực bình luận 60 phút đầu. | Video đã đăng + số liệu ghi vào 10_KPI_THEO_DOI |

**Cửa chặn cứng:** không có chữ ký của bác sĩ kiểm duyệt (B4) thì không lên lịch quay. Không có consent thì không bấm máy.

---

## 3. LỊCH BATCH QUAY MỘT QUÝ

| Buổi quay | Loại | Thời gian | Bối cảnh sử dụng | Nhân vật | Clip mục tiêu | Chuẩn bị |
|---|---|---|---|---|---|---|
| Batch lớn 1A | Batch lớn | Tháng 1 (9/2026) — ngày 05, 08:00–17:30 | S10 → S1 → S4 → S5 → S6 → S8 | Cả 5 nhân vật | 28 | Chốt kịch bản trước 48h; mời 3 khách hàng thật; thu consent; dựng sẵn 4 khay ăn từ 07:00 |
| Batch lớn 1B | Batch lớn | Tháng 1 (9/2026) — ngày 20, 08:00–17:30 | S10 → S2 → S4 → S5 → S7 | Cả 5 nhân vật | 28 | Ưu tiên F01/F07 cần khách hàng thật; đặt lịch phòng InBody trống cả buổi sáng |
| Batch nhanh 1.1 | Batch nhanh | Tháng 1 (9/2026) — thứ Tư tuần 1, 12:00–13:30 | S10 (set cố định, không tháo) | 1–2 nhân vật luân phiên | 9 | Chỉ quay F02/F10/F16 bằng teleprompter; không đổi set; ekip 2 người |
| Batch nhanh 1.2 | Batch nhanh | Tháng 1 (9/2026) — thứ Tư tuần 2, 12:00–13:30 | S10 (set cố định, không tháo) | 1–2 nhân vật luân phiên | 9 | Chỉ quay F02/F10/F16 bằng teleprompter; không đổi set; ekip 2 người |
| Batch nhanh 1.3 | Batch nhanh | Tháng 1 (9/2026) — thứ Tư tuần 3, 12:00–13:30 | S10 (set cố định, không tháo) | 1–2 nhân vật luân phiên | 9 | Chỉ quay F02/F10/F16 bằng teleprompter; không đổi set; ekip 2 người |
| Batch nhanh 1.4 | Batch nhanh | Tháng 1 (9/2026) — thứ Tư tuần 4, 12:00–13:30 | S10 (set cố định, không tháo) | 1–2 nhân vật luân phiên | 9 | Chỉ quay F02/F10/F16 bằng teleprompter; không đổi set; ekip 2 người |
| Docu 1 | Quay bám | Tháng 1 (9/2026) — theo lịch khám của khách | Đa bối cảnh theo lịch khám khách | Nhân vật phụ trách ca + NP1 | 10 | Bám 3 khách hàng song song; quay đúng buổi tái khám để có chỉ số mới |
| Cơ hội 1 | Quay cơ hội | Tháng 1 (9/2026) — hằng ngày | Bất kỳ | Ai đang có mặt | 15 | Quay bằng điện thoại theo SOP; Điều phối kiểm tra chất lượng cuối ngày |

Tháng 2 và tháng 3 **lặp lại đúng cấu trúc trên** (đổi tiền tố 2A/2B/2.x và 3A/3B/3.x). Tổng ≥ 270 clip/quý — phần dư là biên an toàn cho clip hỏng.

---

## 4. CALL SHEET MẪU — MỘT NGÀY BATCH LỚN (28 CLIP)

| Khung giờ | Nhân vật / bộ phận | Nội dung | Phụ trách |
|---|---|---|---|
| 07:30–08:00 | Ekip | Dựng đèn tại S10, kiểm tra âm thanh, test khung hình | DOP + Trợ quay |
| 08:00–08:15 | Toàn bộ | Họp nhanh: chạy qua danh sách 28 clip trong ngày, ai quay lúc nào | Điều phối |
| 08:15–10:00 | NV1 | Batch F02 + F16: 10 clip talking head tại S10 (teleprompter) | DOP |
| 10:00–10:15 | — | Đổi set: S10 → S1 (chuyển đèn, bật màn hình kết quả) | Trợ quay |
| 10:15–11:15 | NV1 + KH A1 | F01 Đọc chỉ số — 2 clip, khách hàng thật, ký consent trước | DOP + Điều phối |
| 11:15–12:00 | NV2 | F04 Bữa ăn thật tại S4 — 4 clip (dựng sẵn 4 khay từ 07:00) | DOP |
| 12:00–12:45 | — | Nghỉ trưa. Trợ quay sao lưu thẻ nhớ đợt 1 | Trợ quay |
| 12:45–13:45 | NV3 + KH A3 | F06 + F07 tại S5 — 5 clip, cần 1 khách hàng nam | DOP |
| 13:45–14:45 | NV4 + KH A2 | F07 + F14 tại S6 — 3 clip, BẮT BUỘC có điều dưỡng trong phòng | DOP + Điều dưỡng |
| 14:45–15:00 | — | Đổi set: S6 → S8/S1 cho ngoại khoa | Trợ quay |
| 15:00–16:00 | NV5 | F13 + F15 — 4 clip, hồ sơ đã che thông tin | DOP |
| 16:00–17:00 | NV1 + NV2 + NV5 | F12 Hội chẩn đa khoa — 1 số, quay 2 máy | DOP + Trợ quay |
| 17:00–17:30 | Toàn bộ | Quay F17 đời thường + hậu trường bằng điện thoại; bảng kiểm clip; sao lưu cuối ngày | Điều phối |

**Sáu nguyên tắc batch (không thoả hiệp):**

1. **Không tháo set S10** — Studio Trust dựng cố định — đây là điều kiện tiên quyết để đạt 90 video/tháng
2. **Gom theo bối cảnh, không gom theo nhân vật** — Đổi set tốn 15 phút; đổi nhân vật tốn 2 phút
3. **Trang phục cố định theo nhân vật** — Cùng blouse/đồng phục cả ngày để clip có thể phát rải trong 30 ngày mà không lộ quay gộp
4. **Mỗi clip quay tối đa 3 lần** — Quá 3 lần thì chuyển sang clip khác, quay lại cuối buổi — tránh tụt năng lượng
5. **Consent trước, máy chạy sau** — Không có bản ký thì không bấm máy, không có ngoại lệ
6. **Sao lưu trong ngày** — Không để footage qua đêm trên thẻ nhớ

---

## 5. EKIP & PHÂN VAI

| Vị trí | SL | Hình thức | Trách nhiệm chính | R/A/C |
|---|---|---|---|---|
| Content Lead / Chủ nhiệm nội dung | 1 | Toàn thời gian | Chốt hook, duyệt kịch bản vòng 1, chủ trì họp thứ Hai, chịu trách nhiệm KPI toàn kênh | R |
| Biên kịch – Copywriter | 1 | Toàn thời gian | Viết kịch bản theo template 4 khối, viết caption & chữ trên màn hình, quản lý ngân hàng hook | R |
| Quay phim chính (DOP) | 1 | Toàn thời gian | Set ánh sáng Studio Trust, quay batch lớn, chuẩn hoá khung hình cho từng bối cảnh | R |
| Trợ quay – Ánh sáng – Âm thanh | 1 | Toàn thời gian | Đèn, mic, hậu cần thiết bị, quản lý thẻ nhớ & sao lưu ngay trong ngày quay | R |
| Dựng phim (Editor) | 2 | Toàn thời gian | Mỗi editor 35–50 clip/tháng; một người chuyên short-form, một người chuyên docu-series | R |
| Điều phối sản xuất (Producer) | 1 | Toàn thời gian | Call sheet, lịch bác sĩ, mời & chuẩn bị khách hàng, thu consent, đạo cụ, dọn bối cảnh | A |
| Quản trị kênh & Cộng đồng | 1 | Toàn thời gian | Đăng bài đúng khung giờ, trả lời bình luận trong 30 phút, gom câu hỏi cho format F10, báo cáo tuần | R |
| Bác sĩ kiểm duyệt y khoa | 1 | Bán thời gian (4h/tuần) | Ký duyệt kịch bản theo checklist 8 điểm; quyền phủ quyết mọi nội dung chuyên môn | A |
| Pháp chế / Tuân thủ | 1 | Theo yêu cầu | Rà nội dung quảng cáo theo Nghị định 342/2025 và Luật Quảng cáo sửa đổi; duyệt hợp đồng KOL & mẫu consent | C |
| 5 nhân vật chuyên gia | 5 | 2–4 giờ/tháng mỗi người | Có mặt đúng lịch batch; không tự đăng nội dung chuyên môn ngoài hệ thống duyệt | R |

R = Thực hiện · A = Chịu trách nhiệm cuối · C = Được hỏi ý kiến

### Thiết bị

| Hạng mục | Cấu hình đề xuất | Vì sao cần |
|---|---|---|
| Máy quay chính | 2 thân máy mirrorless (full-frame) + ống 24–70mm và 35mm khẩu lớn | Quay Studio Trust và các bối cảnh chính, 2 góc song song |
| Máy quay phụ | 2 điện thoại flagship + gimbal nhỏ | Quay cơ hội, POV, F17 đời thường, hậu trường |
| Âm thanh | 2 bộ micro không dây (2 TX + 1 RX) + 1 mic shotgun dự phòng | Bắt buộc — chất lượng tiếng quyết định watch-time hơn hình |
| Ánh sáng | 2 đèn LED bi-color 100W + softbox, 1 đèn tóc, 1 tấm hắt sáng | Dựng cố định tại S10; bộ di động cho S1–S6 |
| Chân máy & thiết bị phụ | 2 tripod, 1 gimbal, 1 slider ngắn, teleprompter gắn điện thoại | Teleprompter dùng cho F02/F16 để tăng tốc độ batch |
| Hiển thị & minh hoạ | 1 màn hình 27" tại S1, 1 màn hình di động, bảng viết kính | Đưa chỉ số lên hình — trục của trụ cột Bằng chứng |
| Đạo cụ chuyên môn | Mô hình mỡ nội tạng, mô hình khớp gối, cân tiểu ly, khay ăn chuẩn, dây kháng lực, thước dây | Tăng độ tin cậy thị giác, giảm phụ thuộc lời nói |
| Lưu trữ | 2 ổ SSD 2TB + NAS lưu trữ trung tâm, quy tắc sao lưu 3-2-1 | Sao lưu ngay trong ngày quay, không để qua đêm trên thẻ |
| Phần mềm | Bộ dựng phim, công cụ phụ đề tự động tiếng Việt, kho nhạc bản quyền, công cụ quản lý lịch nội dung | Phụ đề bắt buộc 100% video — phần lớn người xem tắt tiếng |

---

## 6. KPI BA TẦNG

| Tầng | Chỉ số | Định nghĩa | Mục tiêu | Ai chịu trách nhiệm |
|---|---|---|---|---|
| Tầng | Chỉ số | Định nghĩa | Mục tiêu | Ai chịu trách nhiệm |
| Tầng 1 — TIẾP CẬN | Lượt xem | Tổng view của toàn bộ nội dung trong tháng | ≥ 3.000.000 view/tháng từ tháng thứ 2 | Quản trị kênh |
| Tầng 1 — TIẾP CẬN | Giữ chân 3 giây | % người xem qua mốc 3 giây | ≥ 45% | Biên kịch (chất lượng hook) |
| Tầng 1 — TIẾP CẬN | Tỷ lệ xem hết | % xem hết video | ≥ 25% với clip dưới 30s | Editor + Biên kịch |
| Tầng 2 — NIỀM TIN | Bình luận chuyên môn/1.000 view | Số câu hỏi thật về chuyên môn — chỉ số trust cốt lõi | ≥ 3 | Content Lead |
| Tầng 2 — NIỀM TIN | Lượt lưu (save) | Nội dung đủ giá trị để cất đi xem lại | ≥ 1,5% trên view | Content Lead |
| Tầng 2 — NIỀM TIN | Tăng người theo dõi | Follower mới/tháng | ≥ 15.000/tháng từ tháng thứ 2 | Quản trị kênh |
| Tầng 2 — NIỀM TIN | Tỷ lệ bình luận tích cực | % bình luận không tiêu cực/không nghi ngờ | ≥ 85% | Quản trị kênh |
| Tầng 3 — CHUYỂN ĐỔI | Số inbox/liên hệ | Lead thô từ inbox, bình luận để lại số, form | ≥ 900/tháng | Quản trị kênh + CSKH |
| Tầng 3 — CHUYỂN ĐỔI | Lịch hẹn đặt được | Số khách đặt lịch khám | ≥ 25% trên lead thô | CSKH |
| Tầng 3 — CHUYỂN ĐỔI | Tỷ lệ đến khám | Số khách thực sự đến / số lịch hẹn | ≥ 55% | CSKH |
| Tầng 3 — CHUYỂN ĐỔI | Chi phí trên lead (CPL) | Tổng chi phí sản xuất + media / lead thô | Giảm 20% sau 90 ngày | Content Lead |

**Chỉ số Bắc Đẩu:** tỷ lệ khách đến phòng khám chủ động nhắc tên nhân vật ("tôi xem video của bác sĩ X") ≥ 30% sau 90 ngày.

Nhịp tối ưu: hằng ngày theo dõi 3s retention → hằng tuần rà format thắng/thua → hằng tháng cắt 3 format kém nhất, nhân đôi 3 format thắng.

---

## 7. CHECKLIST PHÁP LÝ — 12 ĐIỂM BẮT BUỘC

Chỉ được đăng khi **mọi điểm BẮT BUỘC ở trạng thái Đạt** và có chữ ký bác sĩ kiểm duyệt.

| Mã | Điểm kiểm tra | Yêu cầu cụ thể | Căn cứ | Ai duyệt |
|---|---|---|---|---|
| L01 | Thông tin bắt buộc trong nội dung quảng cáo | Mọi video/bài mang tính quảng cáo dịch vụ khám chữa bệnh phải thể hiện: tên cơ sở, địa chỉ, số giấy phép hoạt động, và phạm vi chuyên môn đã được phê duyệt. | Nghị định 342/2025/NĐ-CP | Content Lead + Pháp chế |
| L02 | Không vượt phạm vi chuyên môn | Không nói về dịch vụ, kỹ thuật hoặc chỉ định nằm ngoài phạm vi hoạt động chuyên môn đã được cơ quan y tế phê duyệt cho phòng khám. | Nghị định 342/2025/NĐ-CP | Bác sĩ kiểm duyệt |
| L03 | Cấm cam kết kết quả | Loại bỏ mọi câu như 'giảm X kg trong Y ngày', 'cam kết 100%', 'khỏi hoàn toàn', 'không giảm hoàn tiền' trong nội dung chuyên môn. Thay bằng mô tả cơ chế và khoảng kết quả kèm điều kiện. | Luật Quảng cáo & quy định QC dịch vụ KCB | Bác sĩ kiểm duyệt |
| L04 | Không tuyên bố 'nhất – số 1 – duy nhất' | Không dùng từ ngữ so sánh tuyệt đối hoặc so sánh trực tiếp với cơ sở khác nếu không có tài liệu hợp pháp chứng minh. | Luật Quảng cáo | Pháp chế |
| L05 | Bản đồng ý ghi hình (consent) cho mọi khách hàng | Mẫu consent riêng cho: quay hình, sử dụng chỉ số sức khoẻ, ảnh trước–sau, thời hạn sử dụng và quyền rút lại. Lưu bản ký cùng hồ sơ bệnh án. | Quy định bảo vệ dữ liệu cá nhân + Luật Quảng cáo | Điều phối sản xuất |
| L06 | Thư cảm ơn & lời chứng thực của người bệnh | Không dùng thư cảm ơn/lời chứng thực của người bệnh làm nội dung quảng cáo dịch vụ khám chữa bệnh. Nếu muốn kể chuyện khách hàng, hãy trình bày dưới dạng ghi nhận quá trình điều trị có chỉ số, không dưới dạng lời khen dịch vụ. Rà cùng pháp chế trước khi đăng. | Quy định QC dịch vụ KCB | Pháp chế |
| L07 | Ảnh & video trước – sau | Cùng góc máy, cùng ánh sáng, cùng trang phục, không chỉnh sửa hình thể. Ghi rõ mốc thời gian và phương pháp đã dùng. Kèm dòng 'Kết quả khác nhau tuỳ thể trạng từng người'. | Nguyên tắc quảng cáo trung thực | Content Lead |
| L08 | Nghĩa vụ của người chuyển tải sản phẩm quảng cáo (KOL/KOC) | Từ 01/01/2026: người có ảnh hưởng phải công bố rõ nội dung có tài trợ (#Quảng cáo/Sponsored), phải thực sự sử dụng hoặc hiểu rõ dịch vụ, phải kiểm chứng thông tin, và chịu trách nhiệm pháp lý. Mọi hợp tác phải có hợp đồng bằng văn bản kèm hồ sơ chứng minh công bố. | Luật Quảng cáo sửa đổi, hiệu lực 01/01/2026 | Pháp chế + Content Lead |
| L09 | Không chẩn đoán cá nhân trên mạng xã hội | Bình luận hỏi bệnh cá nhân được trả lời bằng câu mẫu: giải thích nguyên tắc chung + mời đến khám. Tuyệt đối không kết luận bệnh hoặc kê đơn qua bình luận/inbox. | Y đức & Luật Khám bệnh, chữa bệnh | Quản trị kênh |
| L10 | Bảo mật hình ảnh trong bối cảnh | Không để lọt vào khung hình: tên/hồ sơ bệnh nhân khác, màn hình chứa dữ liệu cá nhân, mẫu xét nghiệm có nhãn tên. Kiểm tra khung hình trước mỗi cú máy. | Bảo vệ dữ liệu cá nhân | Quay phim chính |
| L11 | Ngôn ngữ về thuốc | Không nêu tên biệt dược, không hướng dẫn liều dùng, không so sánh hiệu quả thuốc trên nội dung đại chúng. Chỉ nói ở mức nhóm thuốc và nguyên tắc 'phải do bác sĩ chỉ định'. | Quy định quảng cáo thuốc | Bác sĩ kiểm duyệt |
| L12 | Lưu trữ hồ sơ tuân thủ | Mỗi video lưu: kịch bản đã duyệt, chữ ký bác sĩ kiểm duyệt, consent khách hàng, bản đăng cuối. Lưu tối thiểu theo thời hạn pháp luật yêu cầu. | Quản trị rủi ro | Điều phối sản xuất |

### Mẫu câu trả lời bình luận hỏi bệnh cá nhân

| Tình huống | Câu trả lời chuẩn | Tuyệt đối không nói |
|---|---|---|
| Hỏi "em bị thế này có sao không bác sĩ" | "Với triệu chứng bạn mô tả thì có vài nguyên nhân khác nhau, và không thể kết luận nếu chưa có chỉ số. Bạn để lại số điện thoại hoặc nhắn tin cho phòng khám, bên mình đặt lịch để bác sĩ đánh giá trực tiếp nhé." | Không đoán bệnh; không nói "bạn bị X"; không nói "không sao đâu" |
| Hỏi "uống thuốc gì để giảm cân" | "Nhóm thuốc hỗ trợ giảm cân có tồn tại và được cấp phép, nhưng bắt buộc phải do bác sĩ chỉ định sau khi có kết quả xét nghiệm. Mình không tư vấn thuốc qua bình luận được." | Không nêu tên biệt dược; không nói liều; không gợi ý mua ở đâu |
| Hỏi "giá bao nhiêu" | "Chi phí phụ thuộc vào phác đồ sau khi khám. Bạn nhắn tin để bên mình gửi khung giá từng gói và giải thích từng khoản nhé." | Không hứa giá cố định trên bình luận công khai |
| Hỏi "cam kết giảm bao nhiêu kg" | "Phòng khám không cam kết số cân. Bên mình cam kết quy trình: khám, xét nghiệm, phác đồ cá nhân hoá và theo dõi chỉ số định kỳ." | Không đưa bất kỳ con số cam kết nào |
| Bình luận tiêu cực / nghi ngờ | "Cảm ơn bạn đã đặt câu hỏi. Đây là số giấy phép hoạt động và phạm vi chuyên môn của phòng khám. Nếu bạn muốn, bên mình mời bạn đến xem quy trình trực tiếp." | Không tranh cãi; không xoá bình luận trừ khi vi phạm; không công kích cá nhân |

### Ba quy tắc vàng cho nhân vật khi lên hình

1. **Nói cơ chế, không nói kết quả.** Mô tả cơ thể hoạt động thế nào; không hứa con số.
2. **Mọi khẳng định phải có chỗ dựa** — một chỉ số, một xét nghiệm, một hướng dẫn chuyên môn. Không có chỗ dựa thì không nói.
3. **Dám nói điều bất lợi cho mình.** Ca từ chối, chống chỉ định, giới hạn của phương pháp — đây là nguồn niềm tin lớn nhất và an toàn pháp lý nhất.

---

## 8. LỘ TRÌNH 90 NGÀY

| Giai đoạn | Trọng tâm | Việc phải làm | Đầu ra cuối giai đoạn |
|---|---|---|---|
| Tháng 1 (Ngày 1–30) | NỀN MÓNG | Dựng cố định Studio Trust (S10); chốt hồ sơ 5 nhân vật; quay 2 batch lớn + 4 batch nhanh; hoàn thiện mẫu consent & quy trình duyệt y khoa; xuất bản 90 video; mở chuyên mục F10 để gom câu hỏi. | 90 video · thư viện nội dung nền · quy trình chạy trơn · KPI theo dõi Tầng 1 |
| Tháng 2 (Ngày 31–60) | MỞ RỘNG & THỬ NGHIỆM | Khởi động docu-series F08 với 3 khách hàng thật; bắt đầu F12 Hội chẩn đa khoa 1 số/tuần; livestream tư vấn 1 buổi/tuần; A/B test 3 kiểu hook trên cùng nội dung; mở tài khoản riêng cho nhân vật mạnh nhất. | 90 video + 4 livestream · dữ liệu A/B · Tầng 2 đạt chuẩn |
| Tháng 3 (Ngày 61–90) | TỐI ƯU & NHÂN BẢN | Cắt 3 format kém nhất, nhân đôi sản lượng 3 format thắng; chuyển nội dung thắng thành creative quảng cáo có trả phí; xây thư viện tái sử dụng (cắt lại clip cũ theo hook mới); bàn giao SOP cho ekip vận hành độc lập. | 90–100 video · CPL giảm 20% · SOP hoàn chỉnh · tỷ lệ nhắc tên nhân vật ≥30% |

### Bảy việc cần chốt trong tuần đầu tiên

1. Khảo sát và chốt vị trí S10 Studio Trust; duyệt ngân sách dựng đèn và phông nền.
2. Chốt hồ sơ 5 nhân vật chuyên gia và lịch có mặt 2–4 giờ/tháng mỗi người.
3. Chỉ định bác sĩ kiểm duyệt và ban hành quy trình ký duyệt kịch bản.
4. Tuyển đủ ekip lõi: điều phối sản xuất, biên kịch, DOP, hai editor.
5. Ban hành mẫu consent (quay hình · chỉ số sức khoẻ · ảnh trước–sau · thời hạn sử dụng).
6. Chọn ba khách hàng đầu tiên cho docu-series 90 ngày, thuộc ba nguyên mẫu khác nhau.
7. Chốt lịch batch lớn 1A/1B và bốn batch nhanh của tháng đầu.

---

## 9. QUY ƯỚC DỮ LIỆU

- TOF / MOF / BOF = Đầu phễu (nhận biết) / Giữa phễu (cân nhắc) / Cuối phễu (quyết định).
- Ô cần ban lãnh đạo xác nhận → đánh dấu `⚠ Cần xác minh`.
- Không bịa số liệu để lấp bảng: thiếu ngân sách/KPI/chỉ số thật → ghi gợi ý + `⚠ Cần xác minh`.

