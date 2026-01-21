
# 🖼️ Шпаргалка по OpenCV: Основные операции обработки изображений

## 1️⃣ Чтение, запись и отображение изображения

```python
import cv2

# Чтение изображения
image = cv2.imread('image.jpg')  # В цвете
gray_image = cv2.imread('image.jpg', cv2.IMREAD_GRAYSCALE)  # В градациях серого

# Запись изображения
cv2.imwrite('output.jpg', image)

# Отображение изображения
cv2.imshow('Image', image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

## 2️⃣ Пороговая фильтрация

```python
# Бинарная пороговая фильтрация
_, binary = cv2.threshold(gray_image, 127, 255, cv2.THRESH_BINARY)

# Обратная бинарная фильтрация
_, binary_inv = cv2.threshold(gray_image, 127, 255, cv2.THRESH_BINARY_INV)

# Транктация
_, trunc = cv2.threshold(gray_image, 127, 255, cv2.THRESH_TRUNC)

# Порог до нуля
_, tozero = cv2.threshold(gray_image, 127, 255, cv2.THRESH_TOZERO)

# Адаптивная пороговая фильтрация
adaptive = cv2.adaptiveThreshold(
    gray_image, 255, cv2.ADAPTIVE_THRESH_GAUSSIAN_C, cv2.THRESH_BINARY, 11, 2)
```

## 3️⃣ Размытие

```python
# Среднее размытие
blurred = cv2.blur(image, (5, 5))

# Гауссово размытие
gaussian_blurred = cv2.GaussianBlur(image, (5, 5), 0)

# Медианное размытие
median_blurred = cv2.medianBlur(image, 5)

# Билатеральное размытие
bilateral_filtered = cv2.bilateralFilter(image, 9, 75, 75)
```

## 4️⃣ Нахождение границ (Canny)

```python
# Обнаружение границ методом Canny
edges = cv2.Canny(image, threshold1=100, threshold2=200)
```

## 5️⃣ Нахождение контуров

```python
# Пороговая фильтрация для получения бинарного изображения
_, binary = cv2.threshold(gray_image, 127, 255, cv2.THRESH_BINARY)

# Нахождение контуров
contours, hierarchy = cv2.findContours(binary, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)

# Рисование контуров на изображении
cv2.drawContours(image, contours, -1, (0, 255, 0), 2)
```

## 6️⃣ Пример полной программы

```python
import cv2

# Шаг 1: Чтение изображения
image = cv2.imread('image.jpg')
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Шаг 2: Применение пороговой фильтрации
_, binary = cv2.threshold(gray_image, 127, 255, cv2.THRESH_BINARY)

# Шаг 3: Нахождение границ
edges = cv2.Canny(gray_image, 100, 200)

# Шаг 4: Нахождение контуров
contours, _ = cv2.findContours(binary, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)

# Шаг 5: Рисование контуров
output = image.copy()
cv2.drawContours(output, contours, -1, (0, 255, 0), 2)

# Шаг 6: Отображение результатов
cv2.imshow('Original', image)
cv2.imshow('Edges', edges)
cv2.imshow('Contours', output)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

## 📌 Примечания

- Используйте подходящие параметры (пороги, размеры ядра, размеры соседства) для достижения оптимального результата.
- Экспериментируйте с разными методами, чтобы понять их влияние на изображение.
