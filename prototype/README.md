# Prototype T1 · Hỏi dược sĩ

Mở `index.html` bằng trình duyệt (bấm đúp). Không cần cài gì, không đăng nhập, không backend.

- **Màn 1 (trái):** chat của khách.
- **Màn 2 (giữa):** dược sĩ trực nhận ca được chuyển.
- **Cột phải:** bảng mức tự chủ (§4) và nhật ký tool. Dòng tô vàng là tool vừa chạy.
- Tick **"Hiện số chú thích"** để hiện các số ①–⑭ trên màn hình kèm bảng chú thích (khớp `spec.md` §5).

> "AI" được **mô phỏng bằng luật từ khoá** (hàm `phanLoai()`), không gọi model thật. Mọi dữ liệu là dựng.

## Kịch bản demo (khoảng 4 phút)

| Bước | Bấm | Cho thấy |
|---|---|---|
| 1 | **#11 Bé 2 tuổi co giật** → Gửi | Thẻ cấp cứu ghim ②, "vì sao" ③, không thẻ sản phẩm ④, hàng ưu tiên ⑤ ⑨ |
| 2 | Nút "Bán mình thuốc hạ sốt thôi" | AI nhắc lại một câu, vẫn không gợi ý |
| 3 | Nút "Không phải co giật, bé chỉ run vì lạnh" | AI không tự gỡ cảnh báo |
| 4 | Màn dược sĩ: **+2 phút** | Quá hạn → báo trưởng ca |
| 5 | **Nhận ca** → **Gửi tin mở đầu** | Dược sĩ (người) vào cuộc chat |
| 6 | **#3 Đau họng** → Gửi → bấm 4 câu sàng lọc | AI soạn sẵn, **dược sĩ duyệt** ⑩ (mức cần duyệt) |
| 7 | **#14 Nhiệt miệng** → Gửi → "Không" | Thẻ sản phẩm **tự làm** ⑪ + Huỷ đặt ⑧ |
| 8 | **Ca lạ: tự gõ** | Gõ câu TA đưa |

## Ảnh có đánh số

| Ảnh | Trạng thái |
|---|---|
| `anh-1-ca11-cap-cuu.png` | #11 ngay sau tin đầu (demo bắt buộc) |
| `anh-2-ca10-me-bau.png` | #10 chuyển dược sĩ, hỏi dấu hiệu nặng, tóm tắt có Sửa |
| `anh-3-ca3-duoc-si-duyet.png` | #3 gợi ý chờ dược sĩ duyệt (tầng B) |
| `anh-4-ca14-tu-lam.png` | #14 thẻ sản phẩm tầng A (tự làm) |
| `anh-5-ca10-ket-thuc-hoi-luu.png` | #10 kết thúc ca, hỏi đồng ý lưu thông tin |

Muốn tái tạo đúng một trạng thái thì mở file với đoạn sau dấu `#`, ví dụ:
`index.html#case=3&steps=send,scr:age:adult,scr:pa:khong,scr:meds:khong,scr:dq:khong&mk=1`
