# Vận dụng cơ bản 2: Khắc phục lỗi khai báo biến số

## Bước 1: Phân tích lỗi

**Prompt lỗi:** `Hãy viết một bài chia sẻ về Kỹ thuật Prompting Nâng cao (Logic & Chuỗi) bằng ngôn ngữ [language]. Dành cho đối tượng {audience}.`

- **Trộn 2 kiểu ngoặc** (`[ ]` và `{ }`): code thay thế chỉ bắt được 1 kiểu, bỏ sót kiểu còn lại.
- **Tên viết thường**: lẫn với từ thường trong câu, AI và regex khó nhận diện biến.
- **`{ }` trùng cú pháp** `str.format()`/JSON: dễ gây lỗi `KeyError`, crash.
- **Biến sót không lộ ra**: AI có thể đọc nguyên chữ `[language]` rồi tự bịa nội dung.

## Bước 2: Đồng bộ biến số

**Quy ước:** chỉ dùng `[ ]`, viết hoa, gạch dưới.

```text
Hãy viết một bài chia sẻ về Kỹ thuật Prompting Nâng cao (Logic & Chuỗi)
bằng ngôn ngữ [NGÔN_NGỮ]. Dành cho đối tượng [ĐỐI_TƯỢNG].
```

**Thay thế tự động:**

```python
for k, v in {"[NGÔN_NGỮ]": "tiếng Việt", "[ĐỐI_TƯỢNG]": "sinh viên năm nhất"}.items():
    tpl = tpl.replace(k, v)
```

**Lợi ích:** một kiểu ngoặc nên thay đồng loạt không sót; viết hoa nên dễ nhận diện, còn `[` sót lại là biết biến chưa được thay.
