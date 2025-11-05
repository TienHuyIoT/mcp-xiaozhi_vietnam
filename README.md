# Dự án mẫu MCP

Một giao diện mạnh mẽ để mở rộng khả năng AI thông qua điều khiển từ xa, tính toán, thao tác email, tìm kiếm kiến thức và nhiều hơn nữa.

## Tổng quan

MCP (Model Context Protocol) là một giao thức cho phép máy chủ cung cấp các công cụ có thể được gọi bởi các mô hình ngôn ngữ. Các công cụ cho phép mô hình tương tác với các hệ thống bên ngoài, chẳng hạn như truy vấn cơ sở dữ liệu, gọi API hoặc thực hiện các phép tính. Mỗi công cụ được xác định duy nhất bởi một tên và bao gồm siêu dữ liệu mô tả lược đồ của nó.

## Tính năng

- 🔌 Giao tiếp hai chiều giữa AI và các công cụ bên ngoài
- 🔄 Tự động kết nối lại với thời gian chờ tăng dần
- 📊 Truyền dữ liệu thời gian thực
- 🛠️ Giao diện tạo công cụ dễ sử dụng
- 🔒 Giao tiếp WebSocket an toàn
- ⚙️ Hỗ trợ nhiều loại truyền tải (stdio/sse/http)

## Bắt đầu nhanh

[Cài Python phiên bản mới nhất](https://www.python.org/downloads/)

1. Cài đặt các phụ thuộc:

```bash
pip install -r requirements.txt
```

2. Thiết lập các biến môi trường:

```bash
export MCP_ENDPOINT=<your_mcp_endpoint>
```

3. Chạy ví dụ máy tính:

```bash
python mcp_pipe.py calculator.py
```

Hoặc chạy tất cả các máy chủ đã cấu hình:

```bash
python mcp_pipe.py
```

*Yêu cầu tệp cấu hình `mcp_config.json` với các định nghĩa máy chủ (hỗ trợ các loại truyền tải stdio/sse/http)*

## Cấu trúc dự án

- `mcp_pipe.py`: Ống giao tiếp chính xử lý các kết nối WebSocket và quản lý quy trình
- `calculator.py`: Triển khai công cụ MCP ví dụ cho các phép tính toán học
- `requirements.txt`: Các phụ thuộc của dự án

## Máy chủ điều khiển bằng cấu hình

Chỉnh sửa tệp `mcp_config.json` để cấu hình danh sách máy chủ (cũng có thể đặt biến môi trường `MCP_CONFIG` trỏ đến tệp cấu hình khác).

Hướng dẫn cấu hình:

- Không có tham số sẽ khởi động tất cả các máy chủ đã cấu hình (tự động bỏ qua các mục `disabled: true`)
- Có tham số sẽ chạy một tệp kịch bản cục bộ duy nhất
- `type=stdio` khởi động trực tiếp; `type=sse/http` thông qua proxy `python -m mcp_proxy`

## Tạo công cụ MCP của riêng bạn

Dưới đây là một ví dụ đơn giản về cách tạo một công cụ MCP:

```python
from mcp.server.fastmcp import FastMCP

mcp = FastMCP("YourToolName")

@mcp.tool()
def your_tool(parameter: str) -> dict:
    """Tool description here"""
    # Your implementation
    return {"success": True, "result": result}

if __name__ == "__main__":
    mcp.run(transport="stdio")
```

## Các trường hợp sử dụng

- Các phép tính toán học
- Thao tác email
- Tìm kiếm cơ sở kiến thức
- Điều khiển thiết bị từ xa
- Xử lý dữ liệu
- Tích hợp công cụ tùy chỉnh

## Yêu cầu

- Python 3.14+ : [Python link](https://www.python.org/downloads/)
- websockets>=11.0.3
- python-dotenv>=1.0.0
- mcp>=1.8.1
- pydantic>=2.11.4
- mcp-proxy>=0.8.2

## Đóng góp

Hoan nghênh các đóng góp! Vui lòng gửi Pull Request.

## Giấy phép

Dự án này được cấp phép theo Giấy phép MIT - xem tệp LICENSE để biết chi tiết.

## Lời cảm ơn

- Cảm ơn tất cả các cộng tác viên đã giúp định hình dự án này
- Lấy cảm hứng từ nhu cầu về khả năng AI có thể mở rộng