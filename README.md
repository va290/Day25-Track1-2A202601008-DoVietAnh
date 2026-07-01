# Day 25 — Track 1: Roadmap & Execution (RICE · Now/Next/Later · OKR · Dependency)

**Học viên:** Đỗ Việt Anh · MãHV **2A202601008** · Repo: `Day25-Track1-2A202601008-DoVietAnh`
**Sản phẩm áp dụng:** **ISA — International Student Assistant** (PRD Day 17 / dự án exam `Exam/C2-App-044`)

## Bài này làm gì
Biến 100 ý tưởng tính năng của ISA thành một kế hoạch execution defendable trước nhà đầu tư, qua 4 framework (4 block):

| Block | Câu hỏi | Framework | File |
|---|---|---|---|
| 1 | Làm **gì** trước? | RICE + 2×2 Value-Effort | [`rice_matrix.md`](rice_matrix.md) |
| 2 | Làm **khi nào**? | Now / Next / Later | [`roadmap_nnl.md`](roadmap_nnl.md) |
| 3 | **Đo** bằng gì? | OKR (Objective + 3 KR) | [`okrs.md`](okrs.md) |
| 4 | **Rủi ro** ở đâu? | Dependency Map + Critical Path | [`dependency_map.md`](dependency_map.md) |

> Tên file theo đúng convention slide Submission (trang 33): `rice_matrix.md` · `roadmap_nnl.md` · `okrs.md` · `dependency_map.md`.

## Slide trình bày
- [`demo.html`](demo.html) — deck 10 trang (left panel TOC, ← → / phím mũi tên).
- [`Day25-slides.pdf`](Day25-slides.pdf) — bản PDF 10 trang (render từng slide → join).

## Kết quả cốt lõi (ISA)
- **RICE:** F2 Guardrail+Escalation cao nhất (~94) → **làm trước**; F1 RAG = Strategic Bet (moat, effort cao); **U16 Thích nghi văn hóa = Non-starter → bỏ**.
- **Now/Next/Later:** NOW = an toàn visa (F2) + định hướng (F5); NEXT = RAG grounding (F1) + freshness (F4) + eval (F6); LATER = trợ lý toàn vòng đời + phân phối B2B.
- **OKR:** đo *outcome* (adoption · **deflection** thay MRR vì phi lợi nhuận · NPS + an toàn), không đo Output.
- **Dependency:** LLM API / hosting / nguồn KB — mỗi Tier-1 có Plan B deploy ≤24h; Critical Path = **Data + Legal** (đúng đặc trưng AI startup).

## Nguyên tắc bám theo deck
3 luật "chấm thật" (Reach ×0.5 · Effort ×1.5 · Confidence ≤50% nếu chưa test user) · roadmap = *vấn đề* không phải *tính năng* & không ngày tháng · OKR đo outcome không output · "không có Plan B = kinh doanh nhà thuê".

> Repo không chứa API key/token/credential hay dữ liệu cá nhân nhạy cảm.
