# mengubah-gambar

from google.colab import files
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Upload image file
uploaded = files.upload()

# Membaca gambar yang diunggah
image_path = list(uploaded.keys())[0]
image = cv2.imread(image_path)
image_gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Fungsi untuk menampilkan gambar asli dan hasil proses

def show_images(title1, image1, title2, image2):
    plt.figure(figsize=(12,6))

    plt.subplot(1, 2, 1)
    plt.imshow(image1, cmap='gray')
    plt.title(title1)
    plt.axis('off')

    plt.subplot(1, 2, 2)
    plt.imshow(image2, cmap='gray')
    plt.title(title2)
    plt.axis('off')

    plt.show()

# Menampilkan Gambar Asli
show_images('Gambar Asli (Grayscale)', image_gray, 'Gambar Asli (RGB)', cv2.cvtColor(image, cv2.COLOR_BGR2RGB))

# 1. Citra Negative
negative_image = 255 - image_gray
show_images('Gambar Asli', image_gray, 'Citra Negative', negative_image)

# 2. Transformasi Log
c = 255 / np.log(1 + np.max(image_gray))
log_image = c * np.log(1 + image_gray.astype(np.float32))
log_image = np.uint8(log_image)
show_images('Gambar Asli', image_gray, 'Transformasi Log', log_image)

# 3. Transformasi Power Law (Gamma Correction)
gamma = 0.5  # Ubah nilai gamma untuk hasil berbeda
power_law_image = np.array(255 * (image_gray / 255) ** gamma, dtype='uint8')
show_images('Gambar Asli', image_gray, 'Transformasi Power Law', power_law_image)

# 4. Histogram Equalization
equalized_image = cv2.equalizeHist(image_gray)
show_images('Gambar Asli', image_gray, 'Histogram Equalization', equalized_image)

# 5. Histogram Normalization
normalized_image = cv2.normalize(image_gray, None, 0, 255, cv2.NORM_MINMAX)
show_images('Gambar Asli', image_gray, 'Histogram Normalization', normalized_image)

# 6. Konversi RGB ke HSI
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
image_hsi = cv2.cvtColor(image_rgb, cv2.COLOR_RGB2HSV)
show_images('Gambar Asli (RGB)', image_rgb, 'Konversi RGB ke HSI (Hue Component)', image_hsi[:,:,0])

# Menentukan thresholding (contoh sederhana)
threshold_value = 120
_, threshold_image = cv2.threshold(image_hsi[:,:,2], threshold_value, 255, cv2.THRESH_BINARY)
show_images('G![download](https://github.com/user-attachments/assets/afe30dfe-5b55-486a-99c7-a95736603f60)
gambar Asli (Intensity Component)', image_hsi[:,:,2], 'Thresholding pada Komponen Intensity', threshold_image)
     ![download](https://github.com/user-attachments/assets/37ac4594-08c7-4e00-aed2-78c64a9517ad)
1.citra negative
input:Gambar asli dalam format RGB atau grayscale.
output:Gambar dengan intensitas warna yang dibalik (negatif).
![download](https://github.com/user-attachments/assets/fe140e42-809a-440c-a06e-9cdd54daf420)
2.transformasi log
input:Gambar asli dalam format RGB atau grayscale.
output:Gambar dengan peningkatan kontras pada area gelap.
![download](https://github.com/user-attachments/assets/0ecadc68-2892-4a23-9e02-72f97bb9e13b)
3.Transformasi Power Law (Gamma):
input:Gambar asli dalam format RGB atau grayscale.
output:Gambar dengan penyesuaian kontras berdasarkan nilai gamma.

![download](https://github.com/user-attachments/assets/9e2e3eeb-0863-4038-bd4f-62651fb267b7)
4.Histogram Equalization:
input:Gambar asli dalam format RGB atau grayscale.
output:Gambar dengan distribusi intensitas yang lebih merata.

![download](https://github.com/user-attachments/assets/50f227d9-daa8-4e4f-8eb5-ad366994611d)
5.Histogram Normalization:
input:Gambar asli dalam format RGB atau grayscale.
output:Gambar dengan intensitas yang dinormalisasi ke rentang 0-255.

![download](https://github.com/user-attachments/assets/f4bfef1a-3796-42b5-9403-dd10e47120e2)
6.Konversi RGB ke HSI:
input:Gambar asli dalam format RGB.
output:Gambar dalam format HSI (Hue, Saturation, Intensity).

