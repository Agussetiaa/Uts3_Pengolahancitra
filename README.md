# Uas3_Pengolahancitra


| Nama  |  Nim | Kelas |
| ------------- | ------------- |------------- |
| Agus Setiawan  | 312210193 | TI 22 A2 |



## Project Web App untuk memanipulasi gambar citra menggunakan Streammlite dengan mengubah 
#### - RGB menjadi HSV
#### - Menghitung Histogram
#### - Brignest dan Contras
#### - Contour

### Kita harus menginstal library yang diperlukan, yaitu Streamlit untuk membuat aplikasi web, OpenCV untuk manipulasi citra, dan Matplotlib untuk menampilkan histogram.

```
pip install streamlit opencv-python matplotlib numpy
```

### Buat file Python (misalnya app.py) dan impor library.

```
import streamlit as st
import cv2
from matplotlib import pyplot as plt
import numpy as np
```

### Membuat Fungsi Manipulasi Citra, untuk 'Konversi RGB ke HSV'

```
def convert_rgb_to_hsv(image):
    return cv2.cvtColor(image, cv2.COLOR_RGB2HSV)
```

### Menghitung Histogram

```
def plot_histogram(image):
    color = ('b', 'g', 'r')
    for i, col in enumerate(color):
        hist = cv2.calcHist([image], [i], None, [256], [0, 256])
        plt.plot(hist, color=col)
        plt.xlim([0, 256])
    plt.title('Histogram')
    return plt
```

### Mengatur Brightness dan Contrast

```
def adjust_brightness_contrast(image, brightness=0, contrast=0):
    new_image = np.zeros(image.shape, image.dtype)
    alpha = contrast * 0.01
    beta = brightness

    # Adjustment made here
    for y in range(image.shape[0]):
        for x in range(image.shape[1]):
            for c in range(image.shape[2]):
                new_image[y,x,c] = np.clip(alpha*image[y,x,c] + beta, 0, 255)
    
    return new_image
```

### Mendeteksi Kontur

```
def find_contours(image):
    gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
    blurred = cv2.GaussianBlur(gray, (5, 5), 0)
    edged = cv2.Canny(blurred, 50, 150)
    contours, _ = cv2.findContours(edged.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
    image_with_contours = image.copy()
    cv2.drawContours(image_with_contours, contours, -1, (0, 255, 0), 3)
    return image_with_contours
```

### Langkah Selanjutnya Streamlit Interface

```
st.title('Image Manipulation App')

uploaded_file = st.file_uploader("Choose an image...", type=["jpg", "jpeg", "png"])
if uploaded_file is not None:
    file_bytes = np.asarray(bytearray(uploaded_file.read()), dtype=np.uint8)
    image = cv2.imdecode(file_bytes, cv2.IMREAD_COLOR)

    st.image(image, caption='Original Image', use_column_width=True)

    if st.button('Convert RGB to HSV'):
        hsv_image = convert_rgb_to_hsv(image)
        st.image(hsv_image, caption='HSV Image', use_column_width=True)

    if st.button('Show Histogram'):
        plt = plot_histogram(image)
        st.pyplot(plt)

    brightness = st.slider("Brightness", min_value=-100, max_value=100, value=0)
    contrast = st.slider("Contrast", min_value=-100, max_value=100, value=0)
    if st.button('Adjust Brightness and Contrast'):
        bc_image = adjust_brightness_contrast(image, brightness, contrast)
        st.image(bc_image, caption='Brightness and Contrast Adjusted Image', use_column_width=True)

    if st.button('Find Contours'):
        contours_image = find_contours(image)
        st.image(contours_image, caption='Image with Contours', use_column_width=True)
```

### Untuk menjalankan aplikasi, bisa menggunakan terminal CMD dengan perintah :

```
streamlit run app.py
```

![image](https://github.com/Agussetiaa/Uas3_Pengolahancitra/assets/115542822/f5c9ba4e-678e-4a32-afe8-ecb5d5b5d87f)

### Dan Hasil run Silahkan pindah ke chrome untuk tampilan nya seperti gamabr di abawah ini :

![image](https://github.com/Agussetiaa/Uas3_Pengolahancitra/assets/115542822/bbe1ae56-1cdf-49f4-a76b-8e26c35bd01a)

### Silakahkan klik browse file dan pilih gambar yang akan di manipulasi 

#### *Gambar Original*

![image](https://github.com/Agussetiaa/Uas3_Pengolahancitra/assets/115542822/8b03954c-caec-4402-9d7f-e3db71a009ef)

#### *RGB menjadi HSV*

![image](https://github.com/Agussetiaa/Uas3_Pengolahancitra/assets/115542822/6f8ecbe5-2926-4d6a-a5d9-2a6c42842197)

#### *hasil gambar menghitung Histogram*

![image](https://github.com/Agussetiaa/Uas3_Pengolahancitra/assets/115542822/dbec6fe1-a058-4605-b20f-3a27befb875c)

#### *hasil gambar mengatur Brignest dan Contras*

![image](https://github.com/Agussetiaa/Uas3_Pengolahancitra/assets/115542822/942ba0d9-3a48-4c7a-be91-8e94f9b53606)

#### *hasil gambar Contour*

![image](https://github.com/Agussetiaa/Uas3_Pengolahancitra/assets/115542822/1b1794f2-723f-4bc0-870c-0825c1b11ff0)


### *--------------------------------------- Terimakasih -----------------------------------------------*


### Link Webapp
http://192.168.160.72:8501
