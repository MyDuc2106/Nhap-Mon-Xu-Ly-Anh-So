# Nhập Môn Xử Lý Ảnh Số - Lab 3  
**Bộ Lọc Không Gian (Spatial Filtering)**

## Mục Tiêu Bài Lab

Lab 3 tập trung vào các kỹ thuật **lọc không gian** trong xử lý ảnh xám nhằm:
- Làm mịn (blur) ảnh để giảm nhiễu.
- Làm sắc nét (sharpen) ảnh để nhấn mạnh chi tiết và biên.
- Hiểu và áp dụng các mặt nạ lọc như trung bình, Gaussian, Laplacian và Sobel.
## Các Phép Lọc Thực Hiện

### 1. Lọc Trung Bình (Mean Filter)

- Làm mịn ảnh bằng cách tính trung bình giá trị pixel trong vùng lân cận.
- Giảm nhiễu, nhưng làm mờ biên ảnh.

```python
kernel = np.ones((3, 3), np.float32) / 9
blurred = cv2.filter2D(img, -1, kernel)
```

---

### 2. Lọc Gaussian

- Sử dụng hàm phân phối chuẩn để tính trọng số cho các pixel lân cận.
- Giữ được biên ảnh tốt hơn lọc trung bình.

```python
gauss = cv2.GaussianBlur(img, (5, 5), 1)
```

---

### 3. Lọc Trung Vị (Median Filter)

- Thay mỗi pixel bằng giá trị trung vị của vùng lân cận.
- Rất hiệu quả trong việc loại bỏ nhiễu muối tiêu (salt-and-pepper).

```python
median = cv2.medianBlur(img, 3)
```

---

### 4. Lọc Laplacian (Làm Sắc Nét)

- Dựa trên đạo hàm bậc hai để làm nổi bật các vùng thay đổi cường độ mạnh.

```python
lap = cv2.Laplacian(img, cv2.CV_64F)
lap = cv2.convertScaleAbs(lap)
```

---

### 5. Lọc Sobel (Phát Hiện Biên)

- Phát hiện biên theo hướng ngang (x) và dọc (y).

```python
sobelx = cv2.Sobel(img, cv2.CV_64F, 1, 0, ksize=3)
sobely = cv2.Sobel(img, cv2.CV_64F, 0, 1, ksize=3)
sobel = cv2.magnitude(sobelx, sobely)
sobel = cv2.convertScaleAbs(sobel)
```

---

## Cấu Trúc Dự Án

```
📦 lab3-spatial-filtering
├── lythuyet.ipynb       # Nội dung lý thuyết và mô tả các bộ lọc
├── baitapTH.ipynb       # Bài tập thực hành và minh hoạ kết quả
├── input.png            # Ảnh đầu vào (có thể thay đổi tuỳ ý)
├── README.md            # Tài liệu mô tả chi tiết bài lab
```


## Ghi Chú

- Lọc trung bình & Gaussian làm ảnh mờ, thích hợp xử lý nhiễu nhẹ.
- Lọc Laplacian & Sobel làm sắc nét và phát hiện biên, nhưng dễ bị nhiễu ảnh hưởng.
- Kết hợp các kỹ thuật lọc có thể tạo ra pipeline xử lý ảnh hiệu quả hơn.

---

## Tài Liệu Tham Khảo

- Gonzalez & Woods, *Digital Image Processing*
- [OpenCV Docs](https://docs.opencv.org/)
- [NumPy Docs](https://numpy.org/doc/)
