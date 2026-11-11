# Team

## Thông tin nhóm

- Tên nhóm: Hehehe
- Lớp: L3B.
- Repo nhóm: `K5-L3B-DAY03-Hehehe-ResearchAgentToolEval`.
- URL repo: https://github.com/trongnghia2304/K5-L3B-DAY03-Hehehe-ResearchAgentToolEval
- Nền tích hợp: main GitHub `a557a55`; CP5 bổ sung trên nhánh `vuvanbinh`.
- Nhánh nộp: `main`. Commit chốt: `3bd3c24` (merge PR #6, đã gộp CP5 vào main; đủ CP1–CP5). Các commit sau commit này chỉ cập nhật tài liệu.

## Thành viên

| STT | Họ tên | MSSV | Email | GitHub | Vai trò |
| --: | ------ | ---- | ----- | ------ | ------- |
| 1 | Vũ Văn Bình | 2A202603831 | binhvuvan2004@gmail.com | hnib1908 | CP1: setup/baseline; CP5: UI, live chat, báo cáo và kiểm tra tích hợp với hỗ trợ Codex |
| 2 | Nguyễn Nghiêm Khánh Tiệp | 2A202603863 | tiepnnk04@gmail.com | tiepnnk01-10 | CP2: tối ưu system prompt và tool declaration (v1–v3), version log, bảng B1 |
| 3 | Trần Thị Hà Anh | 2A202603887 | anhtth.it.work@gmail.com | hnha02 | CP3: phát triển 4 tool mới, unit test, eval routing |
| 4 | Nguyễn Trọng Nghĩa | 2A202603835 | nghiatrongnguyen2304@gmail.com | trongnghia2304 | CP4: viết 10 eval case nhóm, chạy suite group, bảng B3; hỗ trợ CP5: phỏng vấn người dùng ngoài nhóm, ghi kết quả vào A1/B4 |

Thông tin Bình đã được Bình xác nhận trong phiên hoàn thiện CP5; các thành viên khác giữ theo main GitHub.

## Vũ Văn Bình — 2A202603831

### Phần việc phụ trách

- Cấu hình provider OpenAI, kiểm tra môi trường và chạy baseline v0.
- Tổng hợp version log, phân tích lỗi và báo cáo CP1 với hỗ trợ của Codex.
- CP5: hoàn thiện UI/live chat, hướng dẫn, hồ sơ và báo cáo tích hợp.

### Đóng góp cụ thể

- Chạy preflight với OpenAI và xác nhận model `gpt-4o-mini` theo kết quả Terminal đã trao đổi.
- Chạy pytest: 62 passed, 17 skipped, 0 failed.
- Chạy base eval v0: 20 case được đo, 14 pass, không có lỗi provider.
- Nhờ Codex đối chiếu run JSON, ghi version log và soạn phân tích 6 case lỗi. Codex chạy lại pytest offline và lưu output; chưa áp dụng thay đổi v1.
- Trong CP5, Codex trực tiếp triển khai UI trên main `a557a55`, dùng đủ 14 tool và giữ các phần CP2–CP4 của nhóm. Bản local tự thử trước đó được giữ riêng trong stash, không dùng thay bài nhóm.
- Kiểm tra mới: pytest 102 passed, 14 skipped, 0 failed; base 17/20 và group 10/10, đều 0 provider errors. Transcript CLI mới có 5 lượt qua API/tool thật, gồm hỏi thiếu tài khoản, bổ sung và hủy gửi.


### Bằng chứng

- [Run v0](starter_v0/runs/v0_B_base_openai_20261110T180441850646.json).
- [Version log](starter_v0/artifacts/version_log.csv).
- [Output pytest được Codex chạy lại](starter_v0/analysis/cp1_pytest.txt).
- [Báo cáo nhóm](report/team/group_report.md), mục B1 và B2.
- [Báo cáo cá nhân](report/team/2A202603831_VuVanBinh.md).
- [UI](starter_v0/app.py), [hướng dẫn](docs/UI-GUIDE.md), [QA CP5](starter_v0/analysis/cp5_team_qa.md).
- Commit CP1: `fcbfc64` (author `hnib1908`). CP5: lịch sử nhánh `codex/complete-team-main`; cần nhóm review trước khi chốt nộp.

## Nguyễn Nghiêm Khánh Tiệp — 2A202603863

### Phần việc phụ trách

- CP2: tối ưu `system_prompt.md` và `tools.yaml` qua 3 version (v1, v2, v3), mỗi version kiểm chứng một giả thuyết và chạy lại base eval (20 case, OpenAI `gpt-4o-mini`).
- Ghi `artifacts/version_log.csv` cho v1–v3 và điền bảng B1 cùng phân tích từng case trong báo cáo nhóm.
- Hỗ trợ CP1: chạy preflight và một lần base eval v0 để kiểm tra setup.

### Đóng góp cụ thể

- v1 (`system_prompt.md`): bỏ 3 chỉ dẫn xấu của starter, thêm rule clarify/xác nhận trước khi `send` — `case_accuracy` 0.70 → 0.90 (sửa R10, R11).
- v2 (`system_prompt.md`): thêm khối Routing rules — `case_accuracy` 0.95, `tool_routing_accuracy` và `multiturn_accuracy` đạt 1.00; sửa regression M02 của v1.
- v3 (`tools.yaml`): viết lại description 10 tool và convention args — 0.85, giả thuyết bị bác bỏ (R12 vẫn FAIL, regression R10 và M03); đã phân tích nguyên nhân regression.
- Chạy `pytest tests/test_tool_contract.py` (55 passed) sau khi sửa `tools.yaml`; chỉ dùng run có `provider_error_cases == 0`.
- Ghi nhận giới hạn chấm tự động (R08/R14) và độ dao động giữa các lần chạy (v0 chạy lại 0.65 so với 0.70).

### Bằng chứng

- Run: [v1](starter_v0/runs/v1_B_base_openai_20261110T184506774099.json), [v2](starter_v0/runs/v2_B_base_openai_20261110T185439904664.json), [v3](starter_v0/runs/v3_B_base_openai_20261110T190328305130.json).
- [Version log](starter_v0/artifacts/version_log.csv): dòng v1, v2, v3.
- Bảng B1 và các mục "Chi tiết v1/v2/v3" trong [báo cáo nhóm](report/team/group_report.md).
- Commit `252da65` (Complete CP2: v1, v2, v3); PR #1, merge commit `e1ff04e`.
- Báo cáo cá nhân: [`report/team/2A202603863_NguyenNghiemKhanhTiep.md`](report/team/2A202603863_NguyenNghiemKhanhTiep.md).

## Trần Thị Hà Anh — 2A202603887

### Phần việc phụ trách

- Phụ trách CP3: xây dựng tool mới và unit test cho research agent.
- Hoàn thiện tool bắt buộc `github_search` và eval case kiểm tra routing/arguments.
- Thực hiện bonus ≥4 tool tự viết với `deduplicate_sources`, `compare_sources` và `filter_by_date`.
- Đăng ký tool trong `TOOL_FUNCTIONS`, khai báo schema trong `artifacts/tools.yaml` và cập nhật bằng chứng CP3/bonus trong báo cáo nhóm.

### Đóng góp cụ thể

- Viết code và `TOOL.md` cho bốn tool: `github_search`, `deduplicate_sources`, `compare_sources`, `filter_by_date`.
- Viết 12 unit test cho happy path, input xấu và failure path; mock HTTP GitHub để toàn bộ kiểm thử chạy offline.
- Chạy toàn bộ suite: 97 passed, 14 skipped, 0 failed; các test skip là challenge tùy chọn của tool starter.
- Thêm case `G01_github_repository_routing` vào `starter_v0/data/eval_group.json`.
- Hỗ trợ đưa run baseline `v0_B_base_openai_20261110T180640602946.json` vào repo.

### Bằng chứng

- Các commit `ff72034`, `21e9423`, `64abe65`, `fa038dc`; PR #2, merge commit `96196bd`.
- `starter_v0/tools/{github_search,deduplicate_sources,compare_sources,filter_by_date}/`.
- `starter_v0/tests/test_tools_todo.py`, `starter_v0/analysis/cp3_pytest.txt`.
- Báo cáo cá nhân: `report/team/2A202603887_TranThiHaAnh.md`.

## Nguyễn Trọng Nghĩa — 2A202603835

### Phần việc phụ trách

- CP4: viết bộ eval nhóm 10 case trong `starter_v0/data/eval_group.json`, chạy `--suite group` bằng provider thật và điền bảng B3.
- Hỗ trợ CP5: nhờ người ngoài nhóm dùng thử UI, phỏng vấn sau buổi thử và ghi kết quả vào A1, B4 của báo cáo nhóm.

### Đóng góp cụ thể

- Giữ case G01 của CP3 và viết thêm 9 case (G02–G10): tổng 5 single turn + 5 multi turn, mỗi case có `failure_type`, `expect`, `metadata.what_it_tests`.
- Phủ cả 4 tool mới của CP3 (`github_search`, `deduplicate_sources`, `filter_by_date`, `compare_sources`) và luồng xác nhận trước khi `send` (G04, G09).
- Validate schema bằng code của `run_eval.py`; `pytest` 97 passed, 14 skipped, 0 failed.
- Chạy suite group với OpenAI `gpt-4o-mini`: 10/10 case được đo, `provider_error_cases=0`, 10/10 PASS.
- Điền bảng B3 trong báo cáo nhóm, ghi chú lý do `prompt_hash`/`tools_hash` khác dòng v3.
- Tổ chức buổi thử UI với Minh (lớp L3B, ngoài nhóm) ngày 11/11/2026: 5 câu mẫu ở A3 và 2 câu Minh tự hỏi; phỏng vấn 9 câu (dễ dùng, đúng ý, hỏi lại, xác nhận gửi, tốc độ, hiển thị tool, điểm 4/5 và góp ý).
- Đối chiếu nhận xét với transcript 9 lượt: phát hiện câu 4 agent đoán handle giả trước khi `clarify` (người thử không thấy trên UI), query arXiv quá rộng, fetch link Gmail không cảnh báo. Ghi vào A1, B4 và tick mục người ngoài nhóm thử trong `README.md`.

### Bằng chứng

- [`starter_v0/data/eval_group.json`](starter_v0/data/eval_group.json).
- [Run group v3](starter_v0/runs/v3_B_group_openai_20261110T193821499328.json).
- Bảng B3 trong [báo cáo nhóm](report/team/group_report.md).
- Báo cáo cá nhân: [`report/team/2A202603835_NguyenTrongNghia.md`](report/team/2A202603835_NguyenTrongNghia.md).
- Commit `5d09b27` (nhánh `feat/check-point-4`); PR #3, merge commit `9fc3ddd`.
- Phỏng vấn người dùng: [transcript UI của Minh](starter_v0/transcripts/cp5-team-ui_3f8ee7106ccf40ce9046f9521ed981c3.transcript.json); mục A1 và B4 ("Người ngoài nhóm dùng thử") trong [báo cáo nhóm](report/team/group_report.md); commit: bổ sung hash sau khi commit.
