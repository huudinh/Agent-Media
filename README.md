# 🎬 Media Content Producer

> Version 1.1 · **Khung sản xuất nội dung short-form** cho team Media của hệ sinh thái **HCI Group**.

Đóng vai **Chủ nhiệm sản xuất nội dung**: từ insight → hook → kịch bản bấm giờ theo giây → call sheet buổi quay → lịch xuất bản. Đầu ra cầm ra hiện trường quay được ngay, không cần viết lại.

**Khác gì Agent-PBP?** PBP là *Planner* — chiến lược, big idea, content bank, KPI. Agent này là *Producer* — kịch bản, bối cảnh, đạo cụ, lịch quay. Dùng song song: PBP chốt hướng, Producer biến hướng thành clip.

---

## 📘 Hướng dẫn sử dụng

> ### → **[Mở trang hướng dẫn](https://claude.ai/artifact/FTJqHkmCtbR2LWCVRDH1nc)**
>
> Nút Copy sẵn cho bộ não và 6 file tri thức · 13 prompt theo 4 mode + 2 câu lệnh điều khiển sổ quyết định · smoke test 8 câu · ba cơ chế giữ quyền chọn ở phía người.
>
> Trang sinh thẳng từ nội dung repo bằng `python tools/trang-huong-dan.py`, nên **nút Copy luôn khớp file nguồn**.

**Người mới bắt đầu từ trang đó, không phải từ đây.** Repo này là phần file để cài vào Project/GPT/Gem — trang hướng dẫn nói *khi nào dùng cái gì*.

## Đây là một khung, không phải người ra quyết định

**Agent soạn và trình. Con người chọn và ký.** Đây là điều khoản cao nhất của hệ thống ([`SYSTEM-PROMPT.md`](SYSTEM-PROMPT.md) §19) — nó thắng mọi quy tắc khác khi có xung đột.

### Ranh giới

| Việc | Agent | Con người |
|---|---|---|
| Soạn hook · kịch bản · call sheet · lịch | **Làm** | Duyệt |
| Tri thức mâu thuẫn nhau | Nêu ra + trình 2–3 phương án | **Quyết** |
| Nội dung y khoa | Soạn + tự gắn cảnh báo | **Bác sĩ kiểm duyệt ký** |
| Số liệu · giá · ca bệnh · thông tin bác sĩ | Để trống + `⚠ Cần xác minh` | **Cung cấp** |
| Bản đồng ý ghi hình (consent) | Nhắc, không suy đoán | **Thu & ký** |
| Sửa file Tri thức | Trình bản vá đề xuất | **Thực hiện** |
| Bấm máy · đăng bài | Không bao giờ | **Quyết** |

### Ba cơ chế giữ quyền chọn ở phía người

**1. Nhãn nguồn** — mọi khẳng định của Agent đều mang một trong ba nhãn, để bạn biết ngay cái gì là của tài liệu và cái gì là Agent nghĩ ra:

| Nhãn | Nghĩa |
|---|---|
| `[TRI THỨC]` | Có trong file, trích được, nêu được mã |
| `[ĐỀ XUẤT]` | Agent sinh ra, **chưa ai duyệt** |
| `[⚠ CẦN XÁC MINH]` | Cần số liệu hoặc chữ ký từ người thật |

**2. Sổ quyết định** — [`knowledge/decisions.md`](knowledge/decisions.md) ghi mọi chỗ Tri thức chưa nói rõ, kèm các phương án và hệ quả. Agent đọc file này trước mọi tác vụ.

- Điểm **đã chốt 🟢** → Agent theo đúng, ghi mã `DP`.
- Điểm **chưa chốt 🔴** → Agent dùng *Mặc định khung* và gắn nhãn `[MẶC ĐỊNH KHUNG · DPxx · chưa ai chốt]`.
- Xung đột **chưa có mã DP** → Agent **dừng lại và hỏi**, không tự chọn.

**3. Khối lựa chọn** — mọi deliverable kết thúc bằng bảng này, để bạn thấy đúng những đòn bẩy đang có và cách bật chúng:

```
### ⚖ Điểm cần bạn quyết
| # | Việc | Tôi đang dùng | Vì sao | Phương án khác | Đổi bằng cách gõ |
```

### Hai câu lệnh điều khiển

```
TRẠNG THÁI QUYẾT ĐỊNH
```
→ in bảng 10 điểm quyết định kèm việc đang bị ảnh hưởng.

```
DP04 = B
```
→ đổi một lựa chọn. Agent áp dụng ngay, **chỉ in lại phần bị ảnh hưởng**. Thêm lý do nếu muốn: `DP04 = B vì quý này không thêm format mới`.
Đổi xong nhớ cập nhật [`decisions.md`](knowledge/decisions.md) để lần sau khỏi gõ lại.

> **Bốn việc Agent không bao giờ tự quyết — không có mặc định, không có ngoại lệ:** nội dung y khoa chưa ký duyệt · số liệu/giá/ca bệnh · consent · sửa file Tri thức.

---

## Kiến trúc 3 tầng

- **Bộ não (trung tính):** [`SYSTEM-PROMPT.md`](SYSTEM-PROMPT.md) — dán vào ô Chỉ dẫn/Instructions. Dùng chung mọi dịch vụ.
- **Kiến thức dịch vụ:** `knowledge/<dịch-vụ>-plan.md` + `-format-bank.md` + `-hook-bank.md` + `-script-samples.md`.
- **Luật vận hành (dùng chung):** `knowledge/media-production.md`.
- **Quyền quyết định (dùng chung):** [`knowledge/decisions.md`](knowledge/decisions.md) — nơi con người ký. Agent đọc, không được sửa.

Brain biết *cách sản xuất*; file dịch vụ cấp *nhân vật + format + hook + kịch bản mẫu*; file vận hành cấp *quy trình + pháp lý + KPI*; sổ quyết định cấp *ai đã chọn gì*.
**Không trộn nhân vật/giọng giữa các dịch vụ.**

---

## Quick start (3 bước)

1. **Instructions:** dán toàn bộ khối giữa hai vạch ▼▲ trong [`SYSTEM-PROMPT.md`](SYSTEM-PROMPT.md) vào ô **Chỉ dẫn** (Gemini) / **Instructions** (ChatGPT) / **Project instructions** (Claude).
2. **Knowledge:** upload **6 file** `.md` trong `knowledge/` — nhớ cả [`decisions.md`](knowledge/decisions.md), thiếu file này Agent sẽ tự quyết thay bạn.
3. **Test:** chạy câu lệnh smoke test bên dưới.

**Câu lệnh đầu tiên để test:**

```
Bạn là ai, làm được gì, đang nạp dịch vụ nào? Liệt kê 4 mode và cho biết
có bao nhiêu nhân vật, bao nhiêu format, bao nhiêu hook trong Tri thức.
```

Đúng thì Agent trả lời: Media Content Producer · dịch vụ Giảm béo đa khoa · 4 mode SCRIPT/BATCH/CALENDAR/HOOK · 5 nhân vật (NV1–NV5) · 17 format (F01–F17) · 86 hook (H01–H86).

### Đường dự phòng — upload 1 file thay cho 6 file

Nền tảng chặn số file (**Gemini Gems trần 10 file**) hoặc upload nhiều file một lượt bị lỗi thì dùng bản gộp [`goi/GOP-tri-thuc.md`](goi/GOP-tri-thuc.md) (110 KB) thay cho cả **6 file** `knowledge/`.

Nội dung **giống hệt bản rời** — mỗi phần mở đầu bằng dòng `===== tên file =====` nên Agent vẫn đọc đúng từng module, kể cả `decisions.md`.

> ⚠ **Đánh đổi:** dùng bản gộp thì **mất khả năng thay riêng một module** — sửa `decisions.md` là phải sinh lại và upload lại cả bản gộp. **Bản rời vẫn là đường chính.**
>
> Sinh lại sau khi sửa tri thức: `python tools/gop-tham-khao.py`. ⛔ Không sửa tay file trong `goi/`.

---

## Cấu trúc repo

```
SYSTEM-PROMPT.md                    Bộ não Agent (dán vào Instructions)
README.md                           File này
TESTING.md                          10 kịch bản nghiệm thu + phụ lục lỗi dữ liệu
knowledge/
├── giambeo-plan.md                 Trụ cột P1–P5 · Nhân vật NV1–NV5 · Bối cảnh S1–S10
│                                   · Nhân vật phụ NP1–NP4 · Nguyên mẫu khách A1–A5
├── giambeo-format-bank.md          17 format F01–F17: cấu trúc dựng, thời lượng, batch
├── giambeo-hook-bank.md            86 hook H01–H86 theo cụm insight
├── giambeo-script-samples.md       10 kịch bản mẫu KB-01–KB-10 (chuẩn đầu ra)
├── media-production.md             Quy trình 7 bước · lịch batch · call sheet · ekip
│                                   · KPI 3 tầng · checklist pháp lý 12 điểm
└── decisions.md                    Sổ quyết định DP01–DP10 — nơi con người ký
documents/                          Tài liệu nguồn (workbook 12 sheet · docx · link)
goi/GOP-tri-thuc.md                 Bản gộp 6 file knowledge — đường dự phòng khi
                                    chạm trần số file. Sinh bằng tools/gop-tham-khao.py
tools/gop-tham-khao.py              Sinh lại bản gộp sau khi sửa knowledge/
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

## Ví dụ mẫu đầu ra

Đây là **chuẩn nghiệm thu** cho từng mode. Đầu ra của Agent phải đạt đúng mức chi tiết này — thiếu phần nào là chưa đạt.
Bộ kiểm thử đầy đủ: [`TESTING.md`](TESTING.md).

<details>
<summary><b>Mode SCRIPT</b> — mẫu đầy đủ 9 phần (§12)</summary>

**Lệnh:** `SCRIPT: Viết 1 kịch bản cho NV1, dùng hook H20, format F07, quay tại S2. Thời lượng 40 giây. Nguyên mẫu khách hàng A3.`

---

### KB-11 — "Mỡ nội tạng không nhìn thấy bằng gương"

| Nhân vật | Format | Bối cảnh | Thời lượng | Trụ cột | Tầng phễu | Mã hook |
|---|---|---|---|---|---|---|
| NV1 — Bác sĩ Nội tiết | F07 Test tại chỗ | S2 Phòng đo InBody | 40 giây | P2 Bằng chứng & chỉ số | TOF | H20 |

**Diễn viên:** NV1 + khách hàng nguyên mẫu **A3** (anh quản lý 45 tuổi, vòng bụng 102cm, ngại đến phòng khám)

**Đạo cụ:** Máy InBody, thước dây mềm, bản in kết quả InBody (đã che thông tin cá nhân), màn hình hiển thị chỉ số mỡ nội tạng, bút highlight

#### Phân cảnh theo giây

| Giây | Khối | Nội dung & thoại |
|---|---|---|
| 0–3s | HOOK | Cận gương, khách đứng nhìn nghiêng, bụng phẳng hơn tưởng. NV1 ngoài khung: "Mỡ nội tạng không nhìn thấy bằng gương. Chỉ thấy bằng máy này." |
| 3–8s | BỐI CẢNH | Cắt rộng phòng InBody. NV1 chỉ vào máy: "Anh Tuấn, 45 tuổi. Nhìn ngoài anh không béo. Mình đo thử." |
| 8–20s | LÕI 1 — Demo | Khách bước lên máy, cầm tay nắm điện cực. Đếm ngược. Màn hình chạy kết quả. NV1: "Bốn mươi giây. Không đau, không kim." |
| 20–32s | LÕI 2 — Đọc số | NV1 highlight đúng một dòng trên bản in: chỉ số mỡ nội tạng. "Cân nặng anh trong ngưỡng. Nhưng dòng này thì không." Cắt cận thước dây: vòng bụng đo tại chỗ. |
| 32–40s | CHỐT & CTA | NV1 nhìn ống kính: "Nếu anh không có máy, hãy dùng thước dây. Nam trên 90cm là con số y học cần để ý. **Lưu lại video này** và đo thử tối nay." |

- **Chữ trên màn hình:** Số mỡ nội tạng phóng to ở giây 20; số vòng bụng phóng to ở giây 28. **Che toàn bộ tên, ngày sinh, mã hồ sơ** trên bản in và trên màn hình máy. Phụ đề 100%. Cuối video hiện tên cơ sở · địa chỉ · số giấy phép.
- **CTA:** "Lưu lại video này và đo thử tối nay" → clip nuôi nhận biết (TOF), không đẩy lịch hẹn. Đội tiếp nhận: Quản trị kênh gom bình luận hỏi cách đo cho format F10.
- **Lưu ý khi quay:**
  - Không kết luận bệnh lý cho khách trên video (L09). Chỉ mô tả ngưỡng chỉ số.
  - Không nói "anh bị gan nhiễm mỡ" — nói "con số này là lý do nên đi kiểm tra thêm".
  - Kiểm khung hình trước mỗi cú máy: không để lọt hồ sơ/nhãn mẫu của khách khác (L10).
  - Consent ký trước khi bấm máy, gồm mục *sử dụng chỉ số sức khoẻ* (L05).
  - **Cần bác sĩ kiểm duyệt ký duyệt trước khi quay.**
- **Cần xác minh:**

  | Hạng mục | Trạng thái |
  |---|---|
  | Ngưỡng vòng bụng nam 90cm — xác nhận nguồn hướng dẫn phòng khám đang áp dụng | ⚠ Cần xác minh từ bác sĩ kiểm duyệt |
  | Chỉ số mỡ nội tạng thật của khách A3 | ⚠ Cần xác minh — lấy tại buổi đo, không dựng số trước |
  | Consent của anh Tuấn (quay hình + chỉ số sức khoẻ) | ⚠ Cần xác minh — Điều phối sản xuất thu trước 48h |
  | Quyền quay hình máy InBody (logo hãng) | ⚠ Cần xác minh |

</details>

<details>
<summary><b>Mode HOOK</b> — mẫu bảng 9 cột (§15)</summary>

**Lệnh:** `HOOK: Tổng đài nhận nhiều câu hỏi "uống thuốc giảm cân mua trên mạng có hại gan không". Sinh 5 hook cho cụm insight này, phân bổ cho NV1 và NV5.`

**Đã có trong bank — cụm "Thuốc & lời đồn" (H23–H29):** H24 đã phủ góc *đọc nhãn, hoạt chất bị cấm*; H25 đã phủ góc *thuốc được cấp phép cần kê đơn*. Hook mới dưới đây tránh trùng hai góc này.

| Mã hook | Cụm insight / nỗi đau | Nhân vật | Trụ cột | Tầng phễu | HOOK (3 giây — đọc nguyên văn) | Góc triển khai | Format gợi ý | Trạng thái duyệt |
|---|---|---|---|---|---|---|---|---|
| H24 | Thuốc & lời đồn | NV1 | P1 | TOF | Thuốc giảm cân bán trên mạng — tôi đọc bảng thành phần này cho bạn nghe | *(đã có trong bank)* | F03 | Chờ duyệt |
| H25 | Thuốc & lời đồn | NV1 | P1 | MOF | Có nhóm thuốc giảm cân thật, được cấp phép. Nhưng nó không dành cho tất cả mọi người | *(đã có trong bank)* | F02 | Chờ duyệt |
| **H87** | Thuốc & lời đồn | NV1 | P1 | TOF | Gan là nơi xử lý mọi thứ bạn nuốt vào. Kể cả viên bạn mua trên mạng | Cơ chế chuyển hoá qua gan; vì sao men gan là xét nghiệm bắt buộc trước khi dùng bất kỳ thuốc hỗ trợ nào | F02 | Chờ duyệt |
| **H88** | Thuốc & lời đồn | NV1 | P2 | MOF | Trước khi kê bất cứ thứ gì, tôi xem đúng ba dòng trong tờ xét nghiệm này | Bộ chỉ số gan – thận – đường huyết và lý do từng chỉ số | F01 | Chờ duyệt |
| **H89** | Thuốc & lời đồn | NV1 | P1 | TOF | "Thảo dược nên lành" — đây là chỗ câu đó sai | Thảo dược vẫn chuyển hoá qua gan; hàng không nhãn, không số đăng ký | F02 | Chờ duyệt |
| **H90** | Thuốc & lời đồn | NV5 | P4 | MOF | Bệnh nhân giấu chuyện uống thuốc giảm cân trước mổ. Đây là chuyện đã xảy ra | Vì sao phải khai báo mọi thứ đang dùng trước phẫu thuật; rủi ro gây mê và đông máu | F13 | Chờ duyệt |
| **H91** | Thuốc & lời đồn | NV5 | P4 | BOF | Men gan của bạn cao, tôi hoãn mổ. Không phải tôi làm khó bạn | Men gan bất thường là tiêu chí hoãn phẫu thuật; quy trình chuyển bạn sang khoa nội tiết | F13 | Chờ duyệt |

**Lưu ý:** không hook nào nêu tên biệt dược hoặc liều dùng (L11). Toàn bộ ở mức *nhóm thuốc* + "phải do bác sĩ chỉ định".
**Cần xác minh:** cụm insight này lấy từ tổng đài tuần nào, bao nhiêu lượt hỏi → ⚠ Cần xác minh từ CSKH trước khi đưa vào họp B1.

</details>

<details>
<summary><b>Mode BATCH</b> — mẫu call sheet (§13)</summary>

**Lệnh:** `BATCH: Gom 9 clip cho Batch nhanh 1.1 (thứ Tư, 12:00–13:30). Xuất call sheet theo khung giờ.`

**Buổi quay:** Batch nhanh 1.1 · S10 Studio Trust (set cố định, **không tháo**) · ekip 2 người · teleprompter · chỉ F02/F10/F16

#### Call sheet

| Khung giờ | Nhân vật / bộ phận | Nội dung (mã clip) | Phụ trách |
|---|---|---|---|
| 11:45–12:00 | Trợ quay | Bật đèn 3 điểm S10 (đã dựng sẵn), test mic, nạp kịch bản vào teleprompter | Trợ quay |
| 12:00–12:05 | Toàn bộ | Chạy nhanh danh sách 9 clip, thứ tự nhân vật | Điều phối |
| 12:05–12:40 | **NV1** | F02 × 4: H01 · H07 · H09 · H23 — talking head, teleprompter | DOP |
| 12:40–12:45 | — | Đổi nhân vật (2 phút) + chỉnh mic, **không đổi set** | Trợ quay |
| 12:45–13:10 | **NV2** | F10 × 3: H92 · H93 · H94 — đọc bình luận thật (đã che tên) | DOP |
| 13:10–13:25 | **NV1** | F16 × 2: H10 · H12 — con số biết nói, đồ hoạ hậu kỳ | DOP |
| 13:25–13:30 | Toàn bộ | Bảng kiểm 9/9 clip · **sao lưu thẻ nhớ ngay tại chỗ** | Trợ quay |

**Tổng clip:** 4 (F02) + 3 (F10) + 2 (F16) = **9/9 ✅**

#### Khách hàng cần mời

| Khách | Clip liên quan | Trạng thái consent |
|---|---|---|
| — | Không có clip nào cần khách hàng thật trong buổi này | Không áp dụng |

#### Đạo cụ theo set

| Set | Đạo cụ |
|---|---|
| S10 Studio Trust | Bảng viết kính + bút · ghế cao · 4 ảnh chụp bình luận đã che tên (in A5) · mô hình mỡ nội tạng (cho H10) · hộp trà đã bóc nhãn (cho H23) |

#### Sáu nguyên tắc cứng — nhắc lại trước khi bấm máy

1. **Không tháo set S10** — đây là điều kiện để đạt 90 video/tháng
2. **Gom theo bối cảnh, không gom theo nhân vật** — đổi set 15 phút, đổi nhân vật 2 phút
3. **Trang phục cố định theo nhân vật cả ngày** — để clip phát rải 30 ngày không lộ quay gộp
4. **Mỗi clip quay tối đa 3 lần** — quá 3 lần chuyển clip khác, quay lại cuối buổi
5. **Consent trước, máy chạy sau** — không có bản ký thì không bấm máy
6. **Sao lưu trong ngày** — không để footage qua đêm trên thẻ nhớ

#### Ghi chú của Agent (phần Agent phải chủ động nêu)

- **F10 không có hook sẵn trong bank** — theo thiết kế, F10 trả lời bình luận có thật, nên 3 hook `H92 · H93 · H94` là hook **mới sinh trong buổi họp B1**, trạng thái *Chờ duyệt*, đánh mã tiếp sau H91. Không dùng lại hook TOF cũ cho F10.
- **Xung đột Tri thức:** H10 và H12 ghi trụ cột **P1** nhưng format F16 thuộc **P2** trong format bank. Đã lấy trụ cột theo format (**P2**) để lịch xuất bản tính tỷ trọng đúng — cần chốt lại nguồn chân lý (`TESTING.md` Phụ lục A-1).

**Cần xác minh:**

| Hạng mục | Trạng thái |
|---|---|
| 3 ảnh chụp bình luận cho F10 — đã che hết tên/avatar (L10) | ⚠ Cần xác minh từ Quản trị kênh |
| 3 bình luận này là bình luận thật, không dàn dựng | ⚠ Cần xác minh từ Quản trị kênh |
| Con số dùng trong H10 · H12 (dữ liệu phòng khám đã ẩn danh) | ⚠ Cần xác minh từ phòng khám |

</details>

<details>
<summary><b>Mode CALENDAR</b> — mẫu bảng phẳng 14 cột (§14)</summary>

**Lệnh:** `CALENDAR: Lập lịch xuất bản tuần 1 tháng 10/2026, 3 bài/ngày. Trạng thái mặc định "Chưa quay".`

> Mode CALENDAR **xuất file tự động, không hỏi** → `Media-Calendar-GiamBeo.xlsx`
> Trích 3 ngày đầu; bảng đầy đủ 21 dòng nằm trong file.

| STT | Ngày | Thứ | Tuần | Khung giờ | Kênh | Trụ cột | Nhân vật | Format | Mã hook | Chủ đề / Hook | Bối cảnh | Buổi quay | Trạng thái |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 01/10/2026 | Thứ Năm | Tuần 1 | 07:00 | Facebook Page | P1 | NV1 | F02 | H01 | Bạn không thiếu ý chí. Bạn thiếu một tờ xét nghiệm. | S10 | Batch nhanh 1.1 | Chưa quay |
| 2 | 01/10/2026 | Thứ Năm | Tuần 1 | 12:15 | TikTok | P2 | NV2 | F04 | H30 | Bữa sáng này 420 kcal. Bữa sáng 'healthy' bạn hay ăn: 780 kcal | S4 | Batch lớn 1A | Chưa quay |
| 3 | 01/10/2026 | Thứ Năm | Tuần 1 | 20:00 | Reels + TikTok | P4 | NV5 | F13 | H66 | Đây là bốn trường hợp tôi từ chối hút mỡ trong tuần này | S8 | Batch lớn 1A | Chưa quay |
| 4 | 02/10/2026 | Thứ Sáu | Tuần 1 | 07:00 | Facebook Page | P1 | NV3 | F06 | H54 | Squat sai ở 90% người tập. Chỉ cần sửa một điểm này | S5 | Batch lớn 1A | Chưa quay |
| 5 | 02/10/2026 | Thứ Sáu | Tuần 1 | 12:15 | TikTok | P2 | NV1 | F01 | H05 | Cân nặng đứng yên nhưng mỡ giảm 4kg — chị ấy suýt bỏ cuộc | S2 | Batch lớn 1B | Chưa quay |
| 6 | 02/10/2026 | Thứ Sáu | Tuần 1 | 20:00 | Reels + TikTok | P5 | NV2 | F17 | H81 | Bữa trưa thật của chuyên gia dinh dưỡng — không dàn dựng | S9 | Cơ hội 1 | Chưa quay |
| 7 | 03/10/2026 | Thứ Bảy | Tuần 1 | 07:00 | Facebook Page | P3 | NV4 | F08 | H61 | Sau ba buổi trị liệu, chị ấy đi bộ được 30 phút không đau | S6 | Docu 1 | Chưa quay |
| 8 | 03/10/2026 | Thứ Bảy | Tuần 1 | 12:15 | TikTok | P1 | NV2 | F02 | H34 | Đi ăn cưới mà không phá phác đồ: 3 quy tắc | S10 | Batch nhanh 1.1 | Chưa quay |
| 9 | 03/10/2026 | Thứ Bảy | Tuần 1 | 20:00 | Reels + TikTok | P4 | NV1 + NV2 + NV5 | F12 | H74 | Hội chẩn ca này: ba chuyên khoa, ba ý kiến khác nhau | S1 | Batch lớn 1A | Chưa quay |

**Tự kiểm (§17):** mỗi ô một giá trị, không gộp ô · không trùng mã hook · không lặp format ở hai slot liền kề trong cùng ngày · cột `Trụ cột` khớp trụ cột của format cùng dòng · mỗi dòng map về một buổi quay có thật.

**Cần xác minh:** quy tắc luân phiên kênh theo khung giờ chưa có trong Tri thức → ⚠ Cần xác minh từ Quản trị kênh (xem `TESTING.md` Phụ lục A-11).

</details>

---

## Quy trình chuẩn của Agent

1. Làm rõ yêu cầu → xác định dịch vụ + mode
2. Đọc **sổ quyết định**, rồi đọc Tri thức, tra hook bank trước khi sáng tác
3. Trình **spec ngắn** trong chat
4. **Dừng chờ "ok"**
5. Triển khai + tự rà theo checklist §17
6. Đóng bằng **Khối lựa chọn ⚖** — những gì Agent đã tự mặc định và cách bạn đổi

Yêu cầu sửa nhỏ (đổi 1 hook, 1 phân cảnh, 1 CTA) → làm trực tiếp, bỏ bước spec.
Gặp chỗ Tri thức mâu thuẫn mà chưa có mã `DP` nào phủ → **dừng và hỏi**, không tự chọn.

---

## Guardrail then chốt

Agent **không bao giờ**: cam kết số cân/kết quả · dùng "100% / khỏi hoàn toàn / không đau / số 1" · chẩn đoán cá nhân qua bình luận · nêu tên biệt dược hay liều dùng · bịa số liệu, ca bệnh, giá, thông tin bác sĩ · để nhân vật nói ngoài lãnh địa chuyên môn.

Mọi kịch bản y khoa đều gắn dòng **"Cần bác sĩ kiểm duyệt ký duyệt trước khi quay."** Số liệu thiếu → `⚠ Cần xác minh`.

---

## Nghiệm thu Agent

Trước khi bàn giao cho team Media, chạy bộ kiểm thử **[`TESTING.md`](TESTING.md)** — 12 kịch bản, 105 điểm.

| Nhóm | Test | Kiểm cái gì |
|---|---|---|
| Smoke | T01 | Nạp đủ 6 file, đúng số nhân vật/format/hook, không bịa |
| Chức năng | T02 · T03 | SCRIPT — đủ 9 phần §12, 4 khối §10, spec gate, bảng tổng hợp |
| Chức năng | T04 | HOOK — tra bank trước, đánh mã từ H87, đủ 9 cột |
| Chức năng | T05 | BATCH — gom theo bối cảnh, đổi set 15 phút, trạng thái consent |
| Chức năng | T06 | CALENDAR — 14 cột, xuất tự động không hỏi, tỷ trọng trụ cột |
| Đối kháng | T07 | Guardrail — từ chối cam kết kg, biệt dược, "số 1", bỏ pháp lý |
| Đối kháng | T08 | Lãnh địa — NV2 không nói hút mỡ; 2 nhân vật → bắt buộc F12 |
| Đối kháng | T09 | Mã ma (H99/F23/NV7) và bịa số liệu → `⚠ Cần xác minh` |
| Đối kháng | T10 | Dịch vụ chưa nạp → không mượn nhân vật của Giảm béo |
| **Khung** | **T11** | **Tri thức mâu thuẫn → Agent trình lựa chọn, không tự chọn; đảo được bằng `DP02 = B`** |
| **Khung** | **T12** | **Nhãn nguồn; và bốn việc chặn cứng kể cả khi người dùng bảo "cứ tự quyết"** |

**Ngưỡng bàn giao:** ≥ 95/105 điểm **và** 0 lỗi chặn 🔴.

> **T11 và T12 là bài kiểm tra của chính cái khung.** Sai 🔴 ở đây thì các test còn lại đạt bao nhiêu cũng không bàn giao được — vì người dùng sẽ tưởng đã có người duyệt trong khi không ai duyệt cả.
>
> 10 điểm quyết định `DP01`–`DP10` nằm ở [`knowledge/decisions.md`](knowledge/decisions.md). **Chưa chốt điểm nào cũng không chặn Agent chạy** — nhưng `DP02` và `DP04` khiến mode CALENDAR chưa thể đúng tỷ trọng cho tới khi có người ký.

---

## Thêm dịch vụ mới

Chỉ thêm 4 file `knowledge/<dịch-vụ>-plan|format-bank|hook-bank|script-samples.md` theo đúng cấu trúc của bộ `giambeo-*`. **Không sửa `SYSTEM-PROMPT.md`.** File `media-production.md` dùng chung, chỉ sửa khi quy trình vận hành thực sự thay đổi.

`decisions.md` cũng dùng chung: dịch vụ mới có điểm nào cần người chọn thì **thêm mã `DP` mới vào cuối sổ**, ghi rõ dịch vụ nào ở cột *Ảnh hưởng tới*. Không tạo sổ quyết định riêng cho từng dịch vụ — một sổ để không ai phải đi tìm.

---

*Quyết định cuối luôn thuộc người dùng. Không có chữ ký bác sĩ kiểm duyệt thì không bấm máy.*
 
