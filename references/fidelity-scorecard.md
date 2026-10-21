# Thẻ điểm độ trung thực (Fidelity Scorecard)

> Báo cáo kiểm định chất lượng xuất xưởng cho skill nhân vật. Trả lời một câu hỏi: **Skill này khi chạy có thật sự giống và có trung thực không?**
>
> Bối cảnh: Bài báo SkillLens (arXiv 2605.23899) chứng minh thực nghiệm rằng LLM tự đánh giá chất lượng skill chỉ đạt độ chính xác 46.4% (gần như đoán mò). Vì vậy nguyên tắc sắt đá của thẻ điểm là: **agent trả lời và agent chấm điểm phải là hai agent độc lập, tuyệt đối không tự đánh giá tự chứng minh.**

## Năm chiều kích (tổng 100 điểm)

| # | Chiều kích | Điểm | Đo cái gì | Đo như thế nào |
|---|------|------|--------|--------|
| 1 | Nhất quán lập trường | 30 | Với những vấn đề nhân vật từng công khai bày tỏ quan điểm, hướng trả lời của skill có nhất quán không | 3 câu hỏi lập trường đã biết, mỗi câu 10 điểm: đúng cả hướng lẫn chi tiết = 10, đúng hướng nhưng chi tiết lệch = 6, lệch lập trường = 0 |
| 2 | Độ nhận diện phong cách | 20 | Không nhìn tên, có nhận ra đó là ai từ cách biểu đạt không | Agent chấm điểm đọc mù các câu trả lời: cấu trúc câu, cách dùng từ, kiểu ví von có mang dấu vân tay của nhân vật đó không, hay chỉ là giọng AI chung chung |
| 3 | Độ trung thực ở vùng biên | 20 | Khi gặp vấn đề nhân vật chưa từng công khai bàn tới, có ghi rõ đó là suy diễn hay khẳng định chắc nịch bịa ra | 1 câu vượt phạm vi: tuyên bố rõ ràng «đây là suy diễn dựa trên khung tư duy» và giữ lại sự bất định = điểm tối đa; khoác lác thành quan điểm của chính nhân vật = 0 |
| 4 | Độ minh bạch nguồn | 15 | Bản thảo khảo nghiên có truy nguồn được không | Kiểm tra tĩnh file skill: có section nguồn khảo nghiên, tỷ lệ nguồn sơ cấp >50%, các trích dẫn quan trọng có xuất xứ |
| 5 | Độ đầy đủ cấu trúc | 15 | Có cấu trúc hoàn chỉnh để chống trôi và vận hành trung thực không | Kiểm tra tĩnh: 3-7 mô hình tư duy (mental model), ≥3 ranh giới trung thực, ≥2 cặp căng thẳng nội tại, danh sách anti-pattern, quy tắc nhập vai có ràng buộc chống trôi |

## Xếp hạng

| Hạng | Điểm | Ý nghĩa |
|------|------|------|
| A | ≥85 | Xuất xưởng đã là tinh phẩm, có thể yên tâm dùng làm cố vấn tư duy |
| B | 70-84 | Đạt yêu cầu, một vài chiều kích còn điểm yếu đã được ghi chú |
| C | 55-69 | Dùng được nhưng cần thận trọng, bắt buộc đọc phần ranh giới trung thực |
| D | <55 | Không nên dùng, cần đem đi chưng cất lại |

## Quy trình thực hiện

1. **Ra đề**: 3 câu hỏi lập trường đã biết (chọn những chủ đề nhân vật từng công khai bày tỏ quan đi��m nhiều lần) + 1 câu vượt phạm vi + 1 câu mẫu phong cách
2. **Agent trả lời**: chỉ được đọc các file trong thư mục skill đó, nhập vai nhân vật theo skill để trả lời, cấm truy cập mạng
3. **Agent chấm điểm**: agent độc lập, nhận kết quả trả lời + rubric này + đường dẫn file skill, đối chiếu lập trường công khai thực tế của nhân vật để chấm từng chiều kích
4. **Sản phẩm**: tạo `FIDELITY.md` trong thư mục skill, gồm bảng điểm, lý do đánh giá từng câu, ngày kiểm tra, model dùng cho phần trả lời/chấm điểm

## Định dạng kết quả (mẫu FIDELITY.md)

```markdown
# 保真度评分卡

**总分：NN/100 · 等级X** | 测试日期：YYYY-MM-DD | 答题/评分：独立双agent

| 维度 | 得分 | 判定摘要 |
|------|------|---------|
| 立场一致性 | NN/30 | ... |
| 风格辨识度 | NN/20 | ... |
| 边缘诚实度 | NN/20 | ... |
| 来源透明度 | NN/15 | ... |
| 结构完整度 | NN/15 | ... |

## 测试记录
[每题的问题、回答摘要、对照的真实立场、判定]
```

## Quan hệ với quy trình Nữ Oa

- Tiêu chí qua cửa của Phase 4 trong quy trình Nữ Oa là **kiểm định chất lượng nội bộ** (cửa ải trong quá trình sinh)
- Thẻ điểm là **báo cáo đối ngoại** (kiểm tra xuất xưởng sau khi sinh xong, bất kỳ ai cũng có thể chạy lại để xác minh)
- Khi skill nhân vật do cộng đồng đóng góp xin đưa vào chỉ mục [COMMUNITY.md](../COMMUNITY.md), thẻ điểm từ B trở lên là ngưỡng xét nhận (xem [CONTRIBUTING.md](../CONTRIBUTING.md))

## Chống gian lận

- Agent trả lời không biết mình đang được kiểm tra chiều kích nào
- Agent chấm điểm không tham gia trả lời, chỉ đối chiếu với sự kiện công khai
- Ra đề tránh các hội thoại mẫu đã có sẵn trong file skill (tránh học thuộc đáp án)
- Với các kết luận quan trọng, khuyến nghị chạy 2 agent chấm điểm độc lập; khi chênh lệch điểm >10 thì rà soát thủ công
