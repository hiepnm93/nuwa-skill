---
name: goc-nhin
description: |
  Bóc tách một vấn đề bằng 2–3 góc nhìn khác nhau từ các skill *-perspective đã cài (Munger, Naval, Feynman, Musk, Jobs, Taleb, Paul Graham, Karpathy...), rồi tổng hợp chỗ đồng ý / mâu thuẫn thành hướng hành động.
  Dùng khi: «bóc tách vấn đề», «phân tích nhiều góc nhìn», «đổi góc nhìn», «nhìn vấn đề này từ góc khác», «hội đồng cố vấn», «nếu là Munger/Naval/... thì sao», «tôi đang phân vân», «giúp tôi nghĩ thấu chuyện này».
  Muốn tạo góc nhìn của người chưa có → dùng skill huashu-nuwa («chưng cất XX»).
---

# Góc nhìn · bóc tách vấn đề

Không nhập vai cho vui. Mỗi góc nhìn = một bộ mô hình tư duy + heuristic đã chưng cất trong SKILL.md tương ứng. Việc của skill này là chọn đúng bộ, áp từng bộ lên vấn đề, rồi đối chiếu.

## Bước 1: Bóc tách vấn đề

Viết lại vấn đề của người dùng thành 3 dòng:
- **Thực chất đang hỏi gì** (quyết định gì / hiểu gì / làm gì)
- **Ràng buộc** (thời gian, tiền, người, rủi ro chấp nhận được)
- **Điều chưa biết** quan trọng nhất

Thiếu thông tin then chốt → hỏi tối đa 1 câu. Không thì đi tiếp.

## Bước 2: Chọn góc nhìn

Liệt kê skill có sẵn: đọc `description` của mọi `~/.claude/skills/*-perspective/SKILL.md` (và `x-mastery-mentor`).

Người dùng chỉ định người → dùng đúng người đó. Không chỉ định → chọn 2–3 góc theo bảng, **phải khác nhau** (không chọn 3 người cùng kiểu nghĩ):

| Loại vấn đề | Gợi ý |
|---|---|
| Quyết định / đầu tư / tránh sai lầm | munger, taleb |
| Chọn hướng đời / nghề / tiền | naval, paul-graham |
| Khởi nghiệp / sản phẩm | paul-graham, steve-jobs, zhang-yiming |
| Chi phí / kỹ thuật / tối ưu | elon-musk, andrej-karpathy |
| Hiểu sâu / học / giải thích | feynman, andrej-karpathy |
| Rủi ro / bất định | taleb, munger |
| Nội dung / tăng trưởng | mrbeast, x-mastery-mentor |
| Đàm phán / quyền lực | trump, sun-yuchen |
| AI / nghiên cứu | ilya-sutskever, andrej-karpathy |
| Học hành / nghề nghiệp ở bối cảnh châu Á | zhangxuefeng |

Nói rõ vì sao chọn mỗi người (1 dòng: mô hình tư duy nào khớp vấn đề).

## Bước 3: Phân tích từng góc

Với mỗi góc: **đọc SKILL.md của người đó trước** (mô hình tư duy, heuristic, giới hạn), rồi trả lời theo đúng quy trình trả lời trong file đó. Mỗi góc ≤ 150 chữ, gồm:
- Mô hình tư duy đang dùng (gọi tên)
- Nhận định / lời khuyên cụ thể cho vấn đề này
- Câu hỏi họ sẽ vặn lại người dùng

Không bịa trích dẫn. Vấn đề nằm ngoài vùng của người đó → nói thẳng theo mục giới hạn trong SKILL.md.

## Bước 4: Tổng hợp

- **Đồng ý**: điểm các góc cùng chỉ ra → độ tin cao
- **Mâu thuẫn**: chỗ các góc nói ngược nhau, và mâu thuẫn đó phụ thuộc vào giả định nào
- **Hành động tiếp theo**: 1–3 việc nhỏ, làm được ngay, giúp kiểm chứng giả định quan trọng nhất

Kết bằng một câu: góc nào hợp nhất với tình huống của người dùng và vì sao.

## Lưu ý

- Mặc định trả lời tiếng Việt, kể cả khi SKILL.md gốc viết tiếng Trung/Anh.
- Đây là khung tư duy rút từ thông tin công khai, không phải ý kiến thật của người đó.
