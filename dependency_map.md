# Day 25 · Block 4 · Workshop 4 — Dependency Map + Critical Path (ISA)

> Đỗ Việt Anh · 2A202601008 · Track 1 — Roadmap & Execution
> Input: cột **NOW**. Câu hỏi sống còn: *“Nếu OpenAI/Anthropic sập ngày mai, ISA còn chạy được không?”*
> Output: 3 dependencies + Plan B + Critical Path 1 trang.

## A. Dependency Map — 3 “con dao treo trên đầu” (30 ngày tới)
> Quy tắc deck: **mỗi Tier-1 dependency phải có Plan B deploy được trong 24h** — không có Plan B thì “không phải startup, là kinh doanh nhà thuê”.

| Tier | Dependency | Worst-case (1 câu) | Plan B (deploy ≤7 ngày) | Cost Plan B |
|---|---|---|---|---|
| **1 — Critical** | **LLM API** (Anthropic/OpenAI) — lõi trả lời | Bị rate-limit/khóa account/tăng giá 5× → **product down** | **Abstraction layer đa nhà cung cấp**: chuyển Claude ↔ Gemini/GPT sau 1 dòng config; sẵn key dự phòng | ~0.5 person-month dựng lớp trừu tượng + phí API cao hơn chút |
| **1 — Critical** | **Hosting / Cloud** (Railway/free tier) | Hết free tier / region down / vượt quota → **app offline** | **Đóng gói container, portable**: redeploy sang Render/Fly/VPS; tài liệu deploy sẵn | ~vài giờ + ~$5–20/tháng khi rời free tier |
| **2 — Important** | **Nguồn tài liệu chính thức** (KB: web trường/cổng XNC) | Nguồn đổi/đóng/ẩn sau login → KB **lỗi thời** → “sai một cách có thẩm quyền” | **Snapshot + `updated_at`** mọi tài liệu; admin xác minh định kỳ; đàm phán feed chính thức với CTSV | Giờ công admin (định kỳ) + thời gian đàm phán |

*(Ghi chú: vector store/DB tự host → rủi ro thấp hơn, không xếp Tier-1. Rủi ro pháp lý/PII được xử ở guardrail, không phải external dependency.)*

## B. Critical Path cho cột NOW
> Critical Path = **chuỗi task dài nhất & bắt buộc tuần tự**. Trễ 1 ngày trên chuỗi này = trễ launch 1 ngày; trễ task phụ (có buffer) = không sao.

```
CRITICAL PATH (đỏ) — tuần tự, không rút ngắn được:

① Thu thập &        ② Chốt ranh giới      ③ Chat + phân      ④ Guardrail +      ⑤ Eval an toàn     ⑥ Deploy
  xác minh KB   ──▶   pháp lý + rule   ──▶   loại intent   ──▶  Escalation    ──▶  luồng visa    ──▶  pilot +
  (thủ tục)           escalation            (legal/thường)      → người thật       (escalate đúng)    feedback
  [DATA]              [LEGAL]                                    (F2)               [chặn launch]

Task phụ (xám, có buffer — KHÔNG trên critical path):
   • F5 Onboarding checklist + Danh bạ  ── chạy song song, không block F2
   • Đa ngôn ngữ (U6) ── gần free, ship kèm
```

**Task blocking:** ① blocks ②③ · ② blocks ④ · ③ blocks ④ · ④ blocks ⑤ · ⑤ blocks ⑥.
**Chuỗi dài nhất (Critical Path):** ① → ② → ③ → ④ → ⑤ → ⑥.

## C. Ghi chú then chốt
- **Đúng insight deck:** với AI startup, **Data (thu thập KB) + Legal Compliance (ranh giới pháp lý)** gần như **luôn nằm trên Critical Path** — và ở ISA đúng là 2 task đầu chuỗi. Muốn launch nhanh → tối ưu 2 khâu này trước, không phải tô UI.
- **F5 (onboarding/directory) tuy là Quick Win nhưng KHÔNG trên critical path** → làm song song, không quyết định ngày launch.
- **Bài học Case 4 (deck):** startup tóm tắt pháp lý chết vì OpenAI siết rate-limit đúng ngày launch — ISA né bằng **abstraction layer đa nhà cung cấp (Plan B Tier-1)** ngay từ NOW.
