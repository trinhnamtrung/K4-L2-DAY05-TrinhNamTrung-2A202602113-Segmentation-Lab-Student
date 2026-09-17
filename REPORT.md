# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602113 (MSSV — chưa rõ có mã lớp cấp riêng dạng D5_xxx hay không, xem mục 4)
- Ngày / CVAT local: 17/09/2026, CVAT local (http://localhost:8080)
- Công cụ đã dùng: CVAT Brush + Polygon (vẽ tay); Automatic Annotation bằng model tự tích hợp riêng (EoMT-DINOv3, custom Nuclio) làm gợi ý cho vật còn lại, tự kiểm và sửa tay sau đó

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: ảnh `000000181542.jpg`, người phụ nữ mặc áo dài đứng hơi lệch trái so với trung tâm ảnh (object PERSON 18, MANUAL).
- Class và quy tắc tôi dùng để chọn biên: `person`. Chỉ tô phần cơ thể nhìn thấy được; phần bị vật khác che thì dừng lại, không đoán vẽ tiếp phần bị che.
- Nếu dùng gợi ý sau đó: có chạy Automatic Annotation cho các vật còn lại. Phát hiện và sửa: xe ở ảnh `000000458325.jpg` bị gợi ý gộp hai xe cạnh nhau thành một mask (đã tách lại thành hai object riêng); một số người bị bỏ sót chưa được gán nhãn (đã vẽ bổ sung); nhiều mask có lỗ hổng nhỏ bên trong/rìa (đã dùng Brush chế độ Add tô lấp cho khít biên).

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `medium_instance`, ảnh `000000458325.jpg`, khu vực hai xe hơi đậu sát nhau.
- Lỗi thuộc loại: gộp-tách (Automatic Annotation gộp hai xe khác nhau thành một object/mask duy nhất).
- Bằng chứng tôi nhìn thấy: so đối tượng trong panel Objects với ảnh thật, thấy một mask `car` trải dài phủ lên cả hai thân xe cạnh nhau thay vì mỗi xe một mask riêng.
- Quy tắc và hành động sửa: theo phiếu quy tắc "hai vật cùng lớp sát nhau vẫn là hai instance" — xoá mask gộp, vẽ lại thành hai mask `car` riêng biệt, mỗi mask khớp đúng ranh một xe.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại `medium_instance.zip` (COCO 1.0) trước khi đưa vào `submissions/`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): … / chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `easy_semantic`, ảnh có đồi cỏ khô ở nền xa (`7ee6d192-89e2408b.jpg`) | Đồi cỏ khô có tính là `vegetation` không, hay để trống vì không chắc là cỏ/cây | Đề bài tự nhận đây là ca chưa có tài liệu nào quyết; 5 class của Easy không có lớp "terrain" riêng | Câu hỏi cho coach: nên xử lý vùng đồi cỏ khô kiểu này thế nào cho các ảnh tương tự sau này? |
| `cp1_holes`, khe/lỗ trên xe (kính, gương, khe hở) | Khoét mask theo đúng hình lỗ nhìn thấy, hay lấp đầy thành khối liền không có lỗ | `guideline-mini-sheet.md` + rubric cảnh báo lỗi "khoét lỗ tùy tiện khiến vật bị rỗng" | Quyết định: lấp đầy khoảng trống, không khoét lỗ, theo đúng cảnh báo của rubric |
| `cp4_curb`, đoạn ranh road–sidewalk lẫn với lối rẽ vào nhà | Đoạn lối rẽ đổ nhựa giống đường lớn — tính là `road` (vì giống mặt đường) hay `sidewalk` (vì theo chức năng thực tế) | Guideline: "ranh road–sidewalk theo chức năng/bó vỉa, không chỉ theo màu"; kiểm tra thực tế đoạn này không đủ rộng cho ô tô chạy vào | Quyết định: tô `sidewalk`, vì xe không vào được nên đúng chức năng là lối đi bộ, dù bề mặt trông giống đường lớn |
