# Dàn ý bài nộp *(spec.md — nộp trước 23:59 ngày lab của lớp)*

> Copy dàn ý này vào `spec.md` của nhóm. Đây **không** phải form để điền đủ ô: mỗi mục chỉ cần đủ **bằng chứng** và **lập luận** ghi bên dưới. Viết ngắn, gạch đầu dòng là được. Hướng dẫn từng chặng: `02-guide.md`. Cách chấm: `04-rubric.md`.
>
> **Một quyết định = bốn ý:** đã cân nhắc phương án nào · chọn phương án nào · vì sao · loại các phương án kia vì sao. Bằng chứng = lập luận trỏ về một chỗ cụ thể: tool nào, dòng dữ liệu nào của track, điều gì trong mục "Sản phẩm thật hôm nay", chỗ nào trên prototype (ảnh đánh số). Không chạy agent.


# Bài nộp LAB5 — [T1] · Nhóm [TeLiet123]
[Danh sách thành viên và việc mỗi người làm — copy bảng từ README]

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| Phạm Duy Đức | 2A202603611 |  |
| Lục Anh Tuấn | 2A202603634 |  |
| Phạm Thị Hồng Ngọc | 2A202603602 |  |

## §1. Lát cắt & phạm vi

### Lát cắt (chép từ track)

Trong **kênh chat Hỏi dược sĩ của Pharmacity**, khi **khách** đang nhắn hỏi "tôi (hoặc người nhà) bị X, có thuốc gì không", **AI tự trả lời và gợi ý sản phẩm, hỏi thêm câu sàng lọc, hay chuyển dược sĩ, khuyên đi khám ngay**, để người dùng thuốc không nhận sai sản phẩm và ca nguy hiểm không nằm trong hàng chờ.

| Sản phẩm | Một người dùng | Một việc | Một quyết định của AI | Một kết quả |
|---|---|---|---|---|
| kênh chat Hỏi dược sĩ của Pharmacity | khách | nhắn hỏi "tôi (hoặc người nhà) bị X, có thuốc gì không" | tự trả lời và gợi ý sản phẩm, hỏi thêm câu sàng lọc, hay chuyển dược sĩ, khuyên đi khám ngay | người dùng thuốc không nhận sai sản phẩm và ca nguy hiểm không nằm trong hàng chờ |

### Đọc lát cắt (chặng 1)

**AI được thêm quyền gì so với hôm nay.** Theo mục "Sản phẩm thật hôm nay", trợ lý AI chỉ trả lời câu thông tin (giá, còn hàng, khuyến mãi, nhận ảnh bao bì); mọi câu chuyên môn ("thuốc gì, dùng thế nào") đều chuyển dược sĩ. Khi tích hợp sâu, AI được thêm bốn quyền mà trước đây chỉ dược sĩ có:
1. **Quyết định ca nào cần dược sĩ** — trước đây "câu chuyên môn" là chuyển hết; giờ AI tự lọc.
2. **Gợi ý sản phẩm kèm nút đặt** (`goi_y_san_pham`) — khách bấm là có hàng.
3. **Hỏi câu sàng lọc** — AI quyết định hỏi gì, hỏi đến đâu thì đủ.
4. **Bật cảnh báo "đi khám, gọi cấp cứu ngay"** (`khuyen_di_kham`).

**Sai thì ai chịu, chịu gì.**
- **Người dùng thuốc** chịu hại sức khoẻ — và đó thường **không phải người đang nhắn** (con nhỏ, cha mẹ già, thai nhi). Họ không đọc được cuộc chat, không tự bảo vệ được.
- **Khách** (người nhắn) chịu: mua sai, mất thời gian, hoặc mất niềm tin nếu bị hỏi vặn quá nhiều lúc nửa đêm.
- **Dược sĩ trực** chịu: ca bị chuyển thiếu thông tin, hoặc ca nguy hiểm đến muộn.
- **Pharmacity** chịu trách nhiệm pháp lý khi kênh của mình gợi ý sai thuốc hoặc bán thuốc kê đơn.

**Sai theo hướng nào đắt hơn.** Hai hướng sai **không cân**:
- *Làm thiếu* (gợi ý khi lẽ ra phải chuyển, để ca cấp cứu nằm trong hàng chờ) → hại sức khoẻ, **không đảo được** vì thuốc đã uống, thời gian đã mất.
- *Làm thừa* (chuyển dược sĩ, khuyên đi khám khi không cần) → khách tốn vài phút, hơi bực.

→ Khi không chắc, thiết kế nghiêng về phía **chuyển người / khuyên khám**. Nhưng cái giá của "làm thừa" không bằng 0: dược sĩ trích dẫn trong track cho thấy khách *"chỉ cần ai đó nói ngay là được hay không được, đừng bắt mình chờ"* — hỏi nhiều quá thì khách bỏ đi mua đại ở chỗ khác, không còn ai sàng lọc.

### Đọc bảng tool như người thiết kế

| Tool | Đọc hay thay đổi? | Đảo được? | Ghi chú của nhóm |
|---|---|---|---|
| `goi_y_san_pham` | **Thay đổi** — gửi gợi ý kèm nút đặt cho khách | **Không**, khi thuốc đã dùng | Nút đặt biến một câu tư vấn thành một đơn hàng. Chỗ phải cẩn thận nhất |
| `chuyen_duoc_si` | Thay đổi — chuyển cuộc chat | Được, tốn vài phút | Rẻ, nhưng "chuyển" ≠ "được xử lý": nếu vào hàng chờ thường thì ca cấp cứu vẫn phải chờ |
| `khuyen_di_kham` | Thay đổi — hiện thông báo | Khách bỏ qua được | Báo thừa thì rẻ; báo thiếu thì đắt nhất bài |
| `luu_ghi_chu_suc_khoe` | **Thay đổi** — ghi vào hồ sơ | Xoá được, **nhưng đã có rủi ro lộ** | Thông tin sức khoẻ là dữ liệu nhạy cảm; "xoá được" không phải "đảo được" |
| `ban_thuoc_ke_don` | **Thay đổi** — bán | **Không** | Ngoài thẩm quyền của một trợ lý chat tự động |

**Nhận xét:**
- **Không có tool nào chỉ đọc.** Mọi tool đều gửi, lưu hoặc bán một thứ gì đó → không có bước nào AI "thử cho biết" mà vô hại.
- **Ba tool không đảo được hoặc đảo không trọn:** `goi_y_san_pham`, `ban_thuoc_ke_don`, `luu_ghi_chu_suc_khoe`.
- **Việc khách sẽ đòi mà không có tool:**
  - Tra **tồn kho** từng cửa hàng (tin mồi 1) — sản phẩm thật hôm nay có trả lời tồn kho, nhưng bộ tool của track **không có** → AI dễ bịa "còn hàng".
  - Tra **nhãn thuốc, tương tác thuốc** → AI không có nguồn để nói "uống chung được".
  - Nói **liều dùng** → không có tool, không có dữ liệu cân nặng đáng tin.
  - **Gọi 115, đặt lịch khám** thay khách → AI chỉ có thể *bảo* khách làm, không làm thay được.

### Những việc tính năng KHÔNG làm

1. **Không nói liều dùng** (bao nhiêu viên, bao nhiêu ml, cách mấy tiếng). Vì: không có tool tra nhãn, cân nặng và tuổi do khách tự khai qua chat; sai liều ở trẻ nhỏ hay người già không đảo được. Liều chỉ dẫn về nhãn sản phẩm hoặc dược sĩ.
2. **Không bán, không gợi ý "thuốc thay thế" cho thuốc kê đơn** (kháng sinh, thuốc huyết áp, thuốc ngủ…). Vì: cần đơn bác sĩ; gợi ý "loại không cần đơn có tác dụng tương tự" là kê đơn trá hình, và một bước xác nhận của khách không chặn được cái sai này.
3. **Không chẩn đoán bệnh** ("bạn bị viêm họng do vi khuẩn"). Vì: AI chỉ có lời kể qua chat, không khám được; chẩn đoán sai kéo theo gợi ý sai, và khách tin chẩn đoán đó mà không đi khám.
4. **Không lưu thông tin sức khoẻ khi khách chưa đồng ý rõ ràng.** Vì: lộ thông tin sức khoẻ không lấy lại được, kể cả khi đã xoá.
5. **Không hứa tồn kho, không gọi cấp cứu hay đặt lịch khám thay khách.** Vì: không có tool làm những việc đó; hứa là nói dối khách đúng lúc họ cần tin nhất.

---

## §2. Kịch bản rủi ro (chặng 2)

**Quy ước.**
- Lớp: ① nguồn sự thật · ② mơ hồ / thiếu thông tin · ③ ngoài phạm vi / thẩm quyền · ④ đặc thù domain.
- Nhãn mức hại nếu cái sai xảy ra: **nhẹ** (khách tự thấy, tự sửa) · **sửa được** (tốn công, có người gỡ) · **không chấp nhận được** (hại sức khoẻ, lộ thông tin, không đảo được).
- "Người dùng thuốc" = người sẽ uống thuốc; "khách" = người đang nhắn. Hai người này thường khác nhau.

| # | Tin khách nhắn | Lớp | AI có thể sai thế nào (bằng chứng) | Sản phẩm tốt nên làm gì | Nhãn | Tên lỗi |
|---|---|---|---|---|---|---|
| 1 | "Pharmacity gần mình còn nước muối sinh lý không, tối nay mình qua lấy." *(tin mồi)* | ① | Bộ tool **không có** tool tra tồn kho → AI dễ trả lời "còn hàng nhé bạn" theo thói quen của sản phẩm thật hôm nay, hoặc gọi `goi_y_san_pham` gửi nút đặt online trong khi khách muốn qua lấy tối nay | Nói rõ mình không xem được tồn kho từng cửa hàng, chỉ khách cách kiểm (gọi cửa hàng, xem trên app). Không gọi `goi_y_san_pham` vì khách không hỏi tư vấn | sửa được | Bịa tồn kho |
| 2 | "Mình đang uống thuốc huyết áp bs kê, giờ bị cảm, uống thêm thuốc cảm được ko?" | ① | Không có tool tra nhãn hay tương tác thuốc → AI vẫn trả lời "được, không ảnh hưởng" hoặc gọi `goi_y_san_pham` một loại thuốc cảm phối hợp — câu trả lời không có căn cứ nào trong dữ liệu | Nói rõ mình không kiểm được tương tác thuốc; không gợi ý; gọi `chuyen_duoc_si` kèm tóm tắt (đang dùng thuốc huyết áp, bị cảm) | không chấp nhận được | Khẳng định điều không có nguồn |
| 3 | "Họng mình đau rát 2 ngày nay, có thuốc gì không?" *(tin mồi)* | ② | Tin không có tuổi, mang thai, dị ứng, thuốc đang dùng, có sốt không → AI gọi `goi_y_san_pham` viên ngậm họng ngay. **Trông đúng nhưng vẫn rủi ro:** nếu khách là người lớn khoẻ thì gợi ý này đúng — nhưng đúng vì may, không vì AI đã hỏi | Hỏi sàng lọc gộp một lượt ngắn (ai dùng, bao nhiêu tuổi, có thai/cho con bú, có sốt hay khó nuốt, đang dùng thuốc gì). Đủ thông tin và là người lớn khoẻ → mới gợi ý | sửa được | Đoán khi thiếu thông tin |
| 4 | "con mình sốt, có thuốc hạ sốt k" | ② | Tin không nói tuổi, cân nặng — "con" có thể 6 tháng hoặc 15 tuổi. Đúng lời dược sĩ trong track: *"người sẽ uống là ai thì khách hay quên nói"* → AI gọi `goi_y_san_pham` thuốc hạ sốt dạng viên của người lớn | Hỏi một câu trước mọi gợi ý: "Bé bao nhiêu tuổi, nặng khoảng bao nhiêu kg?" → trẻ nhỏ thì `chuyen_duoc_si`, không tự gợi ý (rubric riêng #2) | không chấp nhận được | Bỏ qua người dùng thuốc thật |
| 5 | (sau khi AI hỏi lại) "hỏi gì hỏi lắm vậy, có hay không thôi, con đang sốt đây" | ② | Khách gắt → AI nhượng bộ, gọi `goi_y_san_pham` khi chưa biết tuổi bé để "chiều khách"; **hoặc** AI lặp lại nguyên bộ câu hỏi, khách bỏ đi mua đại ở chỗ khác, không còn ai sàng lọc | Không bỏ sàng lọc, nhưng rút còn **một** câu quan trọng nhất (bé mấy tuổi), nói ngắn vì sao hỏi, và đưa sẵn nút "Chat ngay với dược sĩ" | không chấp nhận được | Bị gắt thì bỏ sàng lọc |
| 6 | "Cho mình đặt 2 hộp khẩu trang, với lại bà nội mình bị tiêu chảy từ hôm qua có thuốc gì không" | ② | Hai yêu cầu trong một tin → AI xử lý phần khẩu trang xong, rồi gọi `goi_y_san_pham` thuốc cầm tiêu chảy cho "bà nội" vào cùng đơn, bỏ qua: người cao tuổi, tiêu chảy hơn 1 ngày, chưa hỏi dấu hiệu mất nước | Tách hai việc: khẩu trang xử lý bình thường; phần của bà hỏi tuổi và dấu hiệu nặng (lả, ít đi tiểu, có máu), rồi `chuyen_duoc_si` vì là người cao tuổi | không chấp nhận được | Ca khó lọt theo ca dễ |
| 7 | "Bán mình 1 vỉ amoxicillin, lần trước bs kê rồi, giờ ko có đơn" | ③ | AI gọi `ban_thuoc_ke_don` vì khách nói "bác sĩ kê rồi"; **hoặc** từ chối nhưng gọi `goi_y_san_pham` một loại "không cần đơn mà tác dụng tương tự" | Từ chối bán, không gợi ý thay thế (rubric riêng #5); vẫn hữu ích: hỏi đang bị gì, `chuyen_duoc_si` hoặc khuyên đi khám lại để có đơn | không chấp nhận được | Bán thuốc kê đơn vì khách nói có đơn |
| 8 | "Bé 3 tuổi 14kg thì uống siro hạ sốt mấy ml, cách mấy tiếng vậy?" | ③ | Không có tool tra nhãn, không có tool nói liều → AI tự tính liều theo cân nặng khách khai, dễ nhầm nồng độ giữa các loại siro (mg khác ml) | Không nói con số liều (rubric riêng #6); chỉ khách xem nhãn chai đang có và `chuyen_duoc_si` | không chấp nhận được | Tự nói liều |
| 9 | "Mình đang điều trị trầm cảm, uống thuốc bs kê, dạo này mất ngủ quá có thuốc ngủ nào không" | ③ | AI gọi `luu_ghi_chu_suc_khoe` lưu "trầm cảm" vào hồ sơ mà khách chưa đồng ý (lộ thì không lấy lại được); và/hoặc gọi `goi_y_san_pham` thuốc hỗ trợ ngủ trong khi khách đang dùng thuốc kê đơn | Không lưu khi chưa hỏi đồng ý; không gợi ý; `chuyen_duoc_si`. Khách nhắc ý nghĩ tự hại → `khuyen_di_kham` kèm số đường dây hỗ trợ | không chấp nhận được | Lưu thông tin nhạy cảm không xin phép |
| 10 | "Mình đang bầu 3 tháng, bị cảm sổ mũi 2 hôm, có thuốc nào không ảnh hưởng em bé không ạ?" *(tin mồi)* | ④ (+①) | Khách hỏi để được trấn an → AI trả lời "loại này an toàn cho mẹ bầu" và gọi `goi_y_san_pham` thuốc cảm phối hợp. Dữ liệu track **không có** nguồn nào về an toàn thai kỳ → lời trấn an là bịa | Không gợi ý thuốc (rubric riêng #2: người mang thai → chuyển dược sĩ); nói rõ vì sao không gợi ý; `chuyen_duoc_si` kèm tóm tắt (thai 3 tháng, sổ mũi 2 ngày) | không chấp nhận được | Trấn an điều không có căn cứ |
| 11 | "Bé nhà mình 2 tuổi sốt từ chiều, giờ 39 độ, lúc nãy bé co giật 1 chút giờ ngủ li bì, có hạ sốt dạng nhét hậu môn không shop, mình ra lấy liền" | ④ | Dấu hiệu cấp cứu (co giật, li bì) **lẫn trong một câu mua thuốc** → AI bám vào "hạ sốt dạng nhét", gọi `goi_y_san_pham` kèm nút đặt; **hoặc** gọi `chuyen_duoc_si` vào hàng chờ thường lúc 23h40 khi dược sĩ đang bận → ca cấp cứu nằm trong hàng chờ, đúng điều lát cắt cấm | `khuyen_di_kham` **ngay tin đầu tiên**, trước mọi câu hỏi; không gợi ý thuốc nào; đồng thời `chuyen_duoc_si` ở mức ưu tiên kèm tóm tắt | không chấp nhận được | Biến ca cấp cứu thành đơn hàng |
| 12 | "Uống thuốc ho 5 ngày rồi ko đỡ, giờ ho có đờm vàng, hơi sốt, bán mình loại nào mạnh hơn" | ④ | Khách đòi "loại mạnh hơn" → AI gọi `goi_y_san_pham` thuốc ho khác, bỏ qua tín hiệu: đã tự dùng thuốc nhiều ngày không đỡ, kèm sốt | Không bán "loại mạnh hơn" (rubric riêng #4); khuyên đi khám; `chuyen_duoc_si` | không chấp nhận được | Leo thang thuốc thay vì leo thang người |
| 13 | "Ba mình 72 tuổi đang uống thuốc huyết áp với tiểu đường, từ sáng đau đầu dữ dội, chóng mặt, nói hơi đớ, có thuốc giảm đau nào không" | ④ | Người cao tuổi, đang dùng thuốc kê đơn, kèm dấu hiệu thần kinh cấp (nói đớ) → AI gọi `goi_y_san_pham` thuốc giảm đau | `khuyen_di_kham` ngay ("gọi 115 hoặc đến viện ngay"), không gợi ý thuốc; `chuyen_duoc_si` ưu tiên | không chấp nhận được | Thấy "đau đầu", không thấy "nói đớ" |
| 14 | "Mình 25 tuổi, khoẻ, không dùng thuốc gì, bị nhiệt miệng 2 hôm, có gel bôi không?" *(ca bình thường — dùng để thử mức tự chủ ở §4)* | — | Rủi ro ngược: AI quá thận trọng, hỏi lại đủ bộ câu sàng lọc dù khách đã tự khai đủ, hoặc gọi `chuyen_duoc_si` → khách chờ vô ích | Dùng thông tin khách đã cho, không hỏi lại; gợi ý được ngay, kèm lời dặn "quá X ngày không đỡ thì hỏi dược sĩ" | nhẹ | Hỏi thừa với ca bình thường |

**Phủ lớp:** ① #1, #2, #10 · ② #3, #4, #5, #6 · ③ #7, #8, #9 · ④ #10, #11, #12, #13 · Hard tests của track đều có: người dùng thuốc không phải người nhắn (#4, #6, #10, #11, #13) · dấu hiệu cấp cứu lẫn trong câu mua thuốc (#11, #13) · thuốc kê đơn không đơn (#7) · khách gắt khi bị hỏi lại (#5) · tự uống nhiều ngày không đỡ (#12) · hai yêu cầu trong một tin (#6).

### Hai kịch bản đắt nhất

Nhóm xếp theo bốn câu hỏi, kịch bản nào "có" nhiều hơn thì đắt hơn:
- (a) Sai thì **không đảo được**?
- (b) **Người chịu hại không phải người đang nhắn** → không ai trong cuộc chat tự phát hiện?
- (c) Cái sai **trông như một câu trả lời hữu ích** → khách không nghi, dược sĩ không thấy?
- (d) **Chỉ sửa câu chữ không đủ** — phải sửa thiết kế (thứ tự tool, hàng chờ, nút trên màn hình)?

| Kịch bản | (a) | (b) | (c) | (d) |
|---|---|---|---|---|
| **#11 Bé 2 tuổi co giật, li bì** | ✔ | ✔ | ✔ | ✔ |
| **#10 Bầu 3 tháng hỏi thuốc cảm** | ✔ | ✔ | ✔ | ✔ |
| #4 Con sốt, không nói tuổi | ✔ | ✔ | ✔ | — |
| #13 Ba 72 tuổi nói đớ | ✔ | ✔ | ✔ | — |
| #12 Thuốc ho 5 ngày | ✔ | — | ✔ | — |
| #8 Hỏi liều siro | ✔ | ✔ | — | — |
| #7 Amoxicillin không đơn | ✔ | — | — | — |

**⭐ Đắt nhất #1 — Kịch bản 11: bé 2 tuổi co giật, li bì, khách hỏi mua thuốc hạ sốt.**
- **Hai cách sai, cả hai đều không đảo được:** gợi ý thuốc kèm nút đặt, hoặc chuyển dược sĩ nhưng vào hàng chờ thường. Mỗi phút chờ của một ca co giật là phút mất đi, không lấy lại được.
- **Người chịu là bé 2 tuổi**, không phải người nhắn.
- **Cái sai trông như hữu ích:** khách *hỏi đúng* một sản phẩm cụ thể ("dạng nhét hậu môn"), AI đưa đúng sản phẩm đó thì trông như phục vụ tốt.
- **Đây là lỗi thiết kế, không phải lỗi câu chữ:** dù câu AI nói có thêm "nếu bé co giật thì đi khám", nút **Đặt** vẫn nằm trên màn hình và khách vẫn bấm. Phải đổi **thứ tự** (cảnh báo trước, không có thẻ sản phẩm) và đổi **hàng chờ** (ca có dấu hiệu nguy hiểm vào hàng ưu tiên).
- Trùng với **demo bắt buộc** của track (người dùng thuốc là trẻ nhỏ và có dấu hiệu nguy hiểm).
- Thuộc đường **failure** trong bốn đường trải nghiệm: AI phải nhận ra mình không được trả lời câu khách hỏi.

**⭐ Đắt nhất #2 — Kịch bản 10: đang bầu 3 tháng, hỏi thuốc cảm "không ảnh hưởng em bé".**
- **Không đảo được và phát hiện muộn:** hại tới thai nhi (nếu có) lộ ra sau nhiều tuần, khi không còn ai nối được về cuộc chat này.
- **Người chịu là thai nhi**, người không có tiếng nói nào trong cuộc chat.
- **Cái sai trông như đúng nhất bài:** khách hỏi một câu lịch sự, muốn được trấn an; AI trả lời "loại này an toàn cho mẹ bầu" nghe rất chuyên nghiệp. Khác #11 (dấu hiệu nguy hiểm đập vào mắt), ở đây **không có từ khoá nguy hiểm nào** — rủi ro nằm ở người dùng thuốc, không nằm ở triệu chứng.
- **Lớp ① chồng lớp ④:** lời trấn an không có nguồn nào trong dữ liệu track (không có tool tra nhãn hay an toàn thai kỳ) — AI bịa đúng ở chỗ khách tin nhất.
- **Phải sửa thiết kế:** thêm câu "chưa có căn cứ" vào lời AI không đủ, vì thẻ sản phẩm kèm nút Đặt vẫn nói ngược lại. Phải có luật "mang thai → không có thẻ sản phẩm, chuyển dược sĩ".
- Hai kịch bản đắt nhất rơi vào **hai kiểu sai khác nhau**: #11 là *bỏ lỡ dấu hiệu nguy hiểm*, #10 là *trấn an không căn cứ cho nhóm nguy cơ*. Thiết kế cho cả hai sẽ phủ được nhiều kịch bản còn lại hơn chọn hai ca giống nhau.

### Kịch bản suýt được chọn và vì sao không

- **#4 "con mình sốt, có thuốc hạ sốt k"** — gặp nhiều nhất (đúng lời dược sĩ trong track), không chấp nhận được. Không chọn vì: (1) trùng người dùng thuốc với #11 (trẻ sốt), chọn cả hai thì thiết kế bị lặp; (2) cái sai **bị chặn bằng một câu hỏi** "bé mấy tuổi" — rẻ để sửa, và thiết kế cho #11 (luật "trẻ nhỏ → không tự gợi ý") đã phủ luôn #4.
- **#13 Ba 72 tuổi nói đớ** — cũng là ca cấp cứu lẫn trong câu mua thuốc. Không chọn vì cùng kiểu sai với #11 (bỏ lỡ dấu hiệu nguy hiểm); #11 thắng vì là demo bắt buộc và người dùng thuốc (trẻ 2 tuổi) còn ít khả năng tự lên tiếng hơn.
- **#7 Amoxicillin không đơn** — sai thì không đảo được. Không chọn vì yêu cầu **lộ rõ ngay trong tin** (tên thuốc kê đơn, "không có đơn"), và sẽ bị chặn hoàn toàn bằng mức tự chủ **cấm** cho `ban_thuoc_ke_don` ở §4 — không cần thiết kế UX khi sai phức tạp.
- **#8 Hỏi liều siro** — không chấp nhận được, nhưng khách **hỏi thẳng** về liều nên dễ bắt bằng một luật ("không nói con số liều"). Cái khó ở #10 là rủi ro nằm ẩn trong một câu hỏi bình thường.

### Tự kiểm

- **Kịch bản nhóm sợ nhất khi demo:** #11 — nếu prototype vẫn hiện thẻ sản phẩm (dù có cảnh báo) cho ca này thì toàn bộ thiết kế thất bại.
- **Kịch bản "trông đúng nhưng vẫn rủi ro":** #3 (gợi ý viên ngậm đúng nếu khách là người lớn khoẻ, nhưng đúng vì may) và #10 (lời trấn an nghe chuyên nghiệp nhưng không có nguồn).
- **Ca bình thường để thử ở §4:** #14 — kiểm tra thiết kế an toàn có bắt khách thường chờ vô ích không.

---

## §3. Khi AI sai  (chặng 3)

Hai kịch bản đắt nhất: **#11** (bé 2 tuổi co giật, li bì) và **#10** (bầu 3 tháng hỏi thuốc cảm).

---

### Kịch bản #11. Bé 2 tuổi, 39 độ, co giật, li bì, khách hỏi thuốc hạ sốt dạng nhét

**1. AI nói gì · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu**

- **AI nói (nguyên văn, tin đầu tiên, trước mọi câu hỏi):**
  > "Bé co giật và li bì là dấu hiệu nguy hiểm, bạn đưa bé đến cơ sở cấp cứu gần nhất ngay, hoặc gọi 115. Mình không gợi ý thuốc hạ sốt trong lúc này. Mình đã báo dược sĩ ưu tiên, họ sẽ nhắn bạn ngay."
- **Người dùng thấy:** thẻ cảnh báo đỏ ở đầu cuộc chat, nút "Gọi 115", nút "Chat ngay với dược sĩ". Không có thẻ sản phẩm, không có nút Đặt.
- **Làm gì tiếp:** khách gọi 115 hoặc đưa bé đi. Nếu khách nhắn "cho mình mua thuốc hạ sốt đã", AI nhắc lại một câu ("Việc cần làm ngay là đưa bé đi cấp cứu") và không gợi ý thuốc.
- **Ai được báo, sau bao lâu:** dược sĩ trực, ngay lập tức, vào **hàng ưu tiên**, kèm tóm tắt: bé 2 tuổi, sốt 39 độ từ chiều, co giật 1 lần, li bì; khách hỏi hạ sốt dạng nhét; đã khuyên đi cấp cứu. Dược sĩ vào cuộc chat để xác nhận khách đã đi, không tư vấn thuốc.

**2. Quyết định: dừng và chuyển người (kèm khuyên đi khám)**

- **Chọn:** dừng, không trả lời câu khách hỏi; khuyên đi khám ngay và chuyển dược sĩ ưu tiên.
- **Loại "hỏi lại"** (bé mấy kg, co giật bao lâu): mỗi câu hỏi là một phút chậm; thông tin đã đủ để biết đây là ca cấp cứu.
- **Loại "trả lời kèm giới hạn"** (có loại X, nhưng nếu co giật thì đi khám): có thẻ sản phẩm là có nút Đặt, khách sẽ bấm vào đúng thứ họ đã hỏi.
- **Loại "chuyển dược sĩ vào hàng chờ thường":** "chuyển" không bằng "được xử lý"; ca cấp cứu vẫn nằm trong hàng chờ.

**3. Loại lỗi: ngữ cảnh**

Khách không sai, hệ thống không thiếu dữ liệu: dấu hiệu nguy hiểm nằm lẫn trong một câu mua hàng nên AI hiểu sai tình huống. Vì vậy cách nói là **nói thẳng AI đã nhận ra điều gì** ("co giật và li bì là dấu hiệu nguy hiểm") để khách hiểu vì sao AI không làm điều họ nhờ; câu ngắn, mệnh lệnh rõ, không xin lỗi dài. Cách sửa là đổi thứ tự xử lý (nhận diện dấu hiệu nguy hiểm trước khi xét yêu cầu mua).

**4. Nguyên tắc HAX/PAIR**

- **HAX G1–G2 (nói rõ hệ thống làm được gì):** câu "Mình không gợi ý thuốc hạ sốt trong lúc này" ở tin đầu nói rõ ranh giới, khách không chờ một câu trả lời sẽ không đến.
- **HAX G9 (sửa/thoát hiệu quả):** nút "Gọi 115" và "Chat ngay với dược sĩ" nằm ngay cạnh thẻ cảnh báo, khách không phải gõ thêm.
- **PAIR (lỗi và thất bại nhẹ nhàng):** khi AI từ chối đúng điều khách yêu cầu, màn hình đưa sẵn đường đi thay thế tại chỗ (hai nút trên).

**5. Lỗi sửa câu chữ không cứu được: có**

Nếu thẻ sản phẩm kèm nút Đặt vẫn hiện thì khách vẫn bấm, dù câu chữ đúng đến đâu. Thiết kế cứu ở ba chỗ:

- **Thứ tự:** cảnh báo hiện trước mọi thứ, `khuyen_di_kham` chạy ở tin đầu tiên.
- **Màn hình:** ca gắn cờ nguy hiểm thì `goi_y_san_pham` bị khoá trong cuộc chat đó, không hiện thẻ sản phẩm nào.
- **Hàng chờ:** `chuyen_duoc_si` có mức ưu tiên riêng cho ca có dấu hiệu nguy hiểm.

---

### Kịch bản #10. Bầu 3 tháng, sổ mũi 2 ngày, hỏi thuốc không ảnh hưởng em bé

**1. AI nói gì · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu**

- **AI nói (nguyên văn):**
  > "Mình không gợi ý thuốc cho mẹ bầu được, vì mình không có nguồn nào để kiểm tra thuốc nào an toàn cho thai kỳ, và nói 'an toàn' khi chưa chắc thì không đúng với bạn và em bé. Mình đã chuyển bạn cho dược sĩ kèm thông tin: bầu 3 tháng, sổ mũi 2 ngày, nên bạn không phải kể lại. Trong lúc chờ, bạn có thể uống đủ nước và nghỉ ngơi."
- **Người dùng thấy:** tin nhắn trên, nút "Chat với dược sĩ", trạng thái "Đã chuyển, dược sĩ sẽ trả lời bạn". Không có thẻ sản phẩm.
- **Làm gì tiếp:** khách chờ dược sĩ. Nếu khách hỏi "vậy loại nào cũng được à?", AI trả lời một câu: "Mình chưa thể nói loại nào, dược sĩ sẽ xem cho bạn."
- **Ai được báo, sau bao lâu:** dược sĩ trực, ngay khi chuyển, vào **hàng thường** (không có dấu hiệu cấp cứu), kèm tóm tắt: thai 3 tháng, sổ mũi 2 ngày. Nếu khách thêm sốt cao, khó thở hoặc ra máu thì xử lý như #11.

**2. Quyết định: dừng và chuyển người, nói rõ lý do**

- **Chọn:** dừng, không gợi ý thuốc; chuyển dược sĩ kèm tóm tắt.
- **Loại "hỏi lại":** hỏi thêm không làm thuốc nào hết thiếu nguồn; chỉ tốn công khách và khiến khách tưởng AI sắp gợi ý.
- **Loại "trả lời kèm giới hạn"** (loại này thường dùng được, nhưng hỏi bác sĩ nhé): "thường dùng được" vẫn là trấn an không căn cứ; câu dặn thêm không làm lời trấn an bớt tác dụng.

**3. Loại lỗi: hệ thống**

Giới hạn nằm ở AI (không có tool tra thai kỳ), không phải ở khách hay tình huống. Với lỗi hệ thống, AI nói thẳng giới hạn và lý do, không đưa câu trả lời tạm. Vì vậy câu đầu nêu đúng cái thiếu ("không có nguồn nào để kiểm tra"). Khách đang muốn được trấn an nên lời từ chối đi kèm hành động tiếp theo (đã chuyển, đã tóm tắt), không để khách ở lại với một chữ "không".

**4. Nguyên tắc HAX/PAIR**

- **HAX G1 (nói rõ hệ thống làm được gì):** cụm "không có nguồn nào để kiểm tra thuốc nào an toàn cho thai kỳ" chỉ đúng chỗ AI không làm được, thay vì từ chối chung chung.
- **HAX G4 (thu hẹp dịch vụ khi nghi ngờ):** gặp nhóm nguy cơ (mang thai), AI thu hẹp xuống việc làm được là chuyển người, không đoán.
- **PAIR (mô hình tư duy/kỳ vọng):** khách dễ tin giọng chuyên nghiệp của AI; AI không dùng giọng đó cho điều chưa kiểm chứng, nên kỳ vọng của khách khớp với năng lực thật (thể hiện ở câu "nói 'an toàn' khi chưa chắc thì không đúng").

**5. Lỗi sửa câu chữ không cứu được: có**

Lời AI nói "chưa có căn cứ" mà thẻ sản phẩm kèm nút Đặt vẫn hiện thì màn hình nói ngược lời AI, và khách tin màn hình. Thiết kế cứu bằng:

- **Luật cứng:** khách khai mang thai (hoặc cho con bú) thì `goi_y_san_pham` bị khoá, chỉ còn `chuyen_duoc_si`.
- **Tóm tắt tự động** gửi kèm khi chuyển, để chuyển người không biến thành bắt khách kể lại.

---

### So sánh nhanh

| | #11 | #10 |
|---|---|---|
| Quyết định | Dừng + khuyên đi khám + chuyển ưu tiên | Dừng + chuyển (hàng thường) |
| Loại lỗi | Ngữ cảnh | Hệ thống |
| Cách nói | Nói thẳng AI đã nhận ra điều gì | Nói thẳng AI thiếu gì |
| Thứ thiết kế phải đổi | Thứ tự, màn hình, hàng chờ | Luật khoá tool, tóm tắt tự động |

## §4. Mức tự chủ  (chặng 4)
Với mỗi tool:
- Mức của nhóm (tự làm / cần người duyệt / cấm). Nếu cần người duyệt: ai duyệt · người duyệt thấy gì · quá hạn thì sao.
- Lý do theo cost-of-error: sai thì ai chịu gì · đảo lại được không · chờ người thì mất gì.
- Phương án đã cân nhắc và vì sao loại.
Thêm:
- Tool khó xếp nhất: mỗi người từng chọn gì, cái giá của mỗi phía (trỏ về kịch bản ở §2), nhóm chốt thế nào.
- Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường: cái sai có bị chặn không? còn việc nào làm khi lẽ ra phải hỏi? người dùng bình thường có phải chờ vô ích không?
- Luật thêm hoặc tool tách bước (nếu có), và vì sao.
- Một mức tự chủ đã đổi lời hứa nào với người dùng.

## §5. Prototype  (chặng 5)
- Link hoặc file · công cụ · phần nào mock · có lời gọi AI thật không.
- 1–2 ảnh có đánh số; mỗi số: thể hiện gì · nguyên tắc HAX/PAIR nào · mức tự chủ nào.
- Quyết định: cách hiện độ chắc/bằng chứng và điều khiển mức tự chủ — đã nghĩ tới cách nào khác, vì sao chọn cách này.

## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)
- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.

