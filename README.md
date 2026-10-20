# Latihan-Sub-Bab-Endokrin-dan-Hormon
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ujian IPA: Sistem Endokrin dan Hormon</title>
    <style>
        :root {
            --primary: #0275d8;
            --success: #5cb85c;
            --danger: #d9534f;
            --light: #f4f7f6;
            --dark: #333;
        }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background: #e9ecef; margin: 0; padding: 0; }
        .container { max-width: 900px; margin: 20px auto; background: white; padding: 20px 30px; border-radius: 10px; box-shadow: 0 4px 8px rgba(0,0,0,0.1); }
        .hidden { display: none !important; }
        
        /* Header & Info */
        .header { display: flex; justify-content: space-between; align-items: center; border-bottom: 2px solid #eee; padding-bottom: 15px; margin-bottom: 20px; flex-wrap: wrap; gap: 10px; }
        .timer { font-size: 1.5em; font-weight: bold; color: var(--danger); }
        
        /* Layout Ujian (Responsive) */
        .exam-layout { display: flex; gap: 20px; }
        .main-content { flex: 3; }
        .sidebar { flex: 1; background: var(--light); padding: 15px; border-radius: 8px; max-height: 500px; overflow-y: auto; }
        
        /* Panel Nomor */
        .panel-grid { display: grid; grid-template-columns: repeat(5, 1fr); gap: 10px; margin-top: 15px; }
        .btn-nav { padding: 10px 0; text-align: center; border-radius: 5px; cursor: pointer; border: 1px solid #ccc; font-weight: bold; background: white; transition: 0.2s; }
        .btn-nav.answered { background: var(--success); color: white; border-color: var(--success); }
        .btn-nav.current { border: 3px solid var(--primary); transform: scale(1.1); }
        
        /* Soal & Opsi */
        .question-text { font-size: 1.2em; margin-bottom: 10px; line-height: 1.5; color: var(--dark); }
        .badge-diff { display: inline-block; padding: 4px 8px; font-size: 0.8em; border-radius: 4px; color: white; margin-bottom: 15px; }
        .badge-lots { background: #17a2b8; }
        .badge-mots { background: #f0ad4e; }
        
        .option-label { display: block; background: var(--light); padding: 12px; margin-bottom: 10px; border-radius: 5px; cursor: pointer; border: 1px solid #ddd; transition: 0.2s; }
        .option-label:hover { background: #e2e6ea; }
        .option-label input { margin-right: 10px; }
        .option-label.selected { background: #d0e8fc; border-color: var(--primary); }

        /* Tombol Aksi */
        .action-buttons { display: flex; justify-content: space-between; margin-top: 20px; gap: 10px; flex-wrap: wrap; }
        button { padding: 12px 20px; border: none; border-radius: 5px; cursor: pointer; font-size: 1em; font-weight: bold; transition: 0.2s; flex: 1; }
        .btn-primary { background: var(--primary); color: white; }
        .btn-warning { background: #f0ad4e; color: white; }
        .btn-danger { background: var(--danger); color: white; width: 100%; margin-top: 20px;}
        
        /* Pembahasan */
        .result-item { border: 1px solid #ccc; border-radius: 8px; padding: 15px; margin-bottom: 15px; }
        .correct-ans { background: #d4edda; border-color: #c3e6cb; }
        .wrong-ans { background: #f8d7da; border-color: #f5c6cb; }
        .discussion { margin-top: 10px; font-size: 0.95em; background: #fff3cd; padding: 10px; border-left: 4px solid #ffc107; }
        
        input[type="text"], input[type="email"] { width: 100%; padding: 12px; margin: 10px 0 20px 0; border: 1px solid #ccc; border-radius: 5px; box-sizing: border-box;}

        /* MEDIA QUERY UNTUK HP (PHONE MODE) */
        @media (max-width: 768px) {
            .container { margin: 0; padding: 15px; border-radius: 0; min-height: 100vh; }
            .exam-layout { flex-direction: column; }
            .sidebar { max-height: none; overflow-y: visible; margin-top: 20px; }
            .action-buttons button { font-size: 0.9em; padding: 10px; }
            .panel-grid { grid-template-columns: repeat(6, 1fr); }
            .header { flex-direction: column; align-items: flex-start; }
            .timer { align-self: flex-end; }
        }
    </style>
</head>
<body>

    <!-- HALAMAN LOGIN -->
    <div id="loginPage" class="container">
        <h2 style="text-align: center; color: var(--primary);">Ujian Akhir: Sistem Endokrin dan Hormon</h2>
        <p style="text-align: center;">Mata Pelajaran: IPA Kelas 9 | Durasi: 45 Menit</p>
        <hr>
        <label>Nama Lengkap (Sesuai Absen):</label>
        <input type="text" id="nama" placeholder="Masukkan nama lengkap" required>
        <label>Email Siswa:</label>
        <input type="email" id="email" placeholder="Masukkan alamat email" required>
        
        <div style="background: #fff3cd; padding: 15px; border-left: 4px solid #ffc107; margin-bottom: 20px; font-size: 0.9em;">
            <strong>⚠️ PERHATIAN PENTING:</strong><br>
            1. <b>Soal & Opsi Jawaban diacak</b> untuk setiap siswa.<br>
            2. Layar akan masuk mode penuh (Fullscreen).<br>
            3. Dilarang keras menekan tombol Home, berpindah aplikasi, membagi layar, atau membuka tab lain.<br>
            4. Pelanggaran lebih dari 2 kali akan mengakibatkan <b>DISKUALIFIKASI</b>.
        </div>
        
        <button class="btn-primary" style="width: 100%; padding: 15px; font-size: 1.1em;" onclick="mulaiUjian()">Saya Mengerti, Mulai Ujian</button>
    </div>

    <!-- HALAMAN UJIAN -->
    <div id="examPage" class="container hidden">
        <div class="header">
            <div>
                <h3 style="margin:0;">IPA: Sistem Endokrin</h3>
                <small id="identitasSiswa"></small>
            </div>
            <div class="timer" id="timerDisplay">45:00</div>
        </div>

        <div class="exam-layout">
            <div class="main-content">
                <div id="badgeDiff" class="badge-diff"></div>
                <div id="questionText" class="question-text"></div>
                <div id="optionsContainer"></div>
                
                <div class="action-buttons">
                    <button id="btnPrev" class="btn-primary" onclick="changeQuestion(-1)">&#8592; Sebelumnya</button>
                    <button id="btnSkip" class="btn-warning" onclick="skipQuestion()">Lewati &#8635;</button>
                    <button id="btnNext" class="btn-primary" onclick="changeQuestion(1)">Selanjutnya &#8594;</button>
                </div>
            </div>
            
            <div class="sidebar">
                <h4 style="margin-top:0; text-align: center;">Navigasi Soal</h4>
                <div class="panel-grid" id="panelGrid"></div>
                <button class="btn-danger" style="padding: 15px; font-size: 1.1em;" onclick="konfirmasiSelesai()">SELESAI & KUMPULKAN</button>
            </div>
        </div>
    </div>

    <!-- HALAMAN HASIL & PEMBAHASAN -->
    <div id="resultPage" class="container hidden">
        <h2 style="text-align: center;">Hasil Ujian</h2>
        <div style="text-align: center; font-size: 1.2em; margin-bottom: 20px;">
            Nama: <span id="resNama"></span><br>
            Nilai Akhir: <strong id="resSkor" style="font-size: 2em; color: var(--primary);"></strong>
        </div>
        <hr>
        <h3>Pembahasan:</h3>
        <div id="discussionContainer"></div>
    </div>

    <script>
        // --- DATABASE SOAL: Sistem Endokrin & Hormon Emosi ---
        const bankSoal = [
            { id: 1, q: "Kelenjar yang memproduksi hormon dan menyalurkan sekresinya langsung ke dalam pembuluh darah tanpa melalui saluran khusus disebut...", opt: ["A. Kelenjar eksokrin", "B. Kelenjar endokrin", "C. Kelenjar getah bening", "D. Kelenjar saliva"], ans: 1, type: "LOTS", bahas: "Kelenjar endokrin (kelenjar buntu) menyekresikan hormon langsung ke dalam aliran darah, berbeda dengan eksokrin yang memiliki saluran khusus." },
            { id: 2, q: "Kelenjar hipofisis (pituitari) sering dijuluki sebagai 'Master of Gland' (pemimpin kelenjar). Alasan utamanya adalah karena kelenjar ini...", opt: ["A. Memiliki ukuran paling besar di antara kelenjar lainnya", "B. Menghasilkan hormon yang mengatur dan merangsang kerja kelenjar endokrin lain", "C. Memproduksi semua jenis hormon yang dibutuhkan tubuh", "D. Mengatur emosi secara langsung melalui otak besar"], ans: 1, type: "MOTS", bahas: "Hipofisis menghasilkan hormon seperti TSH, ACTH, dan FSH/LH yang berfungsi mengendalikan sekresi kelenjar endokrin lainnya." },
            { id: 3, q: "Hormon yang berperan penting dalam memunculkan perasaan bahagia, menstabilkan suasana hati (mood), serta mengatur siklus tidur dan pencernaan adalah...", opt: ["A. Adrenalin", "B. Kortisol", "C. Serotonin", "D. Melatonin"], ans: 2, type: "LOTS", bahas: "Serotonin dikenal sebagai penstabil suasana hati alami. Kadarnya yang cukup mencegah depresi dan memberikan rasa tenang." },
            { id: 4, q: "Saat seseorang dihadapkan pada ancaman atau merasa stres kronis, tubuh memproduksi 'hormon stres' untuk menjaga kewaspadaan jangka panjang. Hormon ini dihasilkan oleh kelenjar adrenal bagian korteks, yaitu...", opt: ["A. Kortisol", "B. Oksitosin", "C. Epinefrin", "D. Testosteron"], ans: 0, type: "MOTS", bahas: "Kortisol adalah hormon stres utama yang meningkatkan gula darah dan menekan sistem imun saat tubuh mengalami stres yang berkepanjangan." },
            { id: 5, q: "Kamu tiba-tiba berpapasan dengan seekor anjing buas. Jantungmu berdebar sangat kencang, napas memburu, dan kamu mendapat energi ekstra untuk berlari cepat. Hormon yang memicu reaksi 'fight or flight' ini adalah...", opt: ["A. Endorfin", "B. Adrenalin (Epinefrin)", "C. Prolaktin", "D. Glukagon"], ans: 1, type: "MOTS", bahas: "Adrenalin memicu peningkatan detak jantung, pernapasan, dan pelepasan glukosa untuk memberi energi instan saat darurat." },
            { id: 6, q: "Oksitosin sering dijuluki sebagai 'hormon cinta'. Secara psikologis dan emosional, hormon ini berperan dalam...", opt: ["A. Memicu agresi dan kemarahan", "B. Meningkatkan tekanan darah dan memicu stres", "C. Memperkuat ikatan emosional (bonding), kasih sayang, empati, dan rasa percaya antar individu", "D. Membuat tubuh merasa lelah dan mengantuk"], ans: 2, type: "MOTS", bahas: "Oksitosin dilepaskan saat interaksi fisik atau emosional yang positif, memicu rasa percaya, empati, dan ikatan batin (seperti antara ibu dan bayi atau pasangan)." },
            { id: 7, q: "Setelah berolahraga lari yang cukup jauh, rasa pegal dan lelah seringkali tergantikan oleh perasaan lega dan bahagia. Hal ini disebabkan oleh produksi hormon pereda nyeri alami tubuh, yaitu...", opt: ["A. Tiroksin", "B. Dopamin", "C. Endorfin", "D. Melatonin"], ans: 2, type: "MOTS", bahas: "Endorfin bekerja mirip dengan analgesik (pereda nyeri) dan memberikan efek euforia atau rasa nyaman setelah aktivitas fisik berat." },
            { id: 8, q: "Sistem penghargaan di otak (reward system) sangat dipengaruhi oleh sebuah hormon. Saat kita berhasil mencapai target, hormon ini membanjiri otak sehingga kita merasa termotivasi dan puas. Hormon ini adalah...", opt: ["A. Melatonin", "B. Insulin", "C. Dopamin", "D. Glukagon"], ans: 2, type: "LOTS", bahas: "Dopamin adalah hormon penggerak motivasi dan pusat kesenangan/penghargaan di otak ketika kita mencapai sesuatu." },
            { id: 9, q: "Kelenjar pankreas memiliki fungsi ganda, salah satunya memproduksi hormon endokrin yang berfungsi menurunkan kadar glukosa darah dengan mengubahnya menjadi glikogen. Hormon tersebut adalah...", opt: ["A. Glukagon", "B. Insulin", "C. Tiroksin", "D. Kortisol"], ans: 1, type: "LOTS", bahas: "Insulin diproduksi oleh sel beta pankreas dan esensial untuk menurunkan gula darah yang tinggi." },
            { id: 10, q: "Seseorang yang tidak dapat memproduksi insulin dalam jumlah cukup akan mengalami peningkatan kadar gula dalam darah yang ekstrem, suatu penyakit yang dikenal dengan nama...", opt: ["A. Diabetes insipidus", "B. Diabetes melitus", "C. Hipoglikemia", "D. Gondok"], ans: 1, type: "LOTS", bahas: "Diabetes melitus (kencing manis) terjadi akibat kekurangan insulin atau resistensi terhadap insulin." },
            { id: 11, q: "Di daerah leher terdapat kelenjar tiroid yang menghasilkan hormon tiroksin. Fungsi utama hormon tiroksin adalah...", opt: ["A. Mengatur kecepatan metabolisme sel tubuh", "B. Menghasilkan hormon kebahagiaan", "C. Mengatur penyerapan air pada ginjal", "D. Menghasilkan enzim pencernaan"], ans: 0, type: "LOTS", bahas: "Tiroksin sangat penting untuk mengatur proses metabolisme dasar dan pembakaran energi di dalam sel." },
            { id: 12, q: "Kekurangan unsur yodium dalam makanan secara terus-menerus dapat menyebabkan kelenjar tiroid bekerja terlalu keras hingga membesar. Kondisi ini disebut...", opt: ["A. Diabetes", "B. Gigantisme", "C. Penyakit Gondok", "D. Kretinisme"], ans: 2, type: "MOTS", bahas: "Yodium adalah bahan baku pembuatan hormon tiroksin. Tanpanya, tiroid membengkak sebagai usaha mengompensasi kekurangan hormon (gondok)." },
            { id: 13, q: "Tubuh menjaga kadar kalsium dalam darah dengan bantuan kelenjar paratiroid. Hormon parathormon (PTH) yang dihasilkan akan bekerja dengan cara...", opt: ["A. Membuang kalsium melalui urin", "B. Memindahkan kalsium dari darah ke dalam tulang", "C. Melepaskan kalsium dari tulang ke dalam aliran darah jika kadarnya turun", "D. Mencegah penyerapan kalsium di usus"], ans: 2, type: "MOTS", bahas: "Parathormon meningkatkan kalsium darah dengan merombak matriks tulang (demineralisasi) ketika kalsium darah sedang rendah." },
            { id: 14, q: "Saat hari mulai gelap, kita biasanya mulai merasa mengantuk. Ini karena kelenjar pineal di otak mulai memproduksi hormon pengatur siklus tidur, yaitu...", opt: ["A. Insulin", "B. Testosteron", "C. Melatonin", "D. Adrenalin"], ans: 2, type: "LOTS", bahas: "Melatonin dihasilkan oleh kelenjar pineal saat gelap untuk memberi sinyal pada tubuh agar beristirahat." },
            { id: 15, q: "Kebiasaan bermain ponsel (terpapar cahaya biru/blue light) sesaat sebelum tidur dapat menyebabkan insomnia ringan karena...", opt: ["A. Cahaya layar menstimulasi pankreas menghasilkan insulin", "B. Mata mengirim sinyal terang ke otak sehingga produksi melatonin terhambat", "C. Meningkatnya hormon endorfin secara drastis", "D. Kelenjar tiroid menjadi terlalu aktif"], ans: 1, type: "MOTS", bahas: "Cahaya biru menekan sekresi melatonin karena otak mengira hari masih siang, sehingga menyebabkan kesulitan tidur." },
            { id: 16, q: "Hormon reproduksi pada pria yang memicu perkembangan otot, perubahan suara menjadi lebih berat, dan tumbuhnya rambut di area tertentu pada masa pubertas diproduksi oleh...", opt: ["A. Testis", "B. Kelenjar Prostat", "C. Ovarium", "D. Kelenjar Timus"], ans: 0, type: "LOTS", bahas: "Testis memproduksi hormon testosteron yang memicu ciri-ciri kelamin sekunder pada pria." },
            { id: 17, q: "Pada wanita, ovarium menghasilkan hormon yang bertanggung jawab mematangkan sel telur serta membentuk ciri kelamin sekunder wanita (seperti membesarnya payudara). Hormon ini adalah...", opt: ["A. Progesteron", "B. Prolaktin", "C. Estrogen", "D. Oksitosin"], ans: 2, type: "LOTS", bahas: "Estrogen adalah hormon reproduksi utama wanita yang membentuk karakteristik feminin dan mengatur pematangan sel telur." },
            { id: 18, q: "Jika kadar glukosa dalam darah menurun drastis saat kita berpuasa, sel alfa pankreas akan menyekresikan hormon untuk merombak glikogen di hati menjadi glukosa. Hormon tersebut adalah...", opt: ["A. Insulin", "B. Glukagon", "C. Somatostatin", "D. Aldosteron"], ans: 1, type: "MOTS", bahas: "Glukagon bekerja berkebalikan dengan insulin; ia menaikkan kadar gula darah saat tubuh kekurangan asupan energi." },
            { id: 19, q: "Kelebihan hormon pertumbuhan (Growth Hormone) yang sangat drastis pada masa kanak-kanak dapat menyebabkan tulang panjang tumbuh secara tidak terkendali, suatu kondisi yang dikenal sebagai...", opt: ["A. Kretinisme", "B. Gigantisme", "C. Dwarfisme", "D. Akromegali"], ans: 1, type: "LOTS", bahas: "Hipersekresi hormon somatotropin (GH) di masa pertumbuhan mengakibatkan gigantisme (tubuh raksasa)." },
            { id: 20, q: "Hormon antidiuretik (ADH) berfungsi mengatur penyerapan kembali air pada tubulus ginjal. Jika tubuh kekurangan hormon ADH, penderita akan mengeluarkan urin dalam volume yang sangat besar (sering kencing). Penyakit ini disebut...", opt: ["A. Gagal ginjal akut", "B. Diabetes melitus", "C. Diabetes insipidus", "D. Nefritis"], ans: 2, type: "MOTS", bahas: "Kurangnya ADH menyebabkan air tidak diserap kembali oleh ginjal, sehingga urin sangat encer dan bervolume banyak (Diabetes insipidus)." },
            { id: 21, q: "Kelenjar ini terletak di rongga dada, sangat aktif pada masa bayi untuk sistem imun (pematangan sel T limfosit), namun ukurannya perlahan mengecil saat manusia beranjak dewasa. Kelenjar yang dimaksud adalah...", opt: ["A. Kelenjar Tiroid", "B. Kelenjar Timus", "C. Kelenjar Pineal", "D. Kelenjar Adrenal"], ans: 1, type: "LOTS", bahas: "Kelenjar timus berperan besar dalam sistem imun bawaan dan pematangan sel T, menyusut (atrofi) setelah pubertas." },
            { id: 22, q: "Hormon yang merangsang produksi air susu (ASI) pada kelenjar payudara seorang ibu yang baru melahirkan adalah...", opt: ["A. Estrogen", "B. Oksitosin", "C. Prolaktin", "D. Progesteron"], ans: 2, type: "LOTS", bahas: "Prolaktin (dihasilkan oleh hipofisis anterior) merangsang sintesis ASI, sementara oksitosin merangsang pengeluaran ASI (let-down reflex)." },
            { id: 23, q: "Hormon reproduksi pada wanita yang memiliki fungsi khusus menebalkan dan mempertahankan dinding rahim (endometrium) untuk persiapan kehamilan jika terjadi pembuahan adalah...", opt: ["A. Luteinizing Hormone (LH)", "B. Follicle Stimulating Hormone (FSH)", "C. Estrogen", "D. Progesteron"], ans: 3, type: "MOTS", bahas: "Progesteron disebut juga hormon kehamilan. Hormon ini mencegah luruhnya dinding rahim agar zigot dapat menempel (implantasi)." },
            { id: 24, q: "Grup hormon 'Happy Hormones' (hormon kebahagiaan) yang memengaruhi kesejahteraan mental dan emosi manusia terdiri atas...", opt: ["A. Dopamin, Oksitosin, Serotonin, dan Endorfin (DOSE)", "B. Adrenalin, Kortisol, Tiroksin, dan Insulin", "C. Estrogen, Progesteron, Testosteron, dan Prolaktin", "D. Melatonin, Glukagon, Parathormon, dan Oksitosin"], ans: 0, type: "MOTS", bahas: "Dopamin (penghargaan), Oksitosin (cinta), Serotonin (penstabil mood), dan Endorfin (penghilang nyeri) dikenal sebagai empat hormon kebahagiaan (DOSE)." },
            { id: 25, q: "Seseorang sering merasa cemas tanpa alasan yang jelas, mudah panik, dan ototnya menegang. Secara hormonal, kondisi stres berkepanjangan ini diakibatkan oleh tingginya kadar hormon...", opt: ["A. Melatonin", "B. Oksitosin", "C. Kortisol", "D. Endorfin"], ans: 2, type: "MOTS", bahas: "Tingginya kortisol dalam aliran darah dalam jangka panjang menciptakan perasaan cemas yang persisten dan melemahkan sistem imun." },
            { id: 26, q: "Selain mengatur metabolisme fisik, hormon tiroid (tiroksin) ternyata juga memengaruhi emosi. Seseorang dengan kondisi hipertiroidisme (kelebihan tiroksin) seringkali mengalami...", opt: ["A. Mudah lelah dan apatis", "B. Gelisah, mudah tersinggung (iritabel), dan hiperaktif", "C. Depresi berat yang memicu keinginan tidur terus", "D. Ketenangan pikiran yang ekstrem"], ans: 1, type: "MOTS", bahas: "Hipertiroid mempercepat semua sistem tubuh, menyebabkan kegelisahan emosional, detak jantung cepat, dan penderitanya mudah gugup/marah." },
            { id: 27, q: "Saat seorang ibu memeluk bayinya, tubuh akan merespon dengan melepaskan hormon yang mengurangi stres ibu dan menciptakan ikatan batin. Hormon ini dihasilkan oleh...", opt: ["A. Kelenjar Tiroid", "B. Hipotalamus lalu dikeluarkan oleh Hipofisis Posterior", "C. Kelenjar Pankreas", "D. Korteks Adrenal"], ans: 1, type: "MOTS", bahas: "Oksitosin diproduksi di hipotalamus dan disimpan serta disekresikan melalui kelenjar hipofisis posterior." },
            { id: 28, q: "Saat wanita mendekati masa menstruasi (PMS), mereka sering mengalami perubahan suasana hati (mood swings) yang drastis, mudah menangis, atau marah. Hal ini paling erat dipengaruhi oleh naik turunnya hormon...", opt: ["A. Adrenalin dan Kortisol", "B. Estrogen dan Progesteron", "C. Insulin dan Glukagon", "D. Melatonin dan Endorfin"], ans: 1, type: "MOTS", bahas: "Fluktuasi dramatis antara kadar estrogen dan progesteron menjelang menstruasi memengaruhi neurotransmiter di otak, termasuk serotonin." },
            { id: 29, q: "Di otak, hormon dopamin diproduksi dari asam amino. Seseorang yang mengalami kekurangan dopamin ekstrem seringkali dikaitkan dengan penyakit saraf yang menyebabkan tremor atau kesulitan bergerak, yaitu penyakit...", opt: ["A. Alzheimer", "B. Meningitis", "C. Parkinson", "D. Stroke"], ans: 2, type: "MOTS", bahas: "Parkinson terjadi karena rusaknya neuron penghasil dopamin di area otak (substantia nigra), mengakibatkan gangguan gerak (tremor) dan suasana hati." },
            { id: 30, q: "Secara alami, kita dapat meningkatkan sekresi keempat hormon kebahagiaan (Dopamin, Serotonin, Oksitosin, Endorfin) melalui...", opt: ["A. Mengonsumsi banyak minuman berenergi dan kafein setiap jam", "B. Berdiam diri di ruang gelap sepanjang hari", "C. Olahraga teratur, bersosialisasi yang baik, berjemur sinar matahari pagi, dan pola makan sehat", "D. Mengonsumsi obat bius dan alkohol secara rutin"], ans: 2, type: "MOTS", bahas: "Gaya hidup sehat (olahraga, aktivitas sosial, sinar matahari, nutrisi) adalah pemicu alami terkuat agar tubuh optimal memproduksi happy hormones." }
        ];

        // --- VARIABEL GLOBAL ---
        let namaSiswa = "";
        let emailSiswa = "";
        let totalTime = 45 * 60; // 45 Menit
        let timerInterval;
        let isExamActive = false;
        let cheatCount = 0;
        let currentIndex = 0;
        let answers = new Array(bankSoal.length).fill(null);

        // --- FUNGSI ACAK (RANDOMIZER) ---
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }

        function acakSoalDanOpsi() {
            shuffleArray(bankSoal);
            bankSoal.forEach(q => {
                let correctAnswerText = q.opt[q.ans];
                shuffleArray(q.opt);
                q.ans = q.opt.indexOf(correctAnswerText); 
            });
        }

        // --- FUNGSI UTAMA ---
        function mulaiUjian() {
            namaSiswa = document.getElementById("nama").value.trim();
            emailSiswa = document.getElementById("email").value.trim();
            
            if (!namaSiswa || !emailSiswa) {
                alert("Harap isi Nama dan Email dengan lengkap!");
                return;
            }

            acakSoalDanOpsi();

            let elem = document.documentElement;
            if (elem.requestFullscreen) { elem.requestFullscreen(); }
            else if (elem.webkitRequestFullscreen) { elem.webkitRequestFullscreen(); }
            else if (elem.msRequestFullscreen) { elem.msRequestFullscreen(); }

            document.getElementById("loginPage").classList.add("hidden");
            document.getElementById("examPage").classList.remove("hidden");
            document.getElementById("identitasSiswa").innerText = `${namaSiswa} | ${emailSiswa}`;
            
            isExamActive = true;
            buatPanelNavigasi();
            tampilkanSoal(0);
            
            timerInterval = setInterval(updateTimer, 1000);
        }

        // --- NAVIGASI SOAL ---
        function buatPanelNavigasi() {
            const panel = document.getElementById("panelGrid");
            panel.innerHTML = "";
            for (let i = 0; i < bankSoal.length; i++) {
                const btn = document.createElement("div");
                btn.className = "btn-nav";
                btn.innerText = i + 1;
                btn.id = "navBtn_" + i;
                btn.onclick = () => tampilkanSoal(i);
                panel.appendChild(btn);
            }
        }

        function tampilkanSoal(index) {
            document.querySelectorAll(".btn-nav").forEach(el => el.classList.remove("current"));
            document.getElementById("navBtn_" + index).classList.add("current");
            
            currentIndex = index;
            const qData = bankSoal[index];
            
            const badge = document.getElementById("badgeDiff");
            badge.innerText = qData.type;
            badge.className = `badge-diff ${qData.type === 'LOTS' ? 'badge-lots' : 'badge-mots'}`;
            
            document.getElementById("questionText").innerHTML = `<b>Soal No ${index + 1}.</b><br>${qData.q}`;
            
            const optsContainer = document.getElementById("optionsContainer");
            optsContainer.innerHTML = "";
            
            qData.opt.forEach((opsi, i) => {
                const lbl = document.createElement("label");
                lbl.className = "option-label";
                if (answers[index] === i) lbl.classList.add("selected");
                
                const inp = document.createElement("input");
                inp.type = "radio";
                inp.name = "radioOpsi";
                inp.value = i;
                if (answers[index] === i) inp.checked = true;
                inp.onchange = () => pilihJawaban(index, i, lbl);
                
                let teksBersih = opsi.replace(/^[A-D]\.\s*/, "");
                let abjadBaru = String.fromCharCode(65 + i);
                
                lbl.appendChild(inp);
                lbl.appendChild(document.createTextNode(abjadBaru + ". " + teksBersih));
                optsContainer.appendChild(lbl);
            });

            document.getElementById("btnPrev").style.visibility = (index === 0) ? "hidden" : "visible";
            document.getElementById("btnNext").style.visibility = (index === bankSoal.length - 1) ? "hidden" : "visible";
        }

        function pilihJawaban(qIndex, optIndex, labelElement) {
            answers[qIndex] = optIndex;
            document.querySelectorAll(".option-label").forEach(el => el.classList.remove("selected"));
            labelElement.classList.add("selected");
            document.getElementById("navBtn_" + qIndex).classList.add("answered");
        }

        function changeQuestion(step) {
            let nextIndex = currentIndex + step;
            if (nextIndex >= 0 && nextIndex < bankSoal.length) tampilkanSoal(nextIndex);
        }

        function skipQuestion() {
            let found = false;
            for (let i = currentIndex + 1; i < bankSoal.length; i++) {
                if (answers[i] === null) {
                    tampilkanSoal(i);
                    found = true; break;
                }
            }
            if(!found) {
                for(let i = 0; i < bankSoal.length; i++){
                    if (answers[i] === null) {
                        tampilkanSoal(i);
                        found = true; break;
                    }
                }
            }
            if(!found) alert("Semua soal sudah dijawab! Silakan tekan tombol Selesai di bawah panel nomor.");
        }

        // --- TIMER ---
        function updateTimer() {
            if (totalTime <= 0) {
                kalkulasiDanKirim("Selesai Waktu Habis");
                return;
            }
            totalTime--;
            let m = Math.floor(totalTime / 60);
            let s = totalTime % 60;
            document.getElementById("timerDisplay").innerText = (m < 10 ? "0" + m : m) + ":" + (s < 10 ? "0" + s : s);
        }

        // --- ANTI CHEAT ---
        document.addEventListener("visibilitychange", () => {
            if (document.hidden && isExamActive) {
                cheatCount++;
                alert(`PELANGGARAN! Anda terdeteksi keluar dari layar ujian. Peringatan ke: ${cheatCount}/2`);
                if (cheatCount >= 2) {
                    alert("Anda Dikeluarkan dari Ujian (Diskualifikasi).");
                    kalkulasiDanKirim("Diskualifikasi");
                }
            }
        });
        history.pushState(null, null, location.href);
        window.onpopstate = function () { history.go(1); };

        // --- PENYELESAIAN ---
        function konfirmasiSelesai() {
            const blmDijawab = answers.filter(a => a === null).length;
            if (blmDijawab > 0) {
                if(!confirm(`Ada ${blmDijawab} soal belum dijawab! Yakin ingin menyelesaikan ujian?`)) return;
            } else {
                if(!confirm("Yakin ingin menyelesaikan ujian dan mengirim jawaban?")) return;
            }
            kalkulasiDanKirim("Selesai Normal");
        }

        // --- MODIFIKASI: KALKULASI & KIRIM VIA WHATSAPP ---
        function kalkulasiDanKirim(statusUjian) {
            isExamActive = false;
            clearInterval(timerInterval);
            
            let benar = 0;
            
            answers.forEach((ans, idx) => {
                let qData = bankSoal[idx];
                let isBenar = (ans === qData.ans);
                if (isBenar) benar++;
            });
            
            let nilaiAkhir = Math.round((benar / bankSoal.length) * 100);
            if (statusUjian === "Diskualifikasi") nilaiAkhir = 0;

            // Tampilkan hasil di halaman (juga menutup fullscreen secara otomatis)
            tampilkanHasilDanPembahasan(nilaiAkhir);

            // Format Pesan WhatsApp
            let nomorTujuan = "6281226260404";
            let teksPesan = `*Laporan Hasil Ujian IPA*\n\n` +
                            `Nama: ${namaSiswa}\n` +
                            `Email: ${emailSiswa}\n` +
                            `Status Ujian: ${statusUjian}\n` +
                            `*Nilai/Skor: ${nilaiAkhir}*`;
            
            // Encode teks menjadi URL format
            let linkWA = `https://api.whatsapp.com/send?phone=${nomorTujuan}&text=${encodeURIComponent(teksPesan)}`;
            
            // Buka tab baru yang mengarah langsung ke WhatsApp
            setTimeout(() => {
                window.open(linkWA, '_blank');
            }, 1000); // Beri jeda 1 detik agar layar exit fullscreen terlebih dahulu
        }

        function tampilkanHasilDanPembahasan(skorAkhir) {
            if (document.exitFullscreen) { document.exitFullscreen(); }
            else if (document.webkitExitFullscreen) { document.webkitExitFullscreen(); }

            document.getElementById("examPage").classList.add("hidden");
            document.getElementById("resultPage").classList.remove("hidden");
            
            document.getElementById("resNama").innerText = namaSiswa;
            document.getElementById("resSkor").innerText = skorAkhir;

            const box = document.getElementById("discussionContainer");
            box.innerHTML = "";

            bankSoal.forEach((q, i) => {
                const jwbSiswa = answers[i];
                const isBenar = jwbSiswa === q.ans;
                
                let jwbTeks = jwbSiswa !== null ? q.opt[jwbSiswa].replace(/^[A-D]\.\s*/, "") : "<i>Tidak Dijawab</i>";
                let kunciTeks = q.opt[q.ans].replace(/^[A-D]\.\s*/, "");
                
                const item = document.createElement("div");
                item.className = `result-item ${isBenar ? 'correct-ans' : 'wrong-ans'}`;
                
                item.innerHTML = `
                    <b>Soal No ${i + 1} (${q.type}) - <small style="color:#666;">ID Soal Asli: ${q.id}</small></b>
                    <p>${q.q}</p>
                    <p>Jawaban Anda: <b>${jwbTeks}</b> ${isBenar ? '✅' : '❌'}</p>
                    <p>Kunci Jawaban: <b>${kunciTeks}</b></p>
                    <div class="discussion"><b>Pembahasan:</b> ${q.bahas}</div>
                `;
                box.appendChild(item);
            });
        }
    </script>
</body>
</html>
