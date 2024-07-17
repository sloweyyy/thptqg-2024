# Phân tích điểm thi THPTQG Việt Nam năm 2024

## Giới thiệu

Dự án này nhằm mục đích trực quan hóa và tìm ra tổng điểm cao nhất của các khối thi khác nhau trong kỳ thi tốt nghiệp THPT quốc gia năm 2024. Bộ dữ liệu bao gồm điểm số của các môn học khác nhau, và mã tính tổng điểm cho mỗi khối thi, xác định học sinh có tổng điểm cao nhất, và trực quan hóa dữ liệu.

## Bộ dữ liệu

Bộ dữ liệu là một tệp CSV có tên `diem_thi_thpt_2024.csv`, bao gồm các cột sau:

-   `sbd` (Số báo danh)
-   `toan` (Toán)
-   `ngu_van` (Ngữ văn)
-   `ngoai_ngu` (Ngoại ngữ)
-   `vat_li` (Vật lý)
-   `hoa_hoc` (Hóa học)
-   `sinh_hoc` (Sinh học)
-   `lich_su` (Lịch sử)
-   `dia_li` (Địa lý)
-   `gdcd` (Giáo dục công dân)
-   `ma_ngoai_ngu` (Mã môn ngoại ngữ)

## Các khối thi

Các khối thi phổ biến bao gồm:

-   Khối A00: Toán, Vật lý, Hóa học
-   Khối A01: Toán, Vật lý, Tiếng Anh
-   Khối B: Toán, Hóa học, Sinh học
-   Khối C: Ngữ văn, Lịch sử, Địa lý
-   Khối D: Ngữ văn, Toán, Ngoại ngữ

Dự án cũng bao gồm các khối thi mở rộng như A02, A03, A04,..., D01, D02,...

```python
exam_blocks = {
    'A00': ['toan', 'vat_li', 'hoa_hoc'],
    'A01': ['toan', 'vat_li', 'ngoai_ngu'],
    'A02': ['toan', 'vat_li', 'sinh_hoc'],
    'A03': ['toan', 'vat_li', 'lich_su'],
    'A04': ['toan', 'vat_li', 'dia_li'],
    'A05': ['toan', 'hoa_hoc', 'lich_su'],
    'A06': ['toan', 'hoa_hoc', 'dia_li'],
    'A07': ['toan', 'lich_su', 'dia_li'],
    'A08': ['toan', 'lich_su', 'gdcd'],
    'A09': ['toan', 'dia_li', 'gdcd'],
    'A10': ['toan', 'vat_li', 'gdcd'],
    'A11': ['toan', 'hoa_hoc', 'gdcd'],
    'A12': ['toan', 'lich_su', 'hoa_hoc'],
    'A13': ['toan', 'lich_su', 'hoa_hoc'],
    'A14': ['toan', 'dia_li', 'hoa_hoc'],
    'A15': ['toan', 'gdcd', 'hoa_hoc'],
    'A16': ['toan', 'ngu_van', 'hoa_hoc'],
    'A17': ['toan', 'vat_li', 'lich_su'],
    'A18': ['toan', 'hoa_hoc', 'lich_su'],
    'B': ['toan', 'hoa_hoc', 'sinh_hoc'],
    'B01': ['toan', 'sinh_hoc', 'lich_su'],
    'B02': ['toan', 'sinh_hoc', 'dia_li'],
    'B03': ['toan', 'sinh_hoc', 'ngu_van'],
    'B04': ['toan', 'sinh_hoc', 'gdcd'],
    'B05': ['toan', 'sinh_hoc', 'lich_su'],
    'B06': ['toan', 'sinh_hoc', 'ngoai_ngu'],
    'C': ['ngu_van', 'lich_su', 'dia_li'],
    'C01': ['ngu_van', 'toan', 'vat_li'],
    'C02': ['ngu_van', 'toan', 'hoa_hoc'],
    'C03': ['ngu_van', 'toan', 'lich_su'],
    'C04': ['ngu_van', 'toan', 'dia_li'],
    'C05': ['ngu_van', 'vat_li', 'hoa_hoc'],
    'C06': ['ngu_van', 'vat_li', 'sinh_hoc'],
    'C07': ['ngu_van', 'vat_li', 'lich_su'],
    'C08': ['ngu_van', 'hoa_hoc', 'sinh_hoc'],
    'C09': ['ngu_van', 'vat_li', 'dia_li'],
    'C10': ['ngu_van', 'hoa_hoc', 'lich_su'],
    'D': ['ngu_van', 'toan', 'ngoai_ngu'],
    'D1': ['ngu_van', 'toan', 'ngoai_ngu'],
    'D2': ['ngu_van', 'toan', 'ngoai_ngu'],
    'D3': ['ngu_van', 'toan', 'ngoai_ngu'],
    'D4': ['ngu_van', 'toan', 'ngoai_ngu'],
    'D5': ['ngu_van', 'toan', 'ngoai_ngu'],
    'D6': ['ngu_van', 'toan', 'ngoai_ngu'],
    'D7': ['toan', 'hoa_hoc', 'ngoai_ngu'],
    'D08': ['toan', 'ngoai_ngu', 'sinh_hoc'],
    'D09': ['toan', 'ngoai_ngu', 'lich_su'],
    'D10': ['toan', 'ngoai_ngu', 'dia_li'],
}
```

## Hướng dẫn sử dụng

Để sử dụng dự án, bạn cần thực hiện các bước sau:

1. Tải dữ liệu: Đảm bảo rằng tệp dữ liệu `diem_thi_thpt_2024.csv` được đặt trong cùng thư mục với mã Python.

2. Chạy mã: Sử dụng Jupyter Notebook hoặc bất kỳ môi trường Python nào để chạy mã.

3. Thay đổi mã: Nếu bạn muốn thực hiện tính toán cho các khối thi khác nhau, bạn có thể chỉnh sửa biến `exam_blocks` trong mã Python để thêm hoặc loại bỏ các khối thi.

4. Chạy mã: Sau khi chỉnh sửa mã, hãy chạy lại mã để tính toán tổng điểm và trực quan hóa dữ liệu.

5. Xem kết quả: Kết quả tính toán và trực quan hóa dữ liệu sẽ được hiển thị trong môi trường chạy mã của bạn.
