
## Dataset
- Jumlah total gambar: ±10.000
- Jumlah kelas: 7
- Setiap kelas berisi 1.498 gambar (seimbang)
- Dataset bersih dan bervariasi (tidak ada noise)
- Pembagian data:
  - **Training:** 70%
  - **Validation:** 20%
  - **Testing:** 10%
- Augmentasi dilakukan secara real-time menggunakan `ImageDataGenerator`:
  - Rescale (1./255)
  - Rotation (±30°)
  - Width & Height Shift (0.2)
  - Zoom (0.3)
  - Horizontal Flip
  - Brightness Range [0.7, 1.3]

## Model Architecture
Model menggunakan **Transfer Learning dengan MobileNetV2** dan **tambahan CNN layer** 
Arsitektur Utama:
1. **Base Model:** MobileNetV2 
2. **Conv2D + BatchNormalization + MaxPooling2D** 
3. **GlobalAveragePooling2D**
4. **Dense(256, ReLU)** + **Dropout(0.4)**
5. **Output Layer:** Dense(num_classes, Softmax)

## Training Result
- **Akurasi Training:** ~94.3%  
- **Akurasi Validation:** ~94.85%  
- **Akurasi Testing:** ~94.51%  
- **Loss Validation:** 0.1562  
- **Loss Testing:** 0.1721  
- Tidak terdapat overfitting signifikan
- Callback:
  - EarlyStopping
  - ReduceLROnPlateau
  - ModelCheckpoint

Tampilan grafik akurasi dan loss menunjukkan model belajar dengan stabil dan konvergen.

## Model Export
Model disimpan dalam tiga format:
| Format | Lokasi |
|---------|---------|
| SavedModel | `/saved_model/` |
| TensorFlow Lite | `/tflite/model.tflite` |
| TensorFlow.js | `/tfjs_model/model.json` |

## Inference (Uji Coba)
Model diuji dengan gambar baru menggunakan format **TFLite** untuk memastikan hasil inferensi sesuai dengan label sebenarnya.

