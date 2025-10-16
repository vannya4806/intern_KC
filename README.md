# Class Weighted BioBERT pada NER Biomedis untuk Mengatasi Ketidakseimbangan Data

Repositori ini berisi kode dan sumber daya untuk proyek penelitian tentang *Biomedical Named Entity Recognition* (BioNER). Proyek ini mengeksplorasi dan membandingkan arsitektur *deep learning* yang berbeda—sebuah model klasik CNN-BiLSTM, model BioBERT yang telah di-*fine-tune*, dan model usulan Class-Weighted BioBERT—untuk mengidentifikasi dan mengklasifikasikan entitas biomedis dari teks ilmiah.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-1.10%2B-%23EE4C2C.svg)
![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20Face-Transformers-yellow)

## 📖 Abstrak

Penelitian ini mengembangkan dan mengevaluasi model *deep learning* untuk mengenali entitas biomedis seperti **DNA, RNA, Protein, Cell-Line, dan Cell-Type** secara otomatis dari literatur ilmiah. Kami melakukan analisis komparatif antara arsitektur klasik **CNN-BiLSTM** dan model Transformer canggih, **BioBERT**. Lebih lanjut, kami mengidentifikasi masalah ketidakseimbangan kelas yang signifikan dalam data latih dan mengusulkan model **Class-Weighted BioBERT** untuk mengatasinya. Temuan kami menunjukkan bahwa meskipun model BioBERT-large yang dioptimalkan memberikan kinerja keseluruhan terbaik, strategi pembobotan kelas secara efektif meningkatkan *recall* untuk kelas minoritas, yang menyoroti adanya *trade-off* krusial antara *precision* dan *recall*.

---

## 🚀 Temuan Utama

* **Keunggulan BioBERT**: Model `BioBERT-base` dan `BioBERT-large` secara signifikan mengungguli arsitektur klasik **CNN-BiLSTM**, yang menunjukkan kekuatan dari *transfer learning* melalui pra-pelatihan pada domain spesifik.
* **Model Standar Terbaik**: Model **BioBERT-large** yang telah dioptimalkan (dengan ID `L-2` dalam eksperimen kami) mencapai kinerja paling tinggi dan seimbang, dengan **Macro F1-Score sebesar 0.88**.
* **Paradoks Class Weighting**: Model usulan kami, **Class-Weighted BioBERT** (`W`), berhasil meningkatkan **Recall** untuk kelas minoritas (misalnya, *Recall* untuk `RNA` melonjak dari 0.76 menjadi **0.89**). Namun, keberhasilan ini dibayar dengan penurunan **Precision** yang signifikan, yang menyebabkan Macro F1-Score keseluruhan menjadi lebih rendah (0.78).
* **Pentingnya Konfigurasi**: Beberapa konfigurasi hyperparameter dapat menyebabkan kegagalan pelatihan total (seperti pada model `B-3`), yang menggarisbawahi pentingnya proses tuning yang cermat.

---

## 🛠️ Model & Arsitektur

Proyek ini membandingkan tiga pendekatan utama:

1.  **CNN-BiLSTM**: Sebuah model *deep learning* hibrida klasik yang dilatih dari awal (*from scratch*), berfungsi sebagai *baseline*.
2.  **BioBERT (Standar)**: Sebuah model Transformer (`arsitektur BERT-base`) yang telah melalui pra-pelatihan pada korpus teks biomedis (abstrak PubMed dan artikel PMC). Kami melakukan *fine-tuning* pada beberapa konfigurasi untuk menemukan *baseline* terbaik.
3.  **Class-Weighted BioBERT (Usulan)**: Sebuah ekstensi dari model BioBERT terbaik. Versi ini memodifikasi fungsi *loss* Cross-Entropy dengan menerapkan bobot yang berbanding terbalik dengan frekuensi kelas, memaksa model untuk lebih memperhatikan entitas yang jarang muncul.

---

## 📦 Dataset

Model dilatih dan dievaluasi menggunakan dataset **Revised JNLPBA**, yang merupakan revisi dari dataset *shared task* JNLPBA 2004. Dataset ini adalah tolok ukur untuk NER di domain biomedis, yang bersumber dari GENIA Corpus.

* **Sumber**: [Taiwan's Academia Sinica, Institute of Information Science](https://iasl-btm.iis.sinica.edu.tw/BNER/)


