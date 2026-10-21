<div align="center">

# 女娲.skill (Nữ Oa)

> *"Người tiếp theo bạn muốn chưng cất không nhất thiết phải là đồng nghiệp."*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-Standard-green)](https://agentskills.io)
[![skills.sh](https://img.shields.io/badge/skills.sh-Compatible-blue)](https://skills.sh)
[![Multi-Runtime](https://img.shields.io/badge/Runtime-Claude%20Code%20·%20Codex%20·%20Cursor%20·%20OpenClaw%20·%20Hermes-blueviolet)](#cài-đặt)

<br>

**Nữ Oa chưng cất cách nghĩ của bất kỳ ai, để Musk, Naval, Munger, Feynman làm việc cho bạn.**

<sub>Xây trên chuẩn mở [Agent Skills](https://agentskills.io). Chạy được trên Claude Code, Codex, Cursor, OpenClaw, Hermes Agent, CodeBuddy, Workbuddy, Gemini CLI, OpenCode và hơn 50 runtime hỗ trợ skill.</sub>

<br>

[colleague-skill](https://github.com/titanwings/colleague-skill) đã chứng minh việc chưng cất một người thành AI skill là làm được.
Vậy sao chỉ dừng ở đồng nghiệp? Hãy chưng cất Munger, Feynman, Musk.
Chỉ cần nhập một cái tên, Nữ Oa tự lo phần nghiên cứu, trích xuất và kiểm chứng.

[Ví dụ](#ví-dụ) · [Cài đặt](#cài-đặt) · [Nữ Oa chưng cất gì](#nữ-oa-chưng-cất-gì) · [Cách hoạt động](#cách-hoạt-động)

<br>

**Ngôn ngữ khác:**

[中文](README.md) · [English](README_EN.md) · [日本語](README_JA.md) · [한국어](README_KO.md) · [Español](README_ES.md)

</div>

---

## Ví dụ

```
Bạn     ❯ Tôi muốn làm nội dung, viết sách, và làm một app độc lập,
           nhưng lúc nào cũng thiếu năng lượng.

Naval   ❯ Bạn vừa liệt kê ba mong muốn. Mỗi mong muốn là một hợp đồng
           bạn ký với sự không vui. Vấn đề không phải năng lượng, mà là ký quá nhiều hợp đồng.

           Tự hỏi: việc nào khiến bạn quên cả thời gian?
           Đó là chỗ kiến thức đặc thù của bạn nằm.

           Không phải chọn một cái mãi mãi. Chỉ là làm một cái trước, rồi cái khác, rồi cái khác.
           Cộng dồn nối tiếp, không phải kiệt sức song song.
```

```
Bạn     ❯ Chi phí kéo khách của SaaS chúng tôi quá cao.

Musk    ❯ Khoan nghĩ cách giảm. Tính giới hạn vật lý tối thiểu trước đã.
           Hành động tối thiểu cần có để có một khách hàng là gì?
           Về lý thuyết, đường ngắn nhất từ lúc họ biết bạn đến lúc trả tiền là gì?

           Đường thực tế của bạn dài gấp mấy lần đường lý thuyết?
           Nếu hơn 3 lần, có những bước bỏ được.
           Đừng tối ưu phễu, hãy hỏi xem phễu có nên tồn tại không.
```

Đây không phải nhập vai. Naval dùng mô hình tư duy "mong muốn là hợp đồng". Musk dùng lập luận "giới hạn tiệm cận". **Họ không trích dẫn câu nói, mà phân tích vấn đề của bạn bằng khung nhận thức của chính những bộ óc đó.**

---

## Cài đặt

Nữ Oa xây trên chuẩn mở [Agent Skills](https://agentskills.io), chạy được trong mọi runtime agent hỗ trợ skill.

### Cách 1: Một dòng (khuyên dùng, đa runtime)

Mở agent có hỗ trợ skill (Claude Code, Codex, Cursor, OpenClaw, Hermes, CodeBuddy, Workbuddy, Gemini CLI, OpenCode và hơn 50 cái khác) rồi bảo nó:

```
Cài skill này cho tôi: https://github.com/alchaincyf/nuwa-skill
```

Hoặc dùng trình cài đặt CLI chung ([vercel-labs/skills](https://github.com/vercel-labs/skills), hỗ trợ hơn 55 runtime):

```bash
npx skills add alchaincyf/nuwa-skill
```

Nó tự nhận ra runtime và đặt skill vào đúng thư mục. Thêm `-a claude-code` / `-a codex` / `-a cursor` / `-a openclaw` để chọn runtime cụ thể.

### Cách 2: Cài tay

<details>
<summary>Thư mục skills của từng runtime</summary>

| Runtime | Đường dẫn |
|---|---|
| Claude Code | `~/.claude/skills/nuwa-skill/` |
| Codex CLI | `~/.codex/skills/nuwa-skill/` |
| Cursor | `~/.cursor/skills/nuwa-skill/` |
| OpenClaw | `~/.openclaw/workspace/skills/nuwa-skill/` |
| Hermes Agent | chạy `tools/install_hermes_skill.py` |
| Runtime khác | clone vào thư mục `skills/` của runtime đó |

```bash
git clone https://github.com/alchaincyf/nuwa-skill <đường-dẫn-ở-trên>
```

</details>

### Cách 3: Dùng làm tài liệu tham khảo (không cần runtime)

Kể cả không có runtime hỗ trợ skill, bạn vẫn có thể dán bất kỳ `SKILL.md` nào vào prompt. Nữ Oa chỉ là markdown + YAML frontmatter.

---

### Cách dùng

Cài xong, nói với agent:

```
> Chưng cất Paul Graham
> Làm skill góc nhìn của Trương Tiểu Long
> Tạo cho tôi skill Đoàn Vĩnh Bình
```

Tạo xong thì gọi thẳng:

```
> Dùng góc nhìn của Munger phân tích quyết định đầu tư này
> Feynman sẽ giải thích máy tính lượng tử thế nào?
> Chuyển sang Naval, tôi đang phân vân giữa ba việc
```

---

## Nữ Oa chưng cất gì

Muốn chưng cất những bộ óc giỏi nhất của một lĩnh vực thì phải lấy thứ sâu hơn thói quen làm việc hằng ngày. Nữ Oa trích xuất các tầng sau:

| Tầng | Mô tả |
|---|---|
| **Cách họ nói** | DNA biểu đạt: giọng, nhịp, từ ưa dùng |
| **Cách họ nghĩ** | Mô hình tư duy, khung nhận thức |
| **Cách họ phán đoán** | Heuristic ra quyết định |
| **Điều họ không làm** | Phản mẫu, giá trị nền |
| **Giới hạn thật** | Những gì skill thực sự không làm được |

Thói quen làm việc có thể truyền qua tài liệu quy trình. Nhưng thứ khiến Munger và Musk ra kết luận khác nhau trước cùng một vấn đề là khung nhận thức của họ. Nữ Oa trích xuất hệ điều hành nhận thức đó.

### Giới hạn thật

Mỗi skill đều nói rõ nó không làm được gì:

- Không chưng cất được trực giác: khung thì trích được, cảm hứng thì không
- Không bắt được sự thay đổi: chỉ là ảnh chụp đến thời điểm dừng nghiên cứu
- Phát ngôn công khai ≠ niềm tin thật: chỉ dựa trên thông tin công khai

**Một skill không nói ra giới hạn của mình thì không đáng tin.**

---

## Những người đã được chưng cất

Nữ Oa đã chưng cất 14 người + 1 chủ đề. Mỗi cái là một skill độc lập, cài được ngay, theo chuẩn Agent Skills, chạy trên Claude Code / Codex / Cursor / OpenClaw / Hermes và các runtime khác:

### Skill nhân vật

| Nhân vật | Lĩnh vực | Repo riêng | Cài một dòng (đa runtime) |
|------|------|---------|---------|
| 🔥 **Paul Graham** | Khởi nghiệp / viết / sản phẩm / triết lý sống | [paul-graham-skill](https://github.com/alchaincyf/paul-graham-skill) | `npx skills add alchaincyf/paul-graham-skill` |
| 🔥 **Trương Nhất Minh** | Sản phẩm / tổ chức / toàn cầu hóa / nhân tài | [zhang-yiming-skill](https://github.com/alchaincyf/zhang-yiming-skill) | `npx skills add alchaincyf/zhang-yiming-skill` |
| 🔥 **Karpathy** | AI / kỹ thuật / giáo dục / mã nguồn mở | [karpathy-skill](https://github.com/alchaincyf/karpathy-skill) | `npx skills add alchaincyf/karpathy-skill` |
| 🔥 **Ilya Sutskever** | An toàn AI / scaling / gu nghiên cứu | [ilya-sutskever-skill](https://github.com/alchaincyf/ilya-sutskever-skill) | `npx skills add alchaincyf/ilya-sutskever-skill` |
| 🔥 **MrBeast** | Làm nội dung / phương pháp YouTube | [mrbeast-skill](https://github.com/alchaincyf/mrbeast-skill) | `npx skills add alchaincyf/mrbeast-skill` |
| 🔥 **Trump** | Đàm phán / quyền lực / truyền thông / dự đoán hành vi | [trump-skill](https://github.com/alchaincyf/trump-skill) | `npx skills add alchaincyf/trump-skill` |
| ⭐ **Steve Jobs** | Sản phẩm / thiết kế / chiến lược | [steve-jobs-skill](https://github.com/alchaincyf/steve-jobs-skill) | `npx skills add alchaincyf/steve-jobs-skill` |
| **Elon Musk** | Kỹ thuật / chi phí / nguyên lý gốc | [elon-musk-skill](https://github.com/alchaincyf/elon-musk-skill) | `npx skills add alchaincyf/elon-musk-skill` |
| **Munger** | Đầu tư / mạng lưới mô hình / tư duy ngược | [munger-skill](https://github.com/alchaincyf/munger-skill) | `npx skills add alchaincyf/munger-skill` |
| **Feynman** | Học / dạy / tư duy khoa học | [feynman-skill](https://github.com/alchaincyf/feynman-skill) | `npx skills add alchaincyf/feynman-skill` |
| **Naval** | Tài sản / đòn bẩy / triết lý sống | [naval-skill](https://github.com/alchaincyf/naval-skill) | `npx skills add alchaincyf/naval-skill` |
| **Taleb** | Rủi ro / phản mong manh / bất định | [taleb-skill](https://github.com/alchaincyf/taleb-skill) | `npx skills add alchaincyf/taleb-skill` |
| **Trương Tuyết Phong** | Chọn hướng học / định hướng nghề / dịch chuyển giai tầng | [zhangxuefeng-skill](https://github.com/alchaincyf/zhangxuefeng-skill) | `npx skills add alchaincyf/zhangxuefeng-skill` |
| **Tôn Vũ Thần** | Marketing / kinh tế chú ý / kiểm soát câu chuyện | [examples/ trong repo này](examples/sun-yuchen-perspective/) | chép `examples/sun-yuchen-perspective/` vào thư mục skills |

### Skill chủ đề

| Chủ đề | Lĩnh vực | Repo riêng | Cài một dòng (đa runtime) |
|------|------|---------|---------|
| **X Mentor** | Phát triển X/Twitter toàn diện | [x-mentor-skill](https://github.com/alchaincyf/x-mentor-skill) | `npx skills add alchaincyf/x-mentor-skill` |

Skill nhân vật chưng cất cách một bộ óc suy nghĩ; skill chủ đề chưng cất phương pháp của một lĩnh vực. Repo nào cũng kèm đủ dữ liệu nghiên cứu và hội thoại mẫu.

🧪 **Bảng điểm độ trung thực**: cả 15 skill chính thức đều qua kiểm thử mù độc lập bằng hai agent (nhất quán lập trường / nhận ra được phong cách / trung thực ở vùng biên / minh bạch nguồn / đầy đủ cấu trúc; phương pháp ở [references/fidelity-scorecard.md](references/fidelity-scorecard.md)), **tất cả đạt hạng A (≥85)**. Điểm: MrBeast/Naval/Taleb/Jobs/Karpathy/Paul Graham/Trương Tuyết Phong 97 · Munger/Feynman/X Mentor 96 · Trump 95 · Ilya 94 · Trương Nhất Minh 93 · Tôn Vũ Thần 91 · Musk 89. Bảng điểm đầy đủ trong `FIDELITY.md` của từng skill.

Muốn người không có trong danh sách? Cài Nữ Oa rồi nói "chưng cất XXX".

---

## Đóng góp & cộng đồng

Hệ sinh thái Nữ Oa lớn lên cùng cộng đồng theo hai đường khác nhau:

- **`SKILL.md` là tài sản lõi và không nhận PR từ bên ngoài.** Thấy lỗi hoặc cải tiến về phương pháp → mở issue để bàn; ý tưởng được nhận sẽ do người duy trì thực hiện và ghi công trong commit (xem PR #59 làm tiền lệ).
- **Skill nhân vật do cộng đồng chưng cất đi qua mục lục [COMMUNITY.md](COMMUNITY.md)**: giữ trong repo của bạn (sao là của bạn), chạy [bảng điểm độ trung thực](references/fidelity-scorecard.md) đạt hạng B trở lên, rồi gửi PR một dòng để được liệt kê.

Luật đầy đủ ở [CONTRIBUTING.md](CONTRIBUTING.md). Các bộ sưu tập cộng đồng, điều phối nhiều persona và ứng dụng theo chủ đề xem ở [COMMUNITY.md](COMMUNITY.md).

---

## Cách hoạt động

Nhập một cái tên, Nữ Oa làm bốn việc:

**1. Sáu luồng nghiên cứu song song**: bài viết, podcast/phỏng vấn, mạng xã hội, góc nhìn của người phê bình, hồ sơ quyết định, dòng thời gian cuộc đời. 6 agent chạy cùng lúc, mỗi luồng đều được lưu lại.

**2. Trích xuất qua ba lớp kiểm chứng**: một nhận định phải qua ba phép thử mới được ghi thành mô hình tư duy: xuất hiện ở từ 2 lĩnh vực trở lên (không phải phát ngôn một lần), dự đoán được lập trường ở câu hỏi mới (có sức dự đoán), không phải điều mà người thông minh nào cũng nghĩ ra (có tính riêng). Phải đủ cả ba.

**3. Dựng skill**: 3–7 mô hình tư duy + 5–10 heuristic ra quyết định + DNA biểu đạt + giá trị & phản mẫu + giới hạn thật, viết vào SKILL.md.

**4. Kiểm định chất lượng**: thử bằng 3 câu hỏi mà người đó đã trả lời công khai; hướng trả lời phải khớp. Sau đó thử 1 câu họ chưa từng đề cập; skill phải tỏ ra không chắc chắn đúng mức thay vì tự tin giả.

Phương pháp đầy đủ ở `references/extraction-framework.md`.

---

## Cấu trúc repo

```
nuwa-skill/
├── SKILL.md                    # Chính Nữ Oa
├── references/
│   ├── extraction-framework.md # Phương pháp trích xuất (đọc file này để hiểu sâu)
│   └── skill-template.md       # Mẫu để sinh skill
└── examples/
    ├── naval-perspective/       # Ví dụ đầy đủ Naval + dữ liệu nghiên cứu
    └── elon-musk-perspective/   # Ví dụ đầy đủ Musk + dữ liệu nghiên cứu
```

Toàn bộ nghiên cứu đều minh bạch. Các ví dụ có đủ file nghiên cứu: bạn xem được thông tin được thu thập, lọc và biến thành mô hình tư duy ra sao.

---

## Lịch sử sao

<div align="center">

[![Star History Chart](https://api.star-history.com/svg?repos=alchaincyf/nuwa-skill&type=Date)](https://star-history.com/#alchaincyf/nuwa-skill&Date)

</div>

---

## Câu chuyện phía sau

[colleague-skill](https://github.com/titanwings/colleague-skill) gần đây bùng nổ trên GitHub: chưng cất đồng nghiệp sắp nghỉ việc thành AI skill, vượt 5.000 sao trong vài ngày. Nó chứng minh một điều: chưng cất một con người là hoàn toàn làm được.

Đã có khả năng chưng cất người, sao chỉ dừng ở đồng nghiệp bên cạnh? Hãy chưng cất những bộ óc giỏi nhất của mọi lĩnh vực. May là những người này thường để lại rất nhiều tư liệu chưng cất được: sách, bài nói, phỏng vấn, mạng xã hội. Đó là một sự nâng cấp lớn cho chính tư duy của bạn.

Tôi đã làm việc tương tự một thời gian: không phải chưng cất đồng nghiệp, mà là Munger, Feynman, Naval, Musk, Taleb. Hôm nay tôi mở mã nguồn phương pháp này.

Nữ Oa không sao chép con người. Nó trích xuất hệ điều hành nhận thức.

**Nữ Oa (女娲)** là nữ thần trong thần thoại Trung Hoa nặn người từ đất sét. Ở đây đất sét là thông tin công khai, và thứ được tạo ra không phải con người, mà là một tấm gương.

---

## Về tác giả

Hoa Thúc (Huashu / Huasheng), AI Native Coder, nhà phát triển độc lập. Mọi sản phẩm đều do AI viết code ([Kitten Fill Light](https://apps.apple.com/app/id6738028637) từng đứng #1 bảng app trả phí App Store Trung Quốc). Đang chạy hơn 40 skill tự làm trong Claude Code. Nữ Oa là skill tạo ra skill.

- WeChat Official Account: 花叔 (Huashu)
- X: [@AlchainHust](https://x.com/AlchainHust)
- Bilibili: [花叔](https://space.bilibili.com/14097567)
- YouTube: [@Alchain](https://www.youtube.com/@Alchain)

## Giấy phép

MIT: cứ dùng, sửa, xây tiếp.

---

<div align="center">

**colleague-skill** chưng cất việc một người làm.<br>
**Nữ Oa** chưng cất cách một người nghĩ.<br><br>
*Người tiếp theo bạn muốn chưng cất không nhất thiết phải là đồng nghiệp.*

<br>

MIT License © [Huashu](https://github.com/alchaincyf)

</div>
