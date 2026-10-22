# project-bot-btc-glow

Prediksi harga **Bitcoin (BTC/IDR)** dengan model deep learning. Proyek ini menarik data candle dari bursa **Indodax**, melatih model **LSTM** (PyTorch), lalu menampilkan hasilnya di dashboard web.

> Catatan: ini proyek belajar machine learning untuk data deret waktu, **bukan** nasihat finansial. Prediksi harga kripto tidak pernah pasti, jangan dipakai untuk mengambil keputusan beli/jual uang sungguhan.

## Alur

```
get_data.py   → tarik OHLCV BTC/IDR dari Indodax (endpoint TradingView)
preprocess.py → bersihkan, bikin fitur, scaling (disimpan ke data/*.pkl, *.npy)
train.py      → latih model LSTM, simpan ke models/best_lstm.pth
dashboard/    → aplikasi Flask untuk menampilkan prediksi vs harga asli
```

## Stack

- Python · PyTorch (LSTM) · scikit-learn · pandas · numpy
- Flask untuk dashboard, matplotlib untuk grafik
- Sumber data: API publik Indodax (`history_v2`)

## Menjalankan

Butuh Python 3.9+.

```bash
pip install -r requirements.txt

python script/get_data.py       # ambil data terbaru
python script/preprocess.py     # siapkan dataset
python script/train.py          # latih model (hasil: models/best_lstm.pth)

python dashboard/app.py         # buka dashboard di http://localhost:5000
```

## Struktur

```
script/     get_data, preprocess, model, train
models/     best_lstm.pth  (bobot model terlatih)
data/       dataset hasil preprocessing + scaler
dashboard/  app.py  (Flask)
```

## Batasan

Model dilatih dari pola harga historis saja. Pasar kripto dipengaruhi banyak hal di luar data harga, jadi anggap ini eksperimen teknis, bukan alat trading.
