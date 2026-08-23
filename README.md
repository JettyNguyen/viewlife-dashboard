[README.md](https://github.com/user-attachments/files/31356313/README.md)
# ViewLife Sales OS

Dashboard tĩnh, triển khai trực tiếp bằng GitHub Pages. Không cần build hoặc cài dependency.

## Deploy

1. Mở repository trên máy và kiểm tra `index.html`.
2. Commit và push lên nhánh đang được GitHub Pages sử dụng (thường là `main`).
3. Trong GitHub: **Settings → Pages → Deploy from a branch**, chọn nhánh và thư mục `/ (root)`.

## Data và backup

- Dữ liệu được lưu trong `localStorage` của trình duyệt; mỗi trình duyệt/thiết bị có bộ dữ liệu riêng.
- Dùng **Export backup** để tải JSON trước khi xóa cache hoặc đổi máy.
- Bản này dùng namespace mới `viewlife_sales_os_v31`, nên không ghi đè dữ liệu của dashboard cũ.

## Bitrix24

- Weekly Report được sinh tự động từ Activity, Opportunity và Order/PO.
- Khuyến nghị dùng **Download JSON payload** rồi chuyển payload qua Bitrix automation hoặc một serverless proxy.
- Không đưa webhook có secret vào source GitHub Pages. Nếu nhập webhook trong UI, URL chỉ được lưu trong trình duyệt hiện tại.
- Endpoint và `fields` cụ thể có thể cần đổi theo loại webhook Bitrix24 của công ty (`tasks.task.add`, CRM activity, hoặc workflow automation).

## Pricing v3.1 guardrails

Một order được đánh dấu exception nếu vi phạm bất kỳ điều kiện nào:

- Unit price thấp hơn floor price của Product Master.
- Discount cao hơn maximum discount của SKU.
- Gross margin thấp hơn ngưỡng governance (mặc định 10%).

Các exception xuất hiện trong Governance Dashboard và Weekly Report.
