# 🤖 AI-Powered Operations Manager: Automated Meeting Analysis & Reporting System

**Author:** Tafarel Hutama Putra  
**Tech Stack:** n8n, Google Gemini 3.0, Google Sheets API, Telegram API, Gmail API, HTML/CSS.
**LINK n8n PROJECT:** https://shanatio.app.n8n.cloud/workflow/5laZbc7vBDBx3rBo
---

## 📖 Latar Belakang (Background)
Dalam ekosistem operasional logistik dan teknologi yang bergerak cepat, rapat evaluasi rutin sering kali menghasilkan banyak wacana dan *action items* yang krusial. Namun, proses pasca-rapat—seperti transkripsi notulensi, validasi klaim manajer terhadap data aktual, dan pendistribusian tugas ke masing-masing divisi—masih dilakukan secara manual. 

Tantangan utama yang sering terjadi meliputi:
1. **Bias & Subjektivitas:** Laporan lisan dari PIC divisi sering kali tidak sejalan dengan realita metrik KPI aktual (misalnya, mengklaim sistem "aman" padahal data menunjukkan anomali).
2. **Kehilangan Konteks Tugas:** *Action items* sering kali tenggelam atau lupa di- *follow up* karena hanya menjadi catatan di buku atau obrolan lisan.
3. **Lambatnya Distribusi Informasi:** Manajer tingkat atas atau *C-Level* membutuhkan waktu berjam-jam untuk merangkum hasil rapat menjadi email arahan kerja.

Proyek ini dibangun untuk menyelesaikan masalah tersebut dengan menciptakan "Asisten AI Eksekutif" yang mampu mendengarkan rapat, menganalisis data, dan mengawal eksekusi operasional secara *real-time*.

## 🎯 Kenapa Proyek Ini Sangat Layak Diautomasi?
Automasi alur ini memberikan *Return on Investment* (ROI) waktu dan efisiensi yang masif melalui:
*   **Data Grounding (Objektivitas Mutlak):** AI tidak hanya merangkum ucapan, tetapi memvalidasinya dengan data historis dari Google Sheets. Klaim palsu atau inkonsistensi ucapan manusia akan secara otomatis ditegur oleh AI melalui *Discrepancy Alert*.
*   **Zero-Touch Execution:** Hanya dengan mengirimkan *Voice Note* (rekaman suara) ke Telegram, seluruh proses analisis hingga distribusi email instruksi kerja ke Kepala Divisi terjadi dalam hitungan detik tanpa campur tangan manusia.
*   **Segmentasi Otomatis (Auto-Routing):** Informasi tidak lagi dicampur aduk. AI secara kognitif memisahkan instruksi untuk divisi Logistik, Data Analytics, dan IT ke dalam *stream* yang berbeda, memastikan setiap divisi hanya menerima email yang relevan dengan tanggung jawab mereka.

## 🏗️ Arsitektur Workflow (n8n)
Workflow automasi ini dibangun di atas platform n8n dengan topologi *Multimodal Ingestion* dan *Dynamic Routing*:

1.  **Telegram Trigger:** Mendengarkan *input audio* (Voice Note) dari rapat evaluasi secara *real-time*.
2.  **Google Sheets Node:** Menarik data metrik KPI aktual (4 minggu terakhir) dari *database* operasional perusahaan.
3.  **Aggregate Node:** Menyatukan ratusan baris data relasional menjadi satu *dataset* JSON utuh sebagai *context grounding*.
4.  **Telegram Get File:** Mengunduh *binary data* dari rekaman suara rapat.
5.  **Analyze Document (Gemini AI):** Node sentral yang memproses Audio (Multimodal) dan Teks KPI (Data Grounding) secara serentak menggunakan model **Gemini 1.5 Pro**. Output berupa JSON terstruktur.
6.  **Edit Fields & Split Out:** Memecah satu objek respons AI menjadi *array* tugas independen untuk setiap divisi yang terdeteksi.
7.  **Switch Node:** Memisahkan jalur eksekusi berdasarkan nama divisi (Logistics, Data Analytics, IT & Infrastructure).
8.  **Gmail Nodes:** Men- *generate* dan mengirimkan laporan berformat HTML eksekutif langsung ke email *Person in Charge* (PIC).

## ✨ Fitur Utama (Core Features)
*   **🎙️ Multimodal Audio Analysis:** Kemampuan AI menelan file audio secara langsung tanpa perlu melalui *speech-to-text* (Whisper) terpisah, menjaga intonasi dan konteks pembicaraan.
*   **📊 Qualitative Forecasting:** AI mampu melakukan ekstrapolasi skenario risiko 2-4 minggu ke depan berdasarkan tren data kuantitatif yang dipadukan dengan sentimen rapat.
*   **🚨 Anti-Hallucination & Discrepancy Engine:** Prompt rekayasa tingkat lanjut yang memaksa AI menjadi auditor data—menyoroti perbedaan antara ucapan manusia dan fakta angka.
*   **✉️ Dynamic HTML Reports:** Output langsung di- *render* menjadi email HTML korporat bergaya eksekutif dengan tabel *Action Items* yang *auto-looping*.

## 🚀 Potensi Pengembangan Selanjutnya (Future Roadmap)
Sistem ini dirancang sangat modular dan siap untuk diintegrasikan lebih jauh dengan:
*   **Task Management Integration:** Menambahkan node Trello/Asana di ujung *Switch* untuk otomatis membuat tiket kerja dari *Action Items*.
*   **Omnichannel Triggering:** Menambahkan Webhook dari Zoom/Google Meet Cloud Recording agar AI langsung bekerja ketika sesi *video conference* diakhiri.
*   **Corporate Memory:** Menulis kembali janji *Action Items* ke dalam Google Sheets induk agar AI dapat menagih tugas tersebut di sesi rapat evaluasi minggu berikutnya.
