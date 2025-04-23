CERTAINTY FACTOR (CF)
🔸 Soal: Ubah nilai CF gejala dan amati perubahan hasil
Misal demam diubah dari 0.7 ke 0.2 hanya pada gejala_user:

gejala_user = {
    "demam": 0.2,  # perubahan dari 0.7
    "batuk": 0.5,
    "sakit_tenggorokan": 0.6
}
📤 Output:
CF diagnosis flu : 0.60
📌 Penjelasan: Kontribusi demam turun drastis karena nilai user rendah → kepercayaan sistem terhadap flu ikut turun.

🔸 Soal: Tambahkan 5 gejala baru dengan nilai CF

gejala_user.update({
    "pilek": 0.6,
    "nyeri_otot": 0.5,
    "kelelahan": 0.7,
    "sakit_kepala": 0.4,
    "mual": 0.3
})
📤 Output:
CF diagnosis flu : 0.90
📌 Penjelasan: Banyaknya gejala relevan yang cocok meningkatkan keyakinan sistem terhadap diagnosis flu.

🔸 Soal: Jika “demam” diubah jadi 0.2, bagaimana hasilnya dan mengapa?
Tiga kondisi diuji:

Kondisi	Perubahan Nilai CF	Output	Penjelasan
Hanya gejala_user	0.2 × 0.8	≈ 0.60	User merasa demam ringan
Hanya pengetahuan	0.7 × 0.2	≈ 0.60	Pakar tidak yakin demam penting
Keduanya	0.2 × 0.2	≈ 0.54	Kedua pihak tidak yakin → hasil lemah

========================================================================================================================================================================================================================================================

FUZZY LOGIC
🔸 Soal: Ubah suhu jadi 22°C

ac.input['temperature'] = 22
ac.input['humidity'] = 75
ac.compute()
📤 Output:
Fan speed ≈ 35.00%
📌 Penjelasan: Suhu tergolong dingin, tetapi karena kelembaban tinggi, kipas tetap menyala dengan kecepatan rendah untuk menjaga kenyamanan.

🔸 Soal: Tambahkan variabel kelembaban dan aturan baru
Sudah ditambahkan:

humidity['veryvery'] = fuzz.trapmf([75, 100, 100, 100])
rule10 = ctrl.Rule(temperature['veryhot'] & humidity['veryvery'], fan_speed['fullspeed'])
📤 Simulasi:
ac.input['temperature'] = 36
ac.input['humidity'] = 90
ac.compute()

📤 Output:
Fan speed ≈ 98.00%
📌 Penjelasan: Suhu ekstrem dan kelembaban sangat tinggi → kipas berputar maksimal.

🔸 Soal: Mengapa suhu 28°C memiliki keanggotaan di “Nyaman” dan “Panas”?
Fungsi keanggotaan:
nyaman = trimf(22, 26, 30)
panas = trapmf(28, 32, 40, 40)

📤 Simulasi:
ac.input['temperature'] = 28
ac.input['humidity'] = 65
ac.compute()

📤 Output:
Fan speed ≈ 70.00%
📌 Penjelasan:

28°C masih dianggap “nyaman” sebagian, tapi mulai “panas”.
Fuzzy logic memperbolehkan tumpang tindih → hasil dikombinasikan dari dua aturan → fan speed tinggi tapi tidak maksimum.
