# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603302
- Ngày / CVAT local: 12/11/2026
- Công cụ đã dùng: CVAT 

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| `easy_semantic` | `easy_semantic.zip` | 3 / 3 | 20 |
| `medium_instance` | `medium_instance.zip` | 3 / 3 | 32 |
| `hard_panoptic` | `hard_panoptic.zip` | 2 / 2 | 30 |
| `cp1_holes` | `cp1_holes.zip` | 0 / 1 | 3 |
| `cp2_slice` | `cp2_slice.zip` | 0 / 1 | 3 |
| `cp5_occlusion` | `cp5_occlusion.zip` | 0 / 1 | 3 |
| `cp3_thin` | `cp3_thin.zip` | 0 / 1 | 3 |
| `cp4_curb` | `cp4_curb.zip` | 0 / 1 | 3 |
| `cp6_coverage` | `cp6_coverage.zip` | 0 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh đầu tiên trong thư mục medium_instance, tại vùng giữa ảnh, vẽ người đàn ông vs nhãn person
- Class và quy tắc tôi dùng để chọn biên: Ví dụ với class car, xác định đường biên theo phần thân xe quan sát được, vẽ polygon sát viền xe, không lấy phần bóng đổ hoặc background xung quanh. Với những phần bị che khuất, tôi chỉ vẽ theo vùng thực sự nhìn thấy, không tự suy đoán phần bị che
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: không dùng, tự xác định và vẽ mask dựa trên ảnh gốc. Ví dụ, với class car, chỉ chọn vùng thân xe nhìn thấy được, không gán phần bóng đổ hoặc vùng đường nằm sát xe thành class car
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

- **Task/ảnh/vùng:** Task 4, ảnh trong tập `medium_instance`, vùng xe ô tô ở khu vực giữa ảnh.
- **Lỗi thuộc loại:** Biên và phủ vùng.
- **Bằng chứng tôi nhìn thấy:** Khi kiểm tra annotation ở mức zoom lớn, đường biên polygon chưa bám sát thân xe, một số điểm còn lấy thừa vùng background xung quanh.
- **Quy tắc và hành động sửa:** Dựa theo guideline, tôi chỉnh lại các điểm polygon để đường biên sát phần thân xe quan sát được, loại bỏ background thừa và không vẽ phần bị che khuất.
- **Sau sửa đã Save và export lại chưa?** Chưa xác nhận export lại.

**Summary tự đánh giá trên GitHub Actions:** Chưa có điểm.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
|---|---|---|---|
| Ảnh 1 – vùng người ngồi trên xe máy | `person` hoặc `rider` | Rider là người đang điều khiển hoặc ngồi trên phương tiện. | Chọn `rider` nếu xác định được người đang điều khiển xe. |
| Ảnh 2 – vùng xe tải ở phía xa | `car` hoặc `truck` | Dựa vào hình dáng và đặc điểm phương tiện thực tế. | Nếu không đủ bằng chứng để phân biệt, chuyển coach review. |
| Ảnh 3 – vùng cây và mặt đất bên đường | `vegetation` hoặc `terrain` | Vegetation là cây, bụi cây, tán lá; terrain là bề mặt địa hình tự nhiên như đất, cỏ thấp. | Chọn class theo vùng quan sát được, không gộp hai vùng. |

**Kết quả tự đánh giá:**
- Summary GitHub Actions: Chưa có điểm.
- Scorecard: Chưa có kết quả xác nhận.
- Các trường hợp chưa rõ sẽ được đưa ra trao đổi với coach trước khi chốt.
