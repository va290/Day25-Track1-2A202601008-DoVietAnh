# Day 25 · Block 1 · Workshop 1 — RICE cho ISA

> Đỗ Việt Anh · 2A202601008 · Track 1 — Roadmap & Execution
> PRD nguồn: **ISA — International Student Assistant** (`Exam/C2-App-044/docs/PRD.md`)
> Output: Bảng RICE 5 dòng + 2×2 Value-Effort → input cho Block 2 (Now/Next/Later).

## Giả định chấm điểm (để số liệu defendable)
- **Pilot tại 1 trường**, cơ sở ~**300–400 SV quốc tế** trong diện dùng ISA.
- **Reach = số user đụng tính năng / quý**, **đã chiết khấu ×0.5** (deck: đừng lạc quan Reach).
- **Effort = person-month, đã ×1.5** (deck: QA + bug + integration luôn đội).
- **Confidence honest**: ISA **chưa có user thật**, giả định PRD §10 chưa kiểm chứng → tối đa 80%; feature nào rủi ro giả định cao → **50%**.

## 5 tính năng cốt lõi được chấm (từ PRD)
| # | Tính năng | Nguồn PRD |
|---|---|---|
| F1 | **RAG chatbot có trích dẫn** (hỏi-đáp học vụ/sinh hoạt, chỉ trả lời từ tài liệu chính thức + citation + `updated_at`) | F1 · US-003/004/005 |
| F2 | **Guardrail + Escalation pháp lý/visa** (intent LEGAL/uncertain → không bịa → chuyển người thật) | F2 · US-007/008 |
| F5 | **Onboarding checklist + Danh bạ dịch vụ** (checklist 3 tháng đầu theo hồ sơ + directory phòng ban/hotline) | F5 · US-009/010 |
| U6 | **Trả lời đa ngôn ngữ** (multilingual) | US-006 |
| U16 | **Thích nghi văn hóa** (cultural adaptation) | US-016 (“có thì tốt”) |

> **Loại khỏi 5 dòng có chủ đích:** **F4 Admin-KB** và **F6 Eval** là công cụ *admin/nội bộ* — Reach trực tiếp ~vài người → RICE cho điểm gần 0 và định giá **thấp sai lệch** (đúng “giới hạn RICE với infra” trong deck). Chúng là *enabler bắt buộc*, không đưa vào cuộc đua ưu tiên user-facing này.

## Bảng RICE
| Tính năng | Reach /quý (đã ×0.5) | Impact | Confidence | Effort pm (đã ×1.5) | **Score = (R·I·C)/E** | Hạng |
|---|---|---|---|---|---|---|
| **F2 — Guardrail + Escalation** | 90 | 3 (massive) | 0.8 | 2.3 | **≈ 94** | 🥇 1 |
| **F5 — Onboarding + Directory** | 125 | 1 (medium) | 0.8 | 1.2 | **≈ 83** | 🥈 2 |
| **U6 — Multilingual** | 100 | 0.5 (low) | 0.8 | 0.6 | **≈ 67** | 🥉 3 |
| **F1 — RAG + citations** | 150 | 2 (high) | 0.5 | 3.8 | **≈ 39** | 4 |
| **U16 — Cultural adaptation** | 40 | 0.5 (low) | 0.5 | 3.8 | **≈ 2.6** | 5 |

**Lý do các số then chốt:**
- **F2 Impact = 3, Confidence = 0.8:** đây là *differentiator + an toàn* (visa cost-of-error cao); cơ chế rõ (legal → escalate), rủi ro thấp hơn F1 nên tự tin hơn. Effort thấp vì phần lớn là *routing + ticket*, không cần trả lời.
- **F1 Confidence = 0.5:** phụ thuộc giả định “tài liệu phủ ≥80% câu hỏi” — **chưa kiểm chứng**. Effort cao nhất (pipeline RAG đầy đủ) → RICE thấp dù value cao.
- **U6 Effort rất thấp:** LLM lo đa ngôn ngữ gần như “free” → điểm cao nhưng Impact thấp (không phải differentiator — ChatGPT cũng đa ngôn ngữ).
- **U16 điểm ~0:** value chưa được xác thực + làm *đúng* thì tốn (tuning + test đa văn hóa) → low value, high effort.

## 2×2 Value–Effort Matrix
```
   VALUE cao
      │
  QUICK WINS            │   STRATEGIC BETS
  (làm ngay, lấy đà)    │   (đầu tư dài hạn = moat)
   • F2 Guardrail+Escal │    • F1 RAG + citations
   • F5 Onboarding+Dir  │
  ─────────────────────┼───────────────────────  EFFORT
  FILL-INS              │   NON-STARTERS
  (làm khi rảnh)        │   (VỨT vào sọt rác)
   • U6 Multilingual    │    • U16 Cultural adaptation
      │
   VALUE thấp
   Effort thấp  ←──────────────────→  Effort cao
```

## Kết luận (3 chỉ định theo Bước 4)
- ✅ **Quick Win làm trước → F2 (Guardrail + Escalation).** RICE cao nhất (~94), là *differentiator + an toàn*, effort vừa phải, **de-risk ngay job giá trị nhất (visa/pháp lý)**. Kèm F5 (onboarding/directory) là quick win phụ.
- 🏰 **Strategic Bet moat dài hạn → F1 (RAG + citations).** Effort cao nên RICE thấp, **nhưng đây là con hào**: trả lời bám tài liệu chính thức + trích dẫn là thứ ChatGPT/Gemini không có → vẫn phải build, chấp nhận đắt.
- ❌ **Non-starter bỏ thẳng → U16 (Thích nghi văn hóa).** Low value (chưa xác thực) + high effort → “VC ghét nhất nếu thấy trong roadmap”. Cắt.

> **Ghi chú trung thực:** Không tính năng nào Confidence = 100% vì **chưa phỏng vấn/đo user thật** — đúng cảnh báo “Confidence ảo” của deck. Ưu tiên có thể đổi ngay khi có số liệu pilot/eval đầu tiên.
