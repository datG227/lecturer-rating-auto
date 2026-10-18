# Auto Đánh Giá Giảng Viên

Bookmarklet tự động tick toàn bộ câu hỏi trong form đánh giá giảng viên. Chỉ cần click 1 cái, nhập captcha rồi submit — xong.

---

## Bookmarklet (paste vào URL của bookmark)

```
javascript:(function(){const groups={};document.querySelectorAll('input[type=radio]').forEach(r=>{if(!groups[r.name])groups[r.name]=[];groups[r.name].push(r);});const allGroups=Object.values(groups);allGroups.forEach((list,index)=>{if(index===allGroups.length-1){list[list.length-1]?.click();}else{list[0]?.click();}});document.querySelectorAll('textarea').forEach(t=>t.value='Em không có ý kiến gì ạ');window.scrollTo(0,document.body.scrollHeight);const cap=document.querySelector('input[type=text],input[name*=captcha]');if(cap)cap.focus();})();
```

---

## Hướng dẫn cài đặt

### Bước 1 — Hiện thanh bookmark

Nhấn `Ctrl + Shift + B` để bật/tắt thanh bookmark bar trong Chrome.

### Bước 2 — Thêm bookmark

1. Chuột phải vào thanh bookmark → chọn **Add new bookmark**
2. **Name**: đặt tên tuỳ ý
3. **URL**: xóa hết nội dung có sẵn, paste đoạn code ở trên vào
4. Nhấn **Save**

> Đoạn code bắt đầu bằng `javascript:` — phải giữ nguyên, không xóa.

---

## Cách dùng

1. Mở trang form đánh giá giảng viên
2. Click bookmark vừa tạo
3. Script tự động:
   - Tick tất cả câu radio = Tốt
   - Điền tất cả ô textarea = `Em không có ý kiến gì ạ`
   - Scroll xuống cuối và focus vào ô captcha
4. Nhập captcha → nhấn Gửi
5. Lặp lại cho giảng viên tiếp theo

---

## Giải thích code

```js
(function () {
    // Bước 1: Gom tất cả radio button theo từng nhóm (mỗi nhóm = 1 câu hỏi)
    const groups = {};
    document.querySelectorAll('input[type=radio]').forEach(r => {
        if (!groups[r.name]) groups[r.name] = [];
        groups[r.name].push(r);
    });

    // Bước 2: Tick từng nhóm
    const allGroups = Object.values(groups);
    allGroups.forEach((list, index) => {
        if (index === allGroups.length - 1) {
            // Câu cuối: chọn lựa chọn cuối
            list[list.length - 1]?.click();
        } else {
            // Các câu còn lại: chọn lựa chọn đầu tiên = Tốt
            list[0]?.click();
        }
    });

    // Bước 3: Điền textarea
    document.querySelectorAll('textarea').forEach(t => {
        t.value = 'Em không có ý kiến gì ạ';
    });

    // Bước 4: Scroll xuống cuối trang
    window.scrollTo(0, document.body.scrollHeight);

    // Bước 5: Focus vào ô nhập captcha
    const cap = document.querySelector('input[type=text],input[name*=captcha]');
    if (cap) cap.focus();
})();
```

---

## Lưu ý

- Captcha vẫn phải nhập tay
- Không tự động submit — vẫn phải bấm Gửi
- Không lưu hay gửi bất kỳ thông tin nào ra ngoài
