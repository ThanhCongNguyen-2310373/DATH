# Đồ Án - Sentiment Analysis

## Cấu trúc thư mục

```
DATH/
├── main.tex              # File LaTeX chính
├── CHUONG_1.tex          # Chương 1: Giới thiệu
├── CHUONG_2.tex          # Chương 2: Cơ sở lý thuyết
├── CHUONG_3.tex          # Chương 3: Phương pháp thực hiện
├── CHUONG4.tex           # Chương 4: Kết quả thực nghiệm
├── CHUONG5.tex           # Chương 5: Kết luận
├── CHUONG6.tex           # Chương 6: Tài liệu tham khảo
├── references.bib        # Database tài liệu tham khảo
├── hcmut.png            # Logo HCMUT
└── Images/              # Thư mục chứa hình ảnh
    ├── 4_1.png
    ├── 4_2.png
    └── ...
```

## Hướng dẫn biên dịch (Compile)

### Phương pháp 1: Sử dụng lệnh đơn giản

```bash
cd DATH
pdflatex -shell-escape -interaction=nonstopmode main.tex
bibtex main
pdflatex -shell-escape -interaction=nonstopmode main.tex
pdflatex -shell-escape -interaction=nonstopmode main.tex
```

### Phương pháp 2: Sử dụng script tự động (Windows PowerShell)

Tạo file `compile.ps1`:

```powershell
# compile.ps1
cd DATH

Write-Host "Compiling LaTeX document..." -ForegroundColor Green

# First pass
Write-Host "[1/4] First pdflatex pass..." -ForegroundColor Yellow
pdflatex -shell-escape -interaction=nonstopmode main.tex

# Generate bibliography
Write-Host "[2/4] Running bibtex..." -ForegroundColor Yellow
bibtex main

# Second pass (incorporate bibliography)
Write-Host "[3/4] Second pdflatex pass..." -ForegroundColor Yellow
pdflatex -shell-escape -interaction=nonstopmode main.tex

# Third pass (resolve cross-references)
Write-Host "[4/4] Third pdflatex pass..." -ForegroundColor Yellow
pdflatex -shell-escape -interaction=nonstopmode main.tex

Write-Host "Done! PDF generated: main.pdf" -ForegroundColor Green
```

Chạy script:
```bash
powershell -ExecutionPolicy Bypass -File compile.ps1
```

### Phương pháp 3: Sử dụng script bash (Linux/MacOS)

Tạo file `compile.sh`:

```bash
#!/bin/bash

echo "Compiling LaTeX document..."

# First pass
echo "[1/4] First pdflatex pass..."
pdflatex -shell-escape -interaction=nonstopmode main.tex

# Generate bibliography
echo "[2/4] Running bibtex..."
bibtex main

# Second pass
echo "[3/4] Second pdflatex pass..."
pdflatex -shell-escape -interaction=nonstopmode main.tex

# Third pass
echo "[4/4] Third pdflatex pass..."
pdflatex -shell-escape -interaction=nonstopmode main.tex

echo "Done! PDF generated: main.pdf"
```

Chạy script:
```bash
chmod +x compile.sh
./compile.sh
```

## Chi tiết các bước biên dịch

1. **First pdflatex pass**: Tạo file `.aux` chứa thông tin về citations và labels
2. **bibtex**: Xử lý references từ `references.bib` và tạo file `.bbl`
3. **Second pdflatex pass**: Incorporate bibliography vào document
4. **Third pdflatex pass**: Resolve tất cả cross-references và page numbers

## Tùy chọn biên dịch

- `-shell-escape`: Cho phép chạy external commands (cần thiết cho minted package)
- `-interaction=nonstopmode`: Tự động skip các lỗi và tiếp tục compile

## Xử lý lỗi thường gặp

### Lỗi: "I can't write on file `main.pdf`"

**Nguyên nhân**: File PDF đang được mở bởi PDF reader

**Giải pháp**:
```powershell
# Đóng PDF reader
taskkill /F /IM AcroRd32.exe
taskkill /F /IM Acrobat.exe
# Hoặc đóng thủ công PDF reader, sau đó compile lại
```

### Lỗi: "Package minted Error"

**Nguyên nhân**: Thiếu Python hoặc Pygments

**Giải pháp** (optional, code vẫn hiển thị nhưng không có syntax highlighting):
```bash
pip install Pygments
```

### Lỗi: "Undefined citations"

**Nguyên nhân**: Chưa chạy bibtex hoặc chưa compile đủ số lần

**Giải pháp**: Chạy đầy đủ 4 bước như hướng dẫn trên

## File output

Sau khi compile thành công, các file sau sẽ được tạo:

- `main.pdf` - **File PDF chính (kết quả cuối cùng)**
- `main.aux` - Auxiliary file
- `main.bbl` - Bibliography data
- `main.blg` - Bibliography log
- `main.log` - Compilation log
- `main.toc` - Table of Contents
- `main.lof` - List of Figures
- `main.lot` - List of Tables
- `main.out` - Hyperref outline

## LaTeX Packages sử dụng

- `minted` - Syntax highlighting cho code
- `vntex` - Hỗ trợ tiếng Việt
- `hyperref` - Hyperlinks và bookmarks
- `tikz` - Vẽ diagrams
- `algorithm2e` - Định dạng algorithms
- `cite` - Quản lý citations
- `graphicx` - Chèn images
- `amsmath` - Công thức toán học

## License

Copyright © 2024-2025. All rights reserved.
