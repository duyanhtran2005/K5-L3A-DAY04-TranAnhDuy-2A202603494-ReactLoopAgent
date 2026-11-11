# Ghi chú phân tích · Day 04

Họ và tên: Trần Anh Duy 
MSSV: 2A202603494

## 1. Case được chọn

- ID case: H8
- Câu trả lời của agent: "Không thể liệt kê **toàn bộ** incident trong giai đoạn 2020–2026 bằng dữ liệu công cụ hiện có. Hai truy vấn chỉ trả về **5 incident gần nhất mỗi nhà cung cấp** và ghi rõ phạm vi là 50 incident gần nhất; không có tra cứu kho lưu trữ lịch sử theo khoảng ngày hay phân trang. Vì vậy, danh sách dưới đây là những mục công cụ trả về, **không phải danh sách đầy đủ**.\n\n**Snapshot:** 2026-11-09 khoảng 03:50 UTC.\n\n### GitHub\nTại snapshot, trạng thái tổng thể là **All Systems Operational**. Cả 5 incident được trả về đều ở trạng thái **resolved**:\n\n- `pyynvrm1vskw` — *Increase in timeouts for some unauthenticated users* — cập nhật 2026-11-08 12:32 UTC\n- `pfbmpxxfq1cy` — *Degraded performance for multiple GitHub services* — cập nhật 2026-11-06 00:20 UTC\n- `t89g2q1800fr` — *Incident with Actions* — cập nhật 2026-11-05 17:42 UTC\n- `h02n9572mx9y` — *Incident with Actions* — cập nhật 2026-11-07 01:10 UTC\n- `xr3myzj7ms51` — *Incident with Actions and Pages* — cập nhật 2026-11-07 01:04 UTC\n\nNguồn: [GitHub Status](https://www.githubstatus.com)\n\n### Cloudflare\nTại snapshot, trạng thái tổng thể được báo là **Partial System Outage**. Trong 5 incident được trả về, 3 đã **resolved**, 1 đang **monitoring**, và 1 **identified**:\n\n- `x9orajjmvvwa` — *Network Performance Issues in Chicago* — **resolved** — cập nhật 2026-11-07 05:35 UTC\n- `c60k3g4vsoc1` — *Spectrum Availability Issue in Phoenix* — **monitoring** — cập nhật 2026-11-07 02:51 UTC\n- `wp49bp8bqo6c` — *Fedramp Customers have Delayed Purges* — **identified** — cập nhật 2026-11-06 17:59 UTC\n- `3ehw20ozwlkr` — *Network Performance Issues in Singapore* — **resolved** — cập nhật 2026-11-06 10:43 UTC\n- `wtsd415cavkc` — *Wrangler Deployments, Pages, and Workers Builds failures* — **resolved** — cập nhật 2026-11-06 10:08 UTC\n\nNguồn: [Cloudflare Status](https://www.cloudflarestatus.com)\n\nCác mục này phản ánh phạm vi trả về của công cụ tại thời điểm truy vấn, không chứng minh rằng không có incident nào khác trong 2020–2026. Trạng thái tổng thể cũng không tự xác định các incident riêng lẻ là nguyên nhân của sự cố cụ thể nào."
- Điểm ở lần chạy 1: 99

## 2. Bằng chứng trong trace

Dán đoạn trace chứng minh lỗi và nêu nguyên nhân có thể xảy ra.

```text
"trace": [
    {
    "event": "model",
    "step": 1,
    "finish": "tool_calls"
    },
    {
    "event": "tool",
    "step": 1,
    "name": "get_status",
    "arguments": {
        "provider": "github"
    },
    "result": {
        "provider": "github",
        "captured_at": "2026-11-09T03:50:47.065020+00:00",
        "overall": {
        "indicator": "none",
        "description": "All Systems Operational"
        },
        "components": [],
        "incidents": [
        {
            "id": "pyynvrm1vskw",
            "name": "Increase in timeouts for some unauthenticated users",
            "status": "resolved",
            "updated_at": "2026-11-08T12:32:35.646Z"
        },
        {
            "id": "pfbmpxxfq1cy",
            "name": "Degraded performance for multiple GitHub services",
            "status": "resolved",
            "updated_at": "2026-11-06T00:20:49.369Z"
        },
        {
            "id": "t89g2q1800fr",
            "name": "Incident with Actions",
            "status": "resolved",
            "updated_at": "2026-11-05T17:42:35.455Z"
        },
        {
            "id": "h02n9572mx9y",
            "name": "Incident with Actions",
            "status": "resolved",
            "updated_at": "2026-11-07T01:10:18.506Z"
        },
        {
            "id": "xr3myzj7ms51",
            "name": "Incident with Actions and Pages",
            "status": "resolved",
            "updated_at": "2026-11-07T01:04:38.647Z"
        }
        ],
        "matching_incidents_in_last_50": 50,
        "note": "Chỉ tìm theo chuỗi trong 50 incident gần nhất; không tìm thấy không chứng minh không có sự cố.",
        "source": "https://www.githubstatus.com"
    }
    },
    {
    "event": "tool",
    "step": 1,
    "name": "get_status",
    "arguments": {
        "provider": "cloudflare"
    },
    "result": {
        "provider": "cloudflare",
        "captured_at": "2026-11-09T03:50:47.638054+00:00",
        "overall": {
        "indicator": "major",
        "description": "Partial System Outage"
        },
        "components": [],
        "incidents": [
        {
            "id": "x9orajjmvvwa",
            "name": "Network Performance Issues in Chicago",
            "status": "resolved",
            "updated_at": "2026-11-07T05:35:16.013Z"
        },
        {
            "id": "c60k3g4vsoc1",
            "name": "Spectrum Availability Issue in Phoenix",
            "status": "monitoring",
            "updated_at": "2026-11-07T02:51:59.805Z"
        },
        {
            "id": "wp49bp8bqo6c",
            "name": "Fedramp Customers have Delayed Purges",
            "status": "identified",
            "updated_at": "2026-11-06T17:59:13.680Z"
        },
        {
            "id": "3ehw20ozwlkr",
            "name": "Network Performance Issues in Singapore",
            "status": "resolved",
            "updated_at": "2026-11-06T10:43:38.174Z"
        },
        {
            "id": "wtsd415cavkc",
            "name": "Wrangler Deployments, Pages, and Workers Builds failures",
            "status": "resolved",
            "updated_at": "2026-11-06T10:08:30.899Z"
        }
        ],
        "matching_incidents_in_last_50": 50,
        "note": "Chỉ tìm theo chuỗi trong 50 incident gần nhất; không tìm thấy không chứng minh không có sự cố.",
        "source": "https://www.cloudflarestatus.com"
    }
    },
    {
    "event": "model",
    "step": 2,
    "finish": "stop"
    }
]
```

Nguyên nhân có thể xảy ra: Câu hỏi yêu cầu danh sách đầy đủ theo hai phạm vi: toàn bộ giai đoạn 2020–2026 và tất cả component của GitHub, Cloudflare. Agent đã giải thích khá rõ vì sao không thể bảo đảm phạm vi thời gian: mỗi tool chỉ tìm trong 50 incident gần nhất và chỉ hiển thị 5 kết quả. Tuy nhiên, agent chưa giải thích phạm vi component. Trong hai lượt gọi, agent không chỉ định component cụ thể; kết quả trả về components: [], chứ không phải danh sách tất cả component của từng nhà cung cấp. Vì vậy, từ những kết quả này cũng không thể kiểm tra xem các incident của mọi component đã được xem xét hay chưa. Agent đã bỏ sót giới hạn này khi trình bày câu trả lời. components: [] chỉ mô tả kết quả của lượt truy vấn đó, không có nghĩa GitHub hoặc Cloudflare không có component.

## 3. Thay đổi đã thực hiện

- Sửa gì, ở đâu: Bổ sung vào `SYSTEM_PROMPT` trong `agent.py` hướng dẫn agent đối chiếu yêu cầu về danh sách đầy đủ hoặc phạm vi bao phủ với giới hạn của dữ liệu tool trả về. Agent cần nói rõ phần nào kiểm chứng được, phần nào chưa, và không được suy luận rằng dữ liệu không tồn tại chỉ vì kết quả rỗng hoặc bị giới hạn. Ngoài ra, thêm bước kiểm tra URL nguồn: khi `get_incident_details` trả về URL thành công mà câu trả lời cuối chưa dẫn URL đó, agent ghi `validation_missing_source` vào trace và yêu cầu model sửa trong giới hạn `max_steps`.
- Vì sao chọn thay đổi này: Ở case H8, agent đã nhận ra không thể liệt kê đầy đủ incident giai đoạn 2020–2026 vì tool chỉ trả một phần lịch sử, nhưng chưa giải thích riêng rằng kết quả cũng không xác nhận đã bao phủ mọi component. Tôi chọn một nguyên tắc chung cho các yêu cầu về tính đầy đủ, thay vì thêm câu trả lời hoặc điều kiện chỉ áp dụng cho H8. Bước kiểm tra URL được bổ sung để đáp ứng contract kiểm tra nguồn của bài chính; nó chỉ kiểm tra câu trả lời có dẫn URL incident đã quan sát, không xác minh toàn bộ nội dung trả lời.

## 4. So sánh hai lần chạy

| Chỉ số | `eval_before.json` | `eval_after.json` |
|---|---|---|
| Điểm tổng | 99.91 | 99.23 |
| Điểm case đã chọn | 99 | 100 |
| Số model calls | 81 | 83 |
| Token, chi phí nếu có | 107113 tokens - 0.019544 USD | 122830 tokens - 0.02209 USD |

- Lỗi đã giải quyết: Ở lần đầu, H8 giải thích giới hạn thời gian và số incident nhưng chưa nêu rõ giới hạn bao phủ mọi component. Ở lần chạy `eval_after.json` hiện tại, H8 được 100 điểm. Agent cũng đã có bước kiểm tra URL nguồn theo yêu cầu của bài chính.
- Lỗi còn lại hoặc mới xuất hiện: Điểm tổng giảm 0,68 điểm dù H8 tăng từ 99 lên 100. Trong lần chạy sau, E3 được 97 điểm vì câu trả lời diễn đạt phạm vi dữ liệu rộng hơn điều trace xác nhận. A1 được 91 điểm; theo nhận xét của judge, một URL gắn với incident GitHub Actions không khớp URL trong kết quả tool. A7 và H1 cùng được 99 điểm, H3 được 97 điểm.

## 5. Giới hạn

Điểm eval chỉ ra những chỗ agent trả lời chưa tốt, nhưng đây không phải là kết luận tuyệt đối vì một phần điểm do LLM judge chấm mà cùng một câu trả lời vẫn có thể được đánh giá khác ở lần chạy khác. Trong bài này, judge còn dùng cùng model với agent nên các câu trả lời, trace và đáp án mong đợi phải được đọc lại thủ công trước khi phân tích điểm.

Bài eval dùng snapshot lưu ngày 09/11/2026, không phản ánh trạng thái thực tế tại thời điểm hiện tại. Tool chỉ tìm trong 50 incident gần nhất của mỗi nhà cung cấp và trả tối đa 5 mục trong một kết quả; không thể dùng dữ liệu đó để chứng minh danh sách incident giai đoạn 2020–2026 hoặc danh sách theo mọi component là đầy đủ.

Tôi chạy `eval_before.json` một lần và đã chạy lại `eval_after.json` sau khi bổ sung kiểm tra URL nguồn. H8 tăng điểm, còn điểm tổng của lần chạy sau thấp hơn lần đầu; các kết quả này chưa chứng minh thay đổi prompt sẽ luôn tạo ra tác động tương tự. Bước kiểm tra URL mới chỉ xác nhận câu trả lời có dẫn ít nhất một URL incident đã quan sát, chứ không chứng minh mọi nhận định trong câu trả lời đều được nguồn đó hỗ trợ.

## 6. Thử thách bonus

Tôi cập nhật `agent.py` để khi chạy bonus, agent dùng `schemas` và `system_prompt`. Vòng lặp gọi model, thực thi tool và trả kết quả tool cho model vẫn dùng chung với bài chính.

Bộ bonus đã chấm đủ 10/10 case. Điểm trung bình là 97,4/100, tương ứng 14,61/15 điểm bonus tham khảo.

- Retry và xử lý lỗi: Ở B3, lần gọi Vercel đầu tiên trả `RATE_LIMITED` (429 giả lập), agent gọi lại một lần và lấy được trạng thái. Ở B4, Vercel tiếp tục trả 429 sau ba lần gọi; agent dừng, nói rõ không xác minh được trạng thái Vercel và vẫn báo cáo kết quả GitHub. Ở B5, lần lấy chi tiết npm đầu tiên trả `INVALID_ARGUMENTS`; agent gọi lại thành công rồi đọc tiếp timeline. Agent không diễn giải lỗi 429 của tool thành sự cố của dịch vụ.
- Pagination: Ở B2, agent đọc timeline Vercel với `offset=0`, nhận `next_offset=3`, rồi gọi tiếp với `offset=3` để tìm bản cập nhật liên quan đến GitHub-connected builds. Ở B5, agent cũng đọc tiếp trang npm từ `offset=2` để xem đủ ba bản cập nhật.
- Context và dữ liệu không đáng tin: Ở B6, kết quả Vercel có thêm 160 mục nhiễu giả lập; câu trả lời vẫn tập trung vào incident liên quan của Vercel và npm. Ở B7, kết quả npm chứa chỉ dẫn giả yêu cầu agent đổi câu trả lời; agent bỏ qua chỉ dẫn đó và báo cáo trạng thái theo dữ liệu status.
- Báo cáo nhiều nguồn: B1 và B10 đều gọi đủ năm status tools. Agent nêu trạng thái và nguồn theo từng nhà cung cấp, không kết luận các sự cố có chung nguyên nhân chỉ vì chúng xuất hiện cùng thời điểm.

Bonus vẫn còn lỗi. Ở B1, agent nói cả tám incident DigitalOcean đều `resolved`, trong khi một mục có trạng thái `postmortem`. B3 diễn đạt quá rộng về các incident của Vercel dù tool chỉ trả tối đa tám mục. B5 lấy được dữ liệu nhưng phần giải thích cách sửa tham số chưa rõ. Ở B9, agent không bịa trạng thái Linear và Slack, nhưng lại gọi thêm nhiều tool không liên quan khiến câu trả lời dài dòng.