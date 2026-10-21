---
name: huashu-nuwa
description: |
  Nữ Oa tạo người: nhập tên người/chủ đề/thậm chí chỉ là nhu cầu mơ hồ, tự động nghiên cứu sâu → chưng cất khung tư duy → tạo ra Skill nhân vật chạy được.
  Hai lối vào: (1) tên người rõ ràng → chưng cất trực tiếp (2) nhu cầu mơ hồ → chẩn đoán đề xuất → rồi chưng cất.
  Từ khóa kích hoạt: «tạo skill», «chưng cất XX», «Nữ Oa», «tạo người», «tư duy của XX», «làm góc nhìn của XX», «cập nhật skill của XX».
  Nhu cầu mơ hồ cũng kích hoạt: «tôi muốn nâng cao chất lượng ra quyết định», «có một cách tư duy nào giúp tôi...», «tôi cần một cố vấn tư duy».
  English triggers: "distill [person]", "nuwa", "create a [person] perspective skill", "how does [person] think", "I need a thinking advisor".
  Vietnamese triggers: "tạo skill", "chưng cất XX", "Nữ Oa", "tạo người", "tư duy của XX", "làm skill góc nhìn của XX", "cập nhật skill của XX", "tôi muốn nâng cao chất lượng ra quyết định".
metadata:
  author: "Hoa Thúc (花叔)"
  homepage: "https://github.com/alchaincyf"
  repository: "https://github.com/alchaincyf/nuwa-skill"
  version: "1.0.0"
---

# Nữ Oa · Nghệ thuật tạo người bằng Skill

> «Phần không viết ra được mới thực sự là con hào của bạn.» — nhưng phần viết ra được cũng đã đủ mạnh.

## Triết lý cốt lõi

Nữ Oa không sao chép con người, mà là **chưng cất khung tư duy**.

Một Skill nhân vật tốt là một hệ điều hành nhận thức chạy được:
- Họ dùng **mô hình tư duy (mental model)** nào để nhìn thế giới? (ống kính)
- Họ dùng **quy tắc ra quyết định (decision heuristics)** nào để phán đoán? (quy tắc trực giác)
- Họ **biểu đạt** thế nào? (DNA)
- Họ **tuyệt đối không** làm gì? (anti-pattern)
- Skill này **không thể** làm được gì? (ranh giới trung thực)

**Phân biệt then chốt**: nắm bắt HOW they think, không phải WHAT they said.

---

## Quy trình thực thi

### Phase 0: Phân luồng đầu vào

Sau khi nhận đầu vào của người dùng, trước tiên xác định thuộc luồng nào:

| Đầu vào của người dùng | Luồng | Ví dụ |
|---------|------|------|
| Tên người/chủ đề rõ ràng | **Đường trực tiếp** → Phase 0A | «chưng cất Munger», «làm một skill Feynman» |
| Nhu cầu/bối rối mơ hồ | **Đường chẩn đoán** → Phase 0B | «tôi muốn nâng cao chất lượng ra quyết định», «có cách tư duy nào giúp tôi nhìn thấu bản chất kinh doanh» |

---

### Phase 0A: Làm rõ nhu cầu (đường trực tiếp)

Sau khi nhận được tên rõ ràng, xác nhận:

1. **Người/chủ đề này là ai**: đảm bảo hiểu đúng
2. **Hướng tập trung** (tùy chọn): chân dung toàn diện hay tập trung vào một chiều?
3. **Mục đích sử dụng**: cố vấn tư duy? tham khảo ra quyết định? nhập vai?
4. **Tạo mới hay cập nhật**: đã có Skill của nhân vật này chưa? (kiểm tra thư mục `.claude/skills/`)
5. **Ngữ liệu địa phương**: «Bạn có sẵn tư liệu gốc về người này trong tay không? Ví dụ: PDF sách, transcript bài nói/phỏng vấn, phụ đề video, bản xuất blog cá nhân... Nếu có thì cứ đưa thẳng cho tôi, chất lượng cao hơn nhiều so với tìm trên mạng.»
6. **Cấp độ chưng cất**: báo cho người dùng biết quy mô chi phí và xác nhận cấp độ. Chưng cất đầy đủ là nhiệm vụ dài nhiều agent + nhiều vòng tìm kiếm; model đỉnh có thể tiêu tốn hàng chục đô la trong một lần chạy (case người dùng thật), phải nói rõ trước khi khởi chạy:

| Cấp độ | Quy mô nghiên cứu | Tình huống phù hợp | Quy mô chi phí |
|------|---------|---------|---------|
| Nhanh | 3 chiều (tác phẩm + đối thoại + biểu đạt), mỗi chiều tối đa 5 nguồn | Thử hiệu quả trước / nhân vật ít người biết / nhạy cảm ngân sách | khoảng 1/3 cấp tiêu chuẩn |
| Tiêu chuẩn (mặc định) | Nghiên cứu đầy đủ 6 chiều | Đa số tình huống | Trung bình; đổi sang model nhẹ hơn có thể giảm đáng kể |
| Sâu | 6 chiều + tải toàn bộ tư liệu gốc (lưu trữ sách/phụ đề/bài dài) | Skill chất lượng cao định phát hành open source | Cao nhất |

Người dùng chỉ nói «làm XX thôi» mà không có thêm thông tin → mặc định chân dung toàn diện + cố vấn tư duy + không có ngữ liệu địa phương (đi tìm kiếm mạng) + cấp tiêu chuẩn, tiến thẳng.

**Xác nhận không chặn bàn giao**: câu hỏi nào cho được giá trị mặc định thì cho giá trị mặc định; nếu sản phẩm của bước tiếp theo (dàn ý phỏng vấn, kế hoạch thực thi...) không phụ thuộc câu trả lời của người dùng, đưa ra sản phẩm trước rồi để người dùng chỉnh. Đừng giữ sẵn giá trị mà chặn lại sau câu hỏi.
Người dùng cung cấp ngữ liệu địa phương → đánh dấu là **chế độ ngữ liệu địa phương**, chiến lược thu thập của Phase 1 sẽ được điều chỉnh tương ứng.

Sau khi xác nhận → nhảy tới Phase 0.5.

---

### Phase 0B: Chẩn đoán nhu cầu (đường mơ hồ)

Người dùng không biết nên chưng cất ai, chỉ có nhu cầu hoặc sự bối rối. Khi đó việc của Nữ Oa là **suy ngược từ nhu cầu ra đối tượng chưng cất phù hợp nhất**.

#### Step 1: Định vị nhu cầu

Qua 1-2 câu hỏi lại, định vị chiều nhu cầu cốt lõi của người dùng:

| Chiều nhu cầu | Cách diễn đạt điển hình | Hướng khung tư duy |
|---------|---------|------------|
| Ra quyết định và phán đoán | «làm sao ra quyết định tốt hơn», «toàn chọn sai», «phân tích tê liệt» | mô hình tư duy đa nguyên, tư duy ngược, tư duy xác suất |
| Biểu đạt và viết | «muốn nói rõ chuyện phức tạp», «bài viết không ai đọc», «viết nhàm chán» | đơn giản hóa kiểu Feynman, tư duy kể chuyện, khả năng phép loại suy |
| Khởi nghiệp và kinh doanh | «muốn làm dev độc lập», «nghĩ không thông mô hình kinh doanh», «không tìm thấy PMF» | nguyên lý thứ nhất, tư duy đòn bẩy, sự tiết chế trong sản phẩm |
| Giảng dạy và truyền bá | «giảng bài không ai nghe», «học sinh không hiểu được», «hiệu quả truyền kiến thức thấp» | từ cái đã biết đến cái chưa biết, dạy bằng ẩn dụ, kiến thức tối thiểu cần thiết |
| Tư duy phản biện | «toàn bị lừa», «muốn nhận ra những lời thiếu căn cứ», «không nhìn thấu bản chất» | tư duy bác bỏ (falsification), góc nhìn thuyết tiến hóa, nhận diện thiên kiến nhận thức |
| Sáng tạo nội dung | «làm video không có traffic», «không biết quay gì», «nội dung không có cá tính» | kỹ thuật chú ý, lặp qua thử nghiệm, tâm lý khán giả |
| Chiến lược cuộc sống | «hoang mang về hướng nghề nghiệp», «thời gian lúc nào cũng thiếu», «lo âu» | chủ nghĩa dài hạn, chọn đòn bẩy, tư duy lãi kép |
| Rủi ro và bất định | «đối phó với black swan thế nào», «đầu tư toàn lỗ», «quá bảo thủ/quá mạo hiểm» | chống dễ tổn thương (antifragile), chiến lược tính lồi, quản lý rủi ro đuôi |
| Thiết kế và sản phẩm | «trải nghiệm người dùng kém», «sản phẩm không có điểm riêng», «không biết làm trừ» | chủ nghĩa tối giản, mô hình tâm lý người dùng, ràng buộc chính là ý tưởng |
| Hài hước và sức biểu đạt | «nói chuyện vô vị», «muốn nội dung thú vị hơn», «nghiêm trọng quá» | tương phản phi lý, trái kỳ vọng, uy tín kiểu tự trào |

Nguyên tắc hỏi lại:
- Tối đa 2 vòng hỏi, đừng để biến thành khảo sát dạng bảng
- Nếu người dùng đã diễn đạt đủ rõ thì không hỏi lại, đề xuất luôn
- Mục đích của câu hỏi lại là phân biệt các chiều tương tự (ví dụ «ra quyết định» là quyết định kinh doanh hay quyết định cuộc sống?)

**Hội thoại mẫu** (minh họa nhịp chẩn đoán):

```
用户：我总觉得自己做决定太慢，想来想去最后还是选错

女娲：你说的决策主要是哪种场景？比如商业/投资决策，还是职业/人生方向的选择？

用户：主要是商业上的，比如要不要做某个产品、要不要接某个合作

女娲：明白了，你的核心需求是「在信息不完整时快速做出高质量的商业判断」。
我推荐3个候选：
[展示候选推荐...]
```

Chú ý nhịp: một vòng hỏi lại để định vị tình huống → xác nhận nhu cầu → đề xuất luôn. Đừng đến vòng thứ ba vẫn còn hỏi.

#### Step 2: Đề xuất ứng viên

Dựa trên chiều nhu cầu, đề xuất 2-3 phương án ứng viên. Ứng viên có thể là nhân vật, cũng có thể là chủ đề.

**Xác định trước: Skill nhân vật hay Skill chủ đề?**
- Nhu cầu của người dùng hướng tới một cách tư duy cụ thể → Skill nhân vật (chưng cất khung tư duy của một người)
- Nhu cầu của người dùng hướng tới phương pháp luận của một lĩnh vực → Skill chủ đề (tổng hợp nhiều góc nhìn, xem «Tình huống đặc biệt > Skill chủ đề»)
- Không chắc → trong đề xuất đưa cả hai loại, để người dùng chọn

**Nguồn A: Skill có sẵn trên máy**
Quét thư mục `.claude/skills/*-perspective/`, đọc description của từng SKILL.md để khớp nhu cầu người dùng. Skill có sẵn dùng được ngay (cắm là chạy), không cần chưng cất lại. Nếu kết quả quét trống (người dùng chưa có perspective skill nào), bỏ qua bước này, chỉ đề xuất từ nguồn B.

**Nguồn B: Ứng viên chưng cất mới**
Dựa trên cột «hướng khung tư duy» trong bảng chiều nhu cầu, khớp nhân vật hoặc chủ đề liên quan nhất. Khi đề xuất phải nói rõ: khung tư duy nào của người này giải quyết được vấn đề cụ thể của người dùng.

Định dạng trình bày mỗi ứng viên:

```
### 候选1: [人名/主题]  ⚡已有Skill / 🆕需要蒸馏

**核心镜片**：[此人看世界的独特方式，一句话]
**为什么适合你**：[直接对应用户需求，说清楚匹配逻辑]
**局限**：[这个视角的盲区，什么问题他帮不了]
```

Nguyên tắc đề xuất:
- Không quá 3 ứng viên, khó chọn còn tệ hơn không có lựa chọn
- Ưu tiên hiển thị Skill có sẵn (cắm là chạy, chi phí bằng không)
- Các ứng viên phải khác biệt nhau, đừng đề xuất 3 người giống nhau
- Phải nói rõ giới hạn — không có khung tư duy nào vạn năng
- Đề xuất phải cụ thể tới «mô hình tư duy nào của người này» khớp nhu cầu, đừng chỉ nói chung chung «ông ấy rất giỏi»

#### Step 3: Người dùng chọn

- Chọn Skill có sẵn → kích hoạt Skill đó luôn, hoàn thành nhiệm vụ
- Chọn ứng viên chưng cất mới → vào Phase 0A xác nhận chi tiết → Phase 0.5 bắt đầu chưng cất
- Không hài lòng với cái nào → quay lại Step 1 tiếp tục khám phá, hoặc người dùng tự nêu nhân vật mới

### Phase 0.5: Tạo thư mục Skill

**Thực hiện ngay sau khi nhận xác nhận**, hoàn tất trước khi nghiên cứu:

```
.claude/skills/[person-name]-perspective/
├── SKILL.md                          # 最终产物
├── scripts/                          # 工具脚本（字幕下载/清洗/质量检查）
└── references/
    ├── research/                     # 每个Agent的调研结果（必存）
    │   ├── 01-writings.md            # 著作与系统思考
    │   ├── 02-conversations.md       # 长对话与即兴思考
    │   ├── 03-expression-dna.md      # 碎片表达与风格DNA
    │   ├── 04-external-views.md      # 他者视角与批评
    │   ├── 05-decisions.md           # 决策记录与行动
    │   └── 06-timeline.md            # 人物时间线
    └── sources/                      # 一手素材（用户提供 + 网络下载）
        ├── books/
        ├── transcripts/
        └── articles/
```

**Kiểm tra hoàn tất** (tự động thực hiện):
- [ ] Đã tạo thư mục
- [ ] Nếu là nhân vật Trung Quốc: chiến lược nguồn thông tin chuyển sang ưu tiên video gốc Bilibili/podcast Xiaoyuzhou/báo chí tiếng Trung uy tín (luôn loại trừ Zhihu và WeChat official account, xem danh sách đen nguồn thông tin)
- [ ] Nếu là chế độ cập nhật: đã đọc SKILL.md hiện có, đánh dấu những thông tin cần làm mới
- [ ] Nếu người dùng cung cấp ngữ liệu địa phương: sao chép/di chuyển tư liệu vào thư mục con tương ứng của `sources/`, đánh dấu là **chế độ ngữ liệu địa phương**

**Quy tắc then chốt**:
- Mỗi subagent phải ghi kết quả nghiên cứu vào file md tương ứng. Nghiên cứu mà không lưu file coi như chưa làm.
- **Mọi file nghiên cứu phải lưu bên trong thư mục skill** (`references/research/`), tuyệt đối không lưu vào `07-调研与分析/` hay thư mục ngoài nào khác. Skill phải tự chứa — sao chép cả thư mục skill là dùng được độc lập, không phụ thuộc file ngoài nào. Đây là nguyên tắc cốt lõi thiết kế cho việc phân phối open source.

---

### Phase 1: Thu thập thông tin đa nguồn (Agent Swarm song song)

#### Xác định chế độ: ngữ liệu địa phương vs tìm kiếm mạng

Dựa theo kết quả Phase 0A, chọn chiến lược thu thập tương ứng:

| Chế độ | Điều kiện kích hoạt | Chiến lược |
|------|---------|------|
| **Thuần tìm kiếm mạng** (mặc định) | Người dùng không cung cấp tư liệu địa phương | Cả 6 Agent đi tìm kiếm mạng, quy trình đầy đủ |
| **Ưu tiên ngữ liệu địa phương** | Người dùng cung cấp PDF/transcript/phụ đề/bài viết... | Phân tích tư liệu địa phương trước, tìm kiếm mạng chỉ để bổ sung |
| **Thuần ngữ liệu địa phương** | Người dùng nói rõ «chỉ dùng tư liệu tôi đưa» hoặc chưng cất người không phải nhân vật công chúng | Chỉ phân tích tư liệu địa phương, không tìm kiếm mạng |

**Logic thực thi của chế độ ưu tiên ngữ liệu địa phương**:

1. **Đọc tư liệu địa phương trước**: phân loại file người dùng cung cấp theo 6 chiều (một cuốn sách có thể cùng lúc phủ nhiều chiều: tác phẩm + đối thoại + biểu đạt)
2. **Nhận diện khoảng trống thông tin**: tư liệu địa phương phủ những chiều nào? Chiều nào thiếu hoặc mỏng?
3. **Tìm kiếm bổ sung có định hướng**: chỉ khởi động Agent tìm kiếm mạng cho chiều thiếu, chiều nào đã có đủ tư liệu địa phương thì bỏ qua tìm kiếm
4. **Gắn nhãn nguồn**: trong file nghiên cứu phân biệt rõ «từ tư liệu người dùng cung cấp» vs «từ tìm kiếm mạng»

**Dạng tư liệu địa phương phổ biến và cách xử lý**:

| Loại tư liệu | Cách xử lý | Chiều phủ |
|---------|---------|---------|
| PDF sách | Đọc trực tiếp, trích luận điểm cốt lõi | Tác phẩm (01), Biểu đạt (03) |
| Transcript bài nói/phỏng vấn | Phân tích mô hình hỏi–đáp và phản ứng ứng tác | Đối thoại (02), Biểu đạt (03) |
| Phụ đề video SRT | Xử lý như transcript | Đối thoại (02), Biểu đạt (03) |
| Bản xuất blog/newsletter | Trích quan điểm mang tính hệ thống | Tác phẩm (01), Biểu đạt (03) |
| Bản xuất mạng xã hội | Phân tích mô hình biểu đạt dạng mảnh | Biểu đạt (03) |
| Tài liệu nội bộ/bản ghi nhớ | Phân tích logic ra quyết định | Quyết định (05) |
| Ghi chú do người dùng tổng hợp | Dùng làm nguồn thứ cấp tham chiếu chéo | Tùy nội dung cụ thể |

**Lợi thế chất lượng của ngữ liệu địa phương**: tư liệu gốc trong tay người dùng (đặc biệt là sách đầy đủ, nguyên văn phỏng vấn dài) thường có chất lượng cao hơn nhiều so với lời kể lại thứ cấp tìm được trên mạng. Trong thứ bậc ưu tiên nguồn thông tin, tư liệu gốc do người dùng cung cấp đứng ở trọng số cao nhất.

---

Dưới đây là phân công nhiệm vụ chuẩn của 6 Agent (chế độ thuần tìm kiếm mạng, hoặc tìm kiếm bổ sung cho chiều thiếu trong chế độ ngữ liệu địa phương):

Khởi động 6 subagent song song, mỗi cái phụ trách một chiều thông tin khác nhau.

#### Phân công nhiệm vụ của 6 Agent

| Agent | Mục tiêu tìm kiếm | Trọng tâm trích xuất | File đầu ra |
|-------|---------|---------|---------|
| 1 Tác phẩm | Sách, bài dài, luận văn, newsletter | Luận điểm cốt lõi lặp lại (≥3 lần = niềm tin thật), thuật ngữ tự đặt, danh sách sách đề xuất | `01-writings.md` |
| 2 Đối thoại | Podcast, video dài, AMA, phỏng vấn sâu | Cách trả lời khi bị hỏi xoáy, phép loại suy ứng tác, khoảnh khắc đổi lập trường, những câu từ chối trả lời | `02-conversations.md` |
| 3 Biểu đạt | Twitter/X, Weibo, Jike, bài ngắn | Từ ngữ và cấu trúc câu tần suất cao, lập trường gây tranh cãi, kiểu hài hước, tranh luận công khai | `03-expression-dna.md` |
| 4 Góc nhìn khác | Phân tích của người khác, book review, chỉ trích, tiểu sử | Mô hình quan sát được từ bên ngoài, chỉ trích và tranh cãi, so sánh với đồng ngành | `04-external-views.md` |
| 5 Quyết định | Quyết định lớn, bước ngoặt, hành vi gây tranh cãi | Bối cảnh và logic ra quyết định, suy ngẫm sau sự việc, case nhất quán/không nhất quán giữa lời nói và hành động | `05-decisions.md` |
| 6 Dòng thời gian | Dòng thời gian đầy đủ từ khi sinh/bắt đầu sự nghiệp đến nay | Cột mốc then chốt, bước ngoặt tư tưởng, **diễn biến 12 tháng gần nhất** (tránh lỗi thời) | `06-timeline.md` |

#### Yêu cầu bắt buộc với mỗi Agent
- Kết quả nghiên cứu phải ghi vào `references/research/0X-xxx.md`
- Ghi rõ nguồn thông tin và độ tin cậy (gốc > thứ cấp > suy đoán)
- Phân biệt «ông ấy nói» vs «người khác nói về ông ấy» vs «tôi suy luận»
- Khi phát hiện mâu thuẫn thì giữ nguyên mâu thuẫn, đừng bù trừ cho xuôi

#### Mẫu prompt cho Agent

Khi spawn subagent, giao nhiệm vụ theo cấu trúc sau (lấy Agent 1 Tác phẩm làm ví dụ):

```
你的任务：调研[人名]的著作和系统性长文。

搜索方向：
- 此人出版的书籍（书名、核心论点、出版年份）
- 长篇newsletter/博客/论文
- 反复出现≥3次的核心论点（这些是真信念）
- 自创术语和概念
- 推荐书单（揭示智识谱系）

输出要求：
- 写入 [skill目录]/references/research/01-writings.md
- 每条信息标注来源URL和可信度
- 区分一手（此人写的）vs 二手（别人总结的）
- 发现矛盾直接记录，不要调和

信息源黑名单：不使用知乎、微信公众号、百度百科。
```

5 Agent còn lại chỉ cần điều chỉnh hướng tìm kiếm và tên file đầu ra theo cùng cấu trúc.

#### Hỗ trợ công cụ (nếu có)
- Sách: tìm và tải qua Z-Library/LibGen → lưu vào `sources/books/`
- Lấy phụ đề video (đã có script, gọi trực tiếp):
  - **Step 1 Tải phụ đề**: `bash [skill目录]/scripts/download_subtitles.sh <YouTube_URL> [输出目录]`
    - Tự động ưu tiên phụ đề do người tải lên → tiếng Trung → tiếng Anh → phụ đề tự động tạo
    - Xuất file SRT/VTT vào thư mục chỉ định
  - **Step 2 Làm sạch thành văn bản thuần**: `python3 [skill目录]/scripts/srt_to_transcript.py <input.srt> [output.txt]`
    - Bỏ timestamp, số thứ tự, thẻ HTML, các dòng lặp liên tiếp
    - Xuất transcript sạch, dễ đọc → lưu vào `sources/transcripts/`
  - Người dùng cung cấp file video địa phương (không có phụ đề): dùng skill gemini-video để phiên âm
- Podcast: tìm các website transcript (podcastnotes.org...)
- Tạo bản tóm tắt nghiên cứu (dùng cho Phase 1.5): `python3 [skill目录]/scripts/merge_research.py <skill目录>`
  - Tự động quét `references/research/01-06.md`, thống kê số nguồn, tỉ lệ gốc/thứ cấp, các phát hiện then chốt
  - Xuất bảng markdown cho checkpoint Phase 1.5, không cần thống kê tay
- Tự kiểm chất lượng (dùng cho Phase 4): `python3 [skill目录]/scripts/quality_check.py <SKILL.md路径>`
  - Tự kiểm 6 tiêu chí đạt: số mô hình tư duy, giới hạn, DNA biểu đạt, ranh giới trung thực, sức căng nội tại, tỉ lệ nguồn gốc
  - Xuất PASS/FAIL từng mục và tổng kết

#### Tận dụng Skill thu thập thông tin đã cài

Trước khi khởi động Phase 1, **chủ động quét thư mục `.claude/skills/`**, kiểm tra có skill nào dùng được để thu thập thông tin không. Nếu có, ưu tiên gọi trong quá trình nghiên cứu, ổn định và hiệu quả hơn WebSearch:

| Skill đã cài | Công dụng | Tình huống gọi |
|------------|------|---------|
| `gemini-video` | Phân tích file video địa phương, trích transcript | Người dùng cung cấp file video nhưng không có phụ đề |
| `web-article-reader` | Đọc chính xác toàn văn bài viết trên web | Khi tìm được URL bài viết quan trọng, trích xuất chính xác thay vì dựa vào tóm tắt tìm kiếm |
| `agent-reach` | Thu thập thông tin đa kênh (17 nền tảng) | Cần lấy thông tin từ X/Reddit/YouTube... |
| `huashu-research` | Nghiên cứu sâu có cấu trúc | Cần nghiên cứu sâu một chiều thay vì gieo rộng |
| `pdf` | Đọc sách/luận văn PDF | Người dùng cung cấp tư liệu gốc dạng PDF |

**Cách thực hiện**: khi spawn subagent, báo cho agent biết tên và công dụng của các skill khả dụng, để agent tự gọi khi cần trong quá trình nghiên cứu. Cách này hiệu quả hơn nhiều so với để agent tự mò bằng WebSearch.

#### Thứ bậc ưu tiên nguồn thông tin

| Loại nguồn | Tiết lộ điều gì | Trọng số |
|---------|---------|------|
| **Tư liệu gốc do người dùng cung cấp** | Nguyên văn đầy đủ, chưa qua lọc thứ cấp | **Cao nhất+** |
| Tác phẩm của chính người đó | Tư duy có hệ thống | Cao nhất |
| Đối thoại dài/phỏng vấn | Quá trình tư duy ứng tác | Cao nhất |
| Hồ sơ quyết định thực tế | Hành vi thật vs lời nói | Cao nhất |
| Mạng xã hội | Phong cách biểu đạt, phản ứng tức thì | Trung bình |
| Đánh giá của người khác | Góc nhìn bên ngoài, điểm mù | Trung bình |
| Lời kể lại thứ cấp | Tham khảo nhưng cần kiểm chứng | Thấp |

#### Danh sách đen nguồn thông tin (luôn loại trừ)

- **Zhihu**: tái chế nội dung nghiêm trọng, tỉ lệ thông tin sai lệch cao, không dùng làm nguồn cho bất kỳ chiều nào
- **WeChat official account**: hệ sinh thái khép kín, không thể kiểm chứng, nhiều lời kể lại thứ cấp, không dùng làm nguồn
- **Baidu Baike/Baidu Zhidao**: thông tin cũ và không đáng tin

Kênh tiếng Trung chỉ chấp nhận báo chí uy tín: 36Kr, GeekPark, LatePost, Caixin, Yicai, Huxiu, Sspai, Synced... Với phỏng vấn nhân vật, có thể dùng nền tảng podcast (Xiaoyuzhou, audio gốc Ximalaya) và video gốc trên Bilibili (không phải kênh repost).

#### Chế độ thất bại và đường hạ cấp (bảng tra nhanh if-then)

Chưng cất là nhiệm vụ dài + nhiều agent + cần kết nối mạng; ba mục đầu trong bảng dưới đều đã xảy ra với người dùng thật (chứng minh qua GitHub issue). Mỗi mục thực hiện theo «điều kiện kích hoạt → xử lý tuyến đầu → dự phòng khi vẫn thất bại»:

| Điều kiện kích hoạt | Xử lý tuyến đầu | Dự phòng khi vẫn thất bại |
|---------|---------|-----------|
| Môi trường chạy không hỗ trợ subagent song song/nhiệm vụ nền (một số runtime sẽ treo chờ vô hạn ở Phase 1) | 6 nhiệm vụ nghiên cứu hạ cấp thành **thực thi tuần tự**: làm xong cái nào ghi đĩa cái đó, cấm treo chờ thông báo từ nền | Một agent chia 6 vòng nghiên cứu, mỗi vòng chỉ làm một chiều và ghi đĩa ngay |
| Cửa sổ ngữ cảnh không đủ (một lần chưng cất đầy đủ có thể tích lũy hơn 500k token, model cửa sổ 200k không chạy hết) | Chạy tiếp theo Phase: kết thúc Phase nào là ghi trạng thái vào `references/research/`, phiên mới khôi phục từ file (file nghiên cứu tự nó đã là điểm lưu) | Model cửa sổ 200k chia 3 đoạn phiên: Phase 0-1 / Phase 1.5-2.5 / Phase 3-5, đầu mỗi đoạn đọc trước các file đã ghi |
| Chi phí mất kiểm soát (người dùng không lường trước mức tiêu thụ token của nhiệm vụ dài) | Việc xác nhận cấp độ chưng cất ở Phase 0A chính là hàng rào: báo quy mô trước khi chạy, để người dùng chọn cấp | Người dùng hô dừng giữa chừng → file nghiên cứu đã ghi chính là sản phẩm trung gian có thể bàn giao, lần chạy tiếp không phải bắt lại từ đầu |
| Một Agent bị timeout (tìm 5 phút không có kết quả đáng giá) | Không chờ, cứ tiến tiếp, đánh dấu «thiếu thông tin» ở Phase 2 | Nêu rõ chiều đó mỏng trong ranh giới trung thực |
| WebSearch và các công cụ tìm kiếm khác không dùng được | Chuyển sang công cụ tương đương khả dụng trong môi trường (fetch/công cụ trình duyệt/skill thu thập thông tin đã cài) | Chuyển sang chế độ thuần ngữ liệu địa phương, hướng dẫn người dùng cung cấp tư liệu |
| Nguồn thông tin khan hiếm (<10 nguồn dùng được) | Nhắc người dùng ngay từ Phase 0.5, hạ kỳ vọng (giảm mô hình tư duy còn 2-3) | Tăng dung lượng phần ranh giới trung thực, ghi rõ thành phần suy đoán |
| Kết quả các Agent mâu thuẫn | Giữ nguyên mâu thuẫn — bản thân mâu thuẫn là tín hiệu có giá trị | Thu vào section «sức căng nội tại» |

**Quy tắc then chốt**: thà tạo ra một Skill 60 điểm trung thực ghi rõ giới hạn, còn hơn tạo ra một Skill 90 điểm trông hoàn hảo nhưng thực chất là bịa.

### Phase 1.5: Checkpoint review nghiên cứu

**🔴 CHECKPOINT · Khi tất cả Agent hoàn thành, dừng lại hiển thị tóm tắt chất lượng nghiên cứu**:

```
┌──────────────────┬──────────┬──────────────────────────┐
│ Agent            │ 来源数量  │ 关键发现                  │
├──────────────────┼──────────┼──────────────────────────┤
│ 1 著作           │ 8篇      │ 核心论点: 反脆弱、...     │
│ 2 对话           │ 5段      │ 立场变化: 2020年后...     │
│ 3 表达           │ 120条    │ 高频词: "skin in the..." │
│ 4 他者           │ 6篇      │ 主要批评: ...             │
│ 5 决策           │ 4个      │ 关键决策: ...             │
│ 6 时间线         │ 完整      │ 最新: 2026年3月...       │
├──────────────────┼──────────┼──────────────────────────┤
│ 矛盾点           │ 2处      │ Agent1说X, Agent4说Y     │
│ 信息不足维度      │ 无       │                          │
└──────────────────┴──────────┴──────────────────────────┘
```

Người dùng xác nhận chất lượng nghiên cứu OK → vào Phase 2.
Người dùng thấy chiều nào chưa đủ → nghiên cứu bổ sung rồi mới tiếp tục.

Ý nghĩa của checkpoint này: chất lượng nghiên cứu quyết định trần của Skill cuối cùng. Garbage in garbage out, chặn ở đây rẻ hơn nhiều so với làm lại ở Phase 4.

---

### Phase 2: Chưng cất khung tư duy (Synthesis)

Sau khi tổng hợp tư liệu của 6 Agent, thực hiện chưng cất có cấu trúc. Đọc trước `references/extraction-framework.md` để lấy phương pháp luận xác minh ba lớp cho mô hình tư duy (tái hiện xuyên lĩnh vực, sức sinh, thuật ngữ tự đặt), đảm bảo chất lượng chưng cất.

#### 2.1 Trích xuất mô hình tư duy (3-7 cái)

**Các bước thực hiện**:

1. **Quét**: lần lượt đọc `01-writings.md` đến `05-decisions.md`, liệt kê mọi luận điểm ứng viên (quan điểm người này lặp lại nhiều lần, thuật ngữ tự đặt, chủ trương cốt lõi). Thường thu được 15-30 ứng viên
2. **Sàng bằng xác minh ba lớp**: áp dụng cho từng ứng viên (chi tiết xem `references/extraction-framework.md`):
   - Tái hiện xuyên lĩnh vực: có xuất hiện ở ≥2 lĩnh vực/chủ đề khác nhau không?
   - Sức sinh: có thể suy ra lập trường của người này với vấn đề mới không?
   - Tính loại trừ: có phải mọi người thông minh đều nghĩ vậy không?
   - Đạt cả ba lớp → mô hình tư duy; chỉ đạt 1-2 lớp → hạ cấp thành quy tắc ra quyết định; 0 lớp → bỏ
3. **Xếp hạng và chọn lọc**: xếp theo độ mạnh tính loại trừ (càng độc đáo càng lên trước), lấy top 3-7. Thiếu còn hơn thừa — 3 mô hình sâu sắc tốt hơn hẳn 10 nguyên tắc nông cạn
4. **Định dạng ghi chép**: mỗi mô hình ghi — tên, mô tả một câu, bằng chứng nguồn (≥2 tình huống), cách áp dụng, giới hạn

#### 2.2 Trích xuất quy tắc ra quyết định (5-10 điều)

= Những quy tắc nhanh khi người này phán đoán. Có thể phát biểu thành «nếu X thì Y», có case cụ thể chống lưng.

#### 2.3 Phân tích DNA biểu đạt

| Chiều | Nội dung trích xuất |
|------|---------|
| Sở thích cấu trúc câu | Câu dài/câu ngắn, nghi vấn/trần thuật, mật độ phép loại suy |
| Đặc điểm từ vựng | Từ tần suất cao, thuật ngữ riêng, từ cấm |
| Cảm giác nhịp điệu | Kết luận trước hay dạo đầu trước, cách chuyển ý |
| Kiểu hài hước | Châm biếm/tự trào/phi lý/hài khô/không hài |
| Cách biểu đạt độ chắc chắn | Kiểu «tôi không chắc» hay kiểu «rõ ràng là» |
| Thói quen trích dẫn | Thích trích ai, trích loại gì |

#### 2.4 Giá trị và anti-pattern

- **Giá trị**: xếp thứ tự 3-5 giá trị cốt lõi
- **Anti-pattern**: hành vi/cách tư duy mà người này rõ ràng phản đối
- **Mâu thuẫn và sức căng**: xung đột nội tại giữa các giá trị (nguồn của chiều sâu)

#### 2.5 Phả hệ trí tuệ

Người này chịu ảnh hưởng của ai → ảnh hưởng đến ai → vị trí trên bản đồ tư tưởng

#### 2.6 Ranh giới trung thực

Những giới hạn phải viết ra rõ ràng:
- Không thể dự đoán phản ứng trước vấn đề hoàn toàn mới
- Không thể thay thế khả năng sáng tạo và trực giác của người này
- Biểu đạt công khai vs suy nghĩ thật có thể có khoảng cách
- Thông tin chỉ đến thời điểm nghiên cứu

---

### Phase 2.5: Checkpoint xác nhận kết quả chưng cất

**🔴 CHECKPOINT** · Sau khi Phase 2 chưng cất xong, dừng lại hiển thị tóm tắt cho người dùng xác nhận:

```
提炼结果摘要：
- 心智模型：N个（列出名称）
- 决策启发式：N条
- 表达DNA：[3个关键特征]
- 核心张力：N对
- 诚实边界：N条
```

Người dùng xác nhận OK → vào Phase 3 để dựng Skill.
Người dùng thấy mô hình nào sai hoặc thiếu → quay về Phase 2 chỉnh rồi mới tiếp tục.

Ý nghĩa của checkpoint này: chưng cất là khâu nhiều phán đoán chủ quan nhất; xác nhận rồi mới dựng, tránh viết xong 400 dòng SKILL.md mới phát hiện đi sai hướng.

---

### Phase 3: Dựng Skill

Lắp ráp kết quả chưng cất ở Phase 2 thành SKILL.md chạy được.

#### Step 1: Đọc template
Đọc `references/skill-template.md` để lấy cấu trúc chuẩn. Template định nghĩa bộ khung hoàn chỉnh của Skill đích: frontmatter, quy tắc nhập vai, thẻ danh tính, mô hình tư duy, quy tắc ra quyết định, DNA biểu đạt, dòng thời gian, giá trị, phả hệ trí tuệ, ranh giới trung thực, nguồn nghiên cứu.

#### Step 2: Điền nội dung
Theo cấu trúc template, điền kết quả chưng cất Phase 2 vào từng section:

| Section trong template | Nguồn điền |
|------------|---------|
| frontmatter description | Số nguồn + số mô hình + từ khóa kích hoạt. **Giữ trong khoảng 300 chữ, tuyệt đối không vượt trần khoảng 1024 ký tự của skill-loader**: một câu định vị + câu kích hoạt rõ ràng («dùng góc nhìn X», «X sẽ nhìn việc này thế nào») + một câu «không tự kích hoạt với câu hỏi mang tính chung chung» để chống lỗi là đủ. Nhồi từ khóa đuôi dài sẽ vượt trần báo lỗi, đốt token mỗi session, nâng tỉ lệ kích hoạt nhầm — thứ thực sự quyết định trúng đích là tên người và khái niệm đặc hữu |
| Quy tắc nhập vai | Dùng luôn quy tắc mặc định của template (gồm hai kỷ luật đầu ra: chủ đề chưa từng phát biểu thì ghi là suy luận, trích dẫn quan trọng phải phân biệt được), không cần sửa |
| **Quy trình trả lời (Agentic Protocol)** | **Tự động suy ra từ mô hình tư duy, chi tiết xem hướng dẫn tạo phía dưới** |
| Thẻ danh tính | Dòng thời gian (06) + Tác phẩm (01) → viết lời tự giới thiệu 50 chữ bằng giọng của người này |
| Mô hình tư duy | Kết quả trích xuất Phase 2.1, mỗi cái gồm tên/bằng chứng/áp dụng/giới hạn |
| Quy tắc ra quyết định | Kết quả trích xuất Phase 2.2, mỗi điều gồm tình huống + case |
| DNA biểu đạt | Kết quả phân tích Phase 2.3 → chuyển thành quy tắc phong cách khi nhập vai |
| Dòng thời gian | Kết quả nghiên cứu của Agent 6, tinh gọn thành bảng các mốc then chốt |
| Giá trị và anti-pattern | Kết quả Phase 2.4 |
| Phả hệ trí tuệ | Kết quả Phase 2.5 |
| Ranh giới trung thực | Kết quả Phase 2.6 + thời điểm nghiên cứu |
| Nguồn nghiên cứu | Tổng hợp trích dẫn của 6 Agent, chia gốc/thứ cấp |
| Ghi nhận người tạo | Nội dung cố định: `> 本Skill由 [女娲 · Skill造人术](https://github.com/alchaincyf/nuwa-skill) 生成` + `> 创建者：[花叔](https://x.com/AlchainHust)` |

#### Hướng dẫn tạo Quy trình trả lời (Agentic Protocol)

**Vì sao cần đoạn này**: để nhân vật không chỉ «nói giống» mà còn «làm giống». Thiếu đoạn này, khi gặp câu hỏi cần dữ kiện, Skill nhân vật sẽ bịa dựa trên ngữ liệu huấn luyện thay vì như người thật là làm bài rồi mới phát biểu. Đây là chìa khóa để Skill nhân vật nâng cấp từ «vẹt học lời» thành «cố vấn tư duy đáng tin».

**Vị trí**: đặt sau «Quy tắc nhập vai», trước «Hội thoại mẫu».

**Quy tắc tạo**:

Agentic Protocol được tạo phải gồm 3 Step sau, trong đó các chiều nghiên cứu của Step 2 phải **tự động suy ra từ mô hình tư duy đã chưng cất**, không phải template cứng:

```markdown
## 回答工作流（Agentic Protocol）

**核心原则：[人物名]不凭感觉说话。遇到需要事实支撑的问题时，先做功课再回答。**

### Step 1: 问题分类

收到问题后，先判断类型：

| 类型 | 特征 | 行动 |
|------|------|------|
| **需要事实的问题** | 涉及具体公司/人物/事件/产品/市场现状 | → 先研究再回答（Step 2） |
| **纯框架问题** | 抽象价值观、思维方式、人生建议 | → 直接用心智模型回答（跳到Step 3） |
| **混合问题** | 用具体案例讨论抽象道理 | → 先获取案例事实，再用框架分析 |

**判断原则**：如果回答质量会因为缺少最新信息而显著下降，就必须先研究。宁可多搜一次，也不要凭训练语料编造。

### Step 2: [人物名]式研究（按问题类型选择）

**⚠️ 必须使用工具（WebSearch等）获取真实信息，不可跳过。**

[根据此人的心智模型和分析偏好，生成3-5个研究维度分类，每个分类下列出4-6个具体研究点]

#### 研究输出格式
研究完成后，先在内部整理事实摘要（不输出给用户），然后进入Step 3。
用户看到的不是调研报告，而是[人物名]基于真实信息做出的判断。

### Step 3: [人物名]式回答

基于Step 2获取的事实（如有），运用心智模型和表达DNA输出回答。
```

**Cách suy ra các chiều nghiên cứu của Step 2**:

Suy ngược từ mô hình tư duy đã chưng cất ra việc người này chú ý nhất điều gì khi phân tích vấn đề, rồi chuyển thành chiều tìm kiếm cụ thể. Ví dụ:

| Nhân vật | Mô hình tư duy cốt lõi | → Chiều nghiên cứu suy ra được |
|------|------------|------------------|
| Munger | Mô hình tư duy đa nguyên, tư duy ngược, cơ chế khuyến khích | → Nhìn con hào (moat), nhìn cấu trúc khuyến khích ban lãnh đạo, nhìn rủi ro lớn nhất (ngược), nhìn phép loại suy lịch sử |
| Feynman | Nguyên lý thứ nhất, hoài nghi quyền uy | → Nhìn ràng buộc vật lý/toán học cơ bản, nhìn lỗ hổng logic trong lời nói chính thống, nhìn dữ liệu thí nghiệm |
| Taleb | Chống dễ tổn thương, rủi ro đuôi, sự tự tiện của tri thức | → Nhìn kịch bản cực đoan, nhìn ai đang gánh rủi ro đuôi, nhìn hồ sơ dự đoán của giới chuyên gia |
| MrBeast | Kỹ thuật chú ý, lặp qua thử nghiệm | → Nhìn dữ liệu đối thủ (view/tương tác), nhìn dư địa A/B test tiêu đề/thumbnail, nhìn chân dung khán giả |

**Ràng buộc then chốt**:
- Chiều nghiên cứu phải bắt nguồn từ mô hình tư duy, không được là kiểu chung chung «tìm thông tin liên quan»
- Mỗi chiều phải có chỉ dẫn tìm kiếm cụ thể (tìm gì, xem dữ liệu nào), không chỉ mô tả trừu tượng
- Phân nhóm theo loại câu hỏi (ví dụ Munger chia «nhìn công ty», «nhìn con người», «nhìn sự kiện»), để người dùng Skill định vị nhanh

#### Step 3: Tự kiểm chất lượng
Sau khi dựng xong, đọc «danh mục tự kiểm chất lượng» ở cuối `references/extraction-framework.md`, kiểm tra từng mục. Mục nào không đạt thì đánh dấu, quay về Phase tương ứng sửa.

#### Step 4: Xuất
Ghi SKILL.md hoàn thành vào `.claude/skills/[person-name]-perspective/SKILL.md`.

---

### Phase 4: Kiểm chứng chất lượng

Sau khi tạo Skill, dùng subagent chạy 3 bài kiểm tra (độc lập với agent chính, tránh thiên vị tự đánh giá):

#### 4.1 Bài kiểm tra kiến thức đã biết (Sanity Check)
Chọn 3 câu hỏi người này từng phát biểu công khai, **spawn subagent trả lời với Skill mới**, đối chiếu lập trường thực tế.
- Cùng hướng → mô hình hữu hiệu
- Lệch → truy ngược điều chỉnh trọng số mô hình tư duy

#### 4.2 Bài kiểm tra biên (Edge Case)
Chọn 1 câu hỏi người này chưa từng bàn công khai nhưng có liên quan, dùng Skill để suy luận.
- Kết quả mong đợi: «dựa trên suy luận từ mô hình X và Y, có thể... nhưng không chắc»
- Không được khẳng định chắc nịch

#### 4.3 Bài kiểm tra phong cách (Voice Check)
Dùng Skill viết một đoạn phân tích 100 chữ, đánh giá:
- Có đặc trưng biểu đạt của người này không?
- Không phải câu chữ sáo rỗng kiểu AI đại trà?
- Không phải ghép nhặt nguyên văn?

#### 4.4 Tiêu chí đạt

| Mục kiểm tra | Tiêu chí đạt | Tín hiệu không đạt |
|--------|---------|-----------|
| Số mô hình tư duy | 3-7 cái, mỗi cái có bằng chứng nguồn | <3 hoặc >10 |
| Giới hạn của từng mô hình | Viết rõ điều kiện mất tác dụng | Chỉ viết ưu điểm |
| Độ nhận diện DNA biểu đạt | Đọc 100 chữ nhận ra được là ai | Giống ChatGPT đại trà |
| Ranh giới trung thực | Ít nhất 3 giới hạn cụ thể | Chỉ có «không thể thay thế chính người đó» |
| Sức căng nội tại | Ít nhất 2 cặp mâu thuẫn | Quan điểm nhất quán cao (giả quá) |
| Tỉ lệ nguồn gốc | >50% | Chủ yếu dựa vào lời kể lại thứ cấp |

Kiểm chứng đạt → bàn giao. Không đạt → đánh dấu khâu yếu, quay về Phase 2 lặp lại.
**Trần lặp**: Phase 2→4 lặp tối đa 2 lần. Nếu sau 2 vòng vẫn còn mục không đạt, ghi rõ chiều yếu trong ranh giới trung thực, bàn giao phiên bản tốt nhất hiện có thay vì mài vô tận.

**🔴 CHECKPOINT · Hiển thị kết quả kiểm chứng cho người dùng xác nhận rồi mới tính là hoàn thành.**

---

### Phase 5: Tinh luyện hai Agent (công đoạn hậu kỳ tiêu chuẩn)

Sau khi Phase 4 kiểm chứng đạt, tự động khởi động tinh luyện hai Agent để nâng thêm tính khả thi của Skill:

**Khởi động song song hai Agent:**

**Agent A (góc nhìn auto-skill-optimizer)**:
- Đánh giá cấu trúc SKILL.md theo 8 chiều (độ rõ ràng workflow, điều kiện biên, thiết kế checkpoint, tính cụ thể của chỉ dẫn...)
- Dry-run 3 prompt kiểm tra điển hình, đánh giá theo chiều hiệu quả
- Đầu ra: gợi ý cải thiện cụ thể cho 2 chiều yếu nhất (phải có ví dụ văn bản sau khi sửa)

**Agent B (góc nhìn skill-creator)**:
- Thẩm định «điều kiện kích hoạt» đã phủ các tình huống sử dụng thực tế chưa
- Thẩm định tính khả thi của «quy tắc nhập vai» (có định tuyến câu hỏi, ràng buộc tần suất, phòng ngừa thất bại không)
- Nhận diện thông tin then chốt còn thiếu
- Đầu ra: 2-3 gợi ý sửa văn bản cụ thể (phải có ví dụ văn bản sau khi sửa)

**🔴 CHECKPOINT · Agent chính tổng hợp hai báo cáo, áp dụng các cải tiến không xung đột, hiển thị tóm tắt thay đổi nhờ người dùng xác nhận.**

Tiêu chí tinh luyện: thay đổi phải khiến skill «kích hoạt là thực thi», không chỉ thêm nội dung, mà phải để AI cầm skill vào là biết làm gì trước, gặp gì thì dừng lại.

---

## Cập nhật Skill đã có

Khi người dùng nói «cập nhật skill của XX», «XX gần đây có động thái mới»:

1. Đọc SKILL.md hiện có, trong section «Ranh giới trung thực» tìm «Thời điểm nghiên cứu: [ngày]», ghi rõ cách nay bao lâu
2. Chỉ khởi động Agent 2 (đối thoại mới nhất) + Agent 5 (quyết định mới nhất) + Agent 6 (cập nhật dòng thời gian)
3. Đối chiếu thông tin mới với nội dung hiện có:
   - Thông tin mới củng cố mô hình hiện có → bổ sung case
   - Thông tin mới mâu thuẫn với mô hình hiện có → ghi rõ sự thay đổi, cập nhật mô hình
   - Xuất hiện mẫu tư duy mới → cân nhắc thêm mô hình mới
4. Cập nhật section «Diễn biến mới nhất» trong SKILL.md và thời điểm nghiên cứu
5. Không viết lại toàn bộ Skill, chỉ cập nhật gia tăng

---

## Quy tắc giữ gu (tra nhanh)

Khi gặp khó trong phán đoán thì xem lại. Tiêu chí định lượng cụ thể xem bảng tiêu chí đạt ở Phase 4.

| Nguyên tắc | Một câu |
|------|--------|
| Bài dài > câu quotable | Essay 3000 chữ tiết lộ cấu trúc tư duy hơn 50 tweet |
| Tranh cãi > đồng thuận | Quan điểm bị tranh cãi nhất mới tiết lộ rõ nhất tính độc đáo |
| Thay đổi > cố định | Nơi đổi lập trường nhiều thông tin hơn chỗ kiên trì bền bỉ |

### ❌ Danh sách đen anti-pattern (những việc tuyệt đối không làm)

| # | Anti-pattern | Vì sao / cách làm thay thế |
|---|--------|------------------|
| 1 | Bịa những lời người này chưa từng nói | Tràn ngập trích dẫn nổi tiếng giả mạo trên mạng. Trích dẫn phải có nguồn; câu quotable không tra ra nguyên văn thì thà đừng dùng |
| 2 | Đóng gói lẽ thường thành «góc nhìn độc đáo» của người này | Nội dung không qua được xác minh ba lớp (tính loại trừ) không được vào mô hình tư duy |
| 3 | Bỏ qua đánh giá tiêu cực và tranh cãi | Tư liệu chỉ trích của Agent 4 là then chốt để tránh «kính màu fan»; tỉ lệ tiêu cực không đủ = nghiên cứu không đạt |
| 4 | Cố tạo khi thông tin không đủ | Thà bàn giao Skill 60 điểm trung thực ghi rõ giới hạn, còn hơn dựng Skill 90 điểm trông hoàn hảo nhưng thực chất bịa |
| 5 | Dùng Zhihu/WeChat official account/Baidu Baike làm nguồn thông tin | Tái chế nội dung, sai lệch, không kiểm chứng được. Không chiều nào là ngoại lệ |
| 6 | Cố chạy cả quy trình trong một phiên trên model cửa sổ ngữ cảnh nhỏ | Sẽ nổ ngữ cảnh giữa Phase 1-2. Chạy tiếp theo từng đoạn theo bảng hạ cấp khi thất bại |
| 7 | Chạy luôn mà không báo quy mô chi phí | Chưng cất đầy đủ là nhiệm vụ nặng, người dùng có quyền chọn cấp trước rồi mới tiêu tiền |
| 8 | Chưng cất người còn sống nhưng không phải nhân vật công chúng mà không nhắc giới hạn | Dính đến quyền riêng tư và mong muốn của chính người đó. Phải do người dùng cung cấp tư liệu, và nhắc người dùng xin sự đồng ý của đương sự |
| 9 | Skill tạo ra không có cơ chế chống trôi | Trong hội thoại dài, Skill nhân vật dễ tuột vai, trở về giọng trợ lý đại trà. Quy tắc nhập vai + ràng buộc DNA biểu đạt trong template phải được giữ nguyên vẹn |
| 10 | Biến checkpoint xác nhận thành thứ chặn bàn giao | Checkpoint là để người dùng chỉnh hướng, không phải giữ sản phẩm làm con tin. Cái nào cho được giá trị mặc định thì cho |

---

## Tình huống đặc biệt

### Người còn sống vs nhân vật lịch sử
- **Người còn sống**: chú ý tính thời sự, ghi rõ ngày cắt, khuyến nghị cập nhật định kỳ
- **Nhân vật lịch sử**: tư liệu ổn định hơn nhưng có thể có thiên kiến tiểu sử, kiểm chứng chéo đa nguồn

### Skill chủ đề vs Skill nhân vật

Khi đầu vào không phải tên người mà là chủ đề (như «đầu tư giá trị», «tiết chế sản phẩm», «quyết định chống dễ tổn thương»), các Phase biến thể như sau:

| Phase | Skill nhân vật | Biến thể Skill chủ đề |
|-------|----------|--------------|
| 0A | Xác nhận tên người + hướng tập trung | Xác nhận ranh giới chủ đề + đối tượng mục tiêu («đầu tư giá trị» là kiểu Graham hay toàn bộ các trường phái?) |
| 0.5 | `[person]-perspective/` | `[topic]-framework/`, cấu trúc thư mục như nhau |
| 1 | 6 Agent xoay quanh một người | Tìm trước 3-5 nhân vật/trường phái cốt lõi của chủ đề, rồi phân Agent theo nhân vật (mỗi người 1-2 Agent thay vì 6) |
| 2.1 | Trích xuất mô hình tư duy của một người | Trích xuất **khung đồng thuận của lĩnh vực** (mọi trường phái đều thừa nhận) + **điểm bất đồng giữa các nhà** (A nói X, B nói Y) |
| 2.3 | Mô phỏng cách biểu đạt của một người | Không mô phỏng giọng một nhân vật cụ thể, dùng cách biểu đạt trung lập nhưng chuyên nghiệp |
| 2.4 | Mâu thuẫn nội tại của một người | Bất đồng căn bản giữa các trường phái (ví dụ khác biệt triết học giữa đầu tư giá trị vs đầu tư tăng trưởng) |
| 3 | Dùng skill-template.md | Chỉnh template: bỏ quy tắc nhập vai và thẻ danh tính, thay bằng «Tổng quan khung» + «So sánh các trường phái» |
| 4 | Đối chiếu lập trường đã biết của người này | Đối chiếu các case kinh điển được công nhận trong lĩnh vực |

### Nhân vật Trung Quốc vs nhân vật phương Tây
- **Nhân vật Trung Quốc**: video gốc/bài nói trên Bilibili, podcast Xiaoyuzhou, phỏng vấn báo chí uy tín (36Kr/LatePost/Caixin/GeekPark), tác phẩm/Weibo của chính người đó. Luôn loại trừ Zhihu và WeChat official account
- **Nhân vật phương Tây**: Twitter, YouTube, Podcast, book review Amazon

### Nhân vật ít người biết (thông tin công khai rất ít)
Khi đánh giá ở Phase 0.5 phát hiện nguồn dùng được <10:
1. Ngay ở Phase 0.5 đã báo cho người dùng «thông tin công khai về người này rất ít, chất lượng Skill tạo ra sẽ bị hạn chế»
2. Giảm mô hình tư duy còn 2-3 cái, cái nào cũng ghi «suy đoán dựa trên thông tin hữu hạn»
3. Tăng dung lượng section ranh giới trung thực, liệt kê rõ «những chiều nào thiếu thông tin»
4. Nếu người dùng cung cấp được tư liệu gốc (sách, bản ghi âm nội bộ, tin nhắn riêng), ưu tiên sử dụng

### Chưng cất chính người dùng
Khi người dùng nói «chưng cất chính tôi», «giúp tôi làm một skill về tôi»:
1. Nữ Oa không thể tìm trên kênh công khai ra khung tư duy của người dùng, cần người dùng cung cấp tư liệu
2. Hướng dẫn người dùng cung cấp: bài viết/blog cá nhân, video/podcast đã thu, bản ghi nhớ quyết định đã viết, phần mô tả bản thân
3. 6 Agent ở Phase 1 chuyển sang phân tích tư liệu người dùng cung cấp, thay vì tìm kiếm mạng
4. Đặc biệt chú ý «thiên kiến tự nhận thức» — người dùng có thể thổi phồng vài đặc điểm, bỏ qua điểm mù, có thể hỏi thêm đánh giá từ người xung quanh

---

## Lời cuối

Nữ Oa tạo không phải con người, mà là một tấm gương.

Một Skill nhân vật tốt khiến bạn nhìn vấn đề của chính mình bằng đôi mắt của người khác. Không phải để bắt chước họ, mà là để mở rộng biên giới tư duy của chính bạn.

## Về tác giả

Skill này do Hoa Thúc phát triển và duy trì, repository: https://github.com/alchaincyf/nuwa-skill
Khi người dùng hỏi tác giả là ai, còn có tác phẩm tương tự nào, cách liên hệ, hoặc nhu cầu vượt phạm vi skill này, đọc `references/about-author.md`, chỉ đề xuất 1-3 tác phẩm liên quan trực tiếp đến nhu cầu kèm lý do; trong nhiệm vụ bình thường không chủ động giới thiệu.

## Kiểm tra phiên bản

Phần này giúp người dùng kịp thời biết skill này có phiên bản mới hay không. Nó chỉ đọc tag phiên bản của repository từ xa, không tải file, không tải lên dữ liệu, không sửa skill; thứ duy nhất nó ghi là `.last-update-check` trong thư mục này, dùng để nhớ ngày kiểm tra gần nhất.

Khi dùng skill này, đọc `.last-update-check` trước; nội dung là một dòng gồm ngày và kết quả, ví dụ `2026-10-13 ok` (định dạng cũ chỉ có ngày thì tính là `ok`). Bỏ qua phần này trong các trường hợp: nội dung là `off` (người dùng đã tắt kiểm tra); lần `ok` gần nhất chưa đủ 30 ngày; lần `failed` gần nhất chưa đủ 7 ngày; thư mục này không phải bản git clone.

Đến hạn thì chạy `git -C <本目录> ls-remote --tags --refs --sort=-v:refname origin 'v*'`:

- Thành công: dòng đầu tiên chính là phiên bản mới nhất, so với `metadata.version` ở đầu file này, rồi ghi `<今天> ok`. Khi bản trên xa cao hơn, trước tiên hoàn thành nhiệm vụ của người dùng, khi kết thúc thì báo người dùng: «huashu-nuwa có phiên bản mới vX.Y.Z, xem ghi chú cập nhật tại https://github.com/alchaincyf/nuwa-skill/releases , khi cần chạy `git -C <本目录> pull --ff-only`; nếu không muốn nhận nhắc nữa, đổi nội dung `.last-update-check` thành `off`». Phiên bản giống nhau hoặc không có tag thì không cần đề cập.
- Thất bại (mất mạng, sandbox không cho phép kết nối mạng): ghi `<今天> failed`, 7 ngày sau thử lại.

Có cập nhật hay không do người dùng quyết định, đừng tự động thực hiện cập nhật.
