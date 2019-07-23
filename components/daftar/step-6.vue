<template>
  <div>
    <div class="subheading primary__dark--text">Apa motivasi kamu mengikuti FLS 2019?</div>
    <v-text-field
      v-model="model.essayMotivationJoin"
      data-vv-as="Jawaban Motivasi"
      :error-messages="errors.collect('motivationJoin')"
      multi-line
      counter="1500"
      v-validate="'required|max:1500'"
      data-vv-name="motivationJoin"
      placeholder="Motivasi"
      class="pa-0"
    ></v-text-field>

    <div class="subheading primary__dark--text mt-4">Mengapa kamu memilih room tersebut?</div>
    <v-text-field
      v-model="model.essayRoomSelected"
      data-vv-as="Jawaban Alasan"
      :error-messages="errors.collect('roomSelected')"
      multi-line
      counter="1500"
      v-validate="'required|max:1500'"
      data-vv-name="roomSelected"
      placeholder="Alasan"
      class="pa-0"
    ></v-text-field>

    <div class="title primary__dark--text mt-4">Studi Kasus Room</div>

    <div v-html="caseStudyQuestion" class="subheading primary__dark--text mt-4"></div>
    <v-text-field
      v-model="model.essayCaseStudy"
      data-vv-as="Studi kasus"
      :error-messages="errors.collect('caseStudy')"
      multi-line
      counter="1500"
      v-validate="'required|max:1500'"
      data-vv-name="caseStudy"
      placeholder="Jawaban"
      class="pa-0"
    ></v-text-field>
  </div>
</template>

<script>
export default {
  data () {
    return {
      model: {
        essayMotivationJoin: '',
        essayRoomSelected: '',
        essayCaseStudy: ''
      },
      tes: `<strong>dodo</strong>`
    }
  },
  computed: {
    roomSelected () {
      return this.$store.state.roomSelected
    },
    caseStudyQuestion () {
      switch (this.roomSelected) {
        case 1:
          return `
            <h3>Digital</h3>
            <p>Tren Internet of Things (IoT) merambah hampir di semua lini kehidupan. Contoh nyatanya pun semakin terlihat dengan banyaknya perangkat-perangkat terkoneksi yang tersebar dan digunakan oleh banyak orang di dunia, tak terkecuali di Indonesia. Hal ini terjadi seiring dengan peningkatan konektivitas jaringan internet. Data dari IDC menyebutkan bahwa perangkat IoT di Asia Pasifik (termasuk Indonesia) diproyeksikan akan bertambah dari 3,1 miliar perangkat menjadi 8,6 miliar perangkat pada tahun 2015-2020. Begitu pula dengan pertumbuhan pasar dari USD 250 miliar menjadi USD 583 miliar pada kurun waktu yang sama.</p>

            <p>Pangsa pasar IoT di Indonesia diperkirakan berkembang pesat dan nilainya bakal mencapai Rp444 triliun pada tahun 2022. Nilai tersebut disumbang dari konten dan aplikasi sebesar Rp192,1 triliun, disusul platform Rp156,8 triliun, perangkat IoT Rp56 triliun, serta network dan gateway Rp39,1 triliun. (sumber: kemenperin.go.id)</p>

            <p>Internet of Things bukan saja melulu mengenai "Things" atau perangkatnya, melainkan aplikasi dan layanan yang menjadi pendukung dari IoT. Semakin banyak perangkat terkoneksi, maka akan semakin banyak pula aplikasi dan layanan yang berjalan. Seperti misalnya, penghitungan meteran listrik otomatis, jam tangan pintar yang dapat mengukur detak jantung dan langsung menampilkan hasilnya di layar ponsel, dan sebagainya. Di baliknya, terdapat berbagai aplikasi yang bekerja secara simultan atau pun bersamaan untuk menghasilkan data-data tersebut.</p>
            
            <p>Namun, di baliknya, tersembunyi potensi ancaman terhadap keamanan data, keamanan fisik, keamanan dari perangkat, regulasi, privasi, enkripsi, otentikasi, dan segudang ancaman lain yang perlu ditangani agar kendala tersebut tidak mengganggu di kemudian harinya.</p>
            
            <p>Bagaimana sikap dan strategi pendekatan seperti apa yang bisa anda tawarkan sebagai solusi dari ancaman terhadap keamanan data/privasi pengguna?</p>
          `
        
        case 2:
          return `
            <h3>Education</h3>
            <p>Bagaimana penerapan kurikulum yang tepat guna untuk menunjang pendidikan tinggi Indonesia dalam tuntutan era edukasi 4.0 dan apakah langkah yang diterapkan oleh pemerintah, perguruan tinggi dan institusi pendukung lainnya sudah sesuai dan siap untuk dijalankan di Indonesia dengan segala peraturan yang ada serta mempersiapkan indonesia bertanding dalam kompetensi ASEAN 2025?</p>
          `
        case 3:
          return `
            <h3>Environment</h3>
            <p>Masalah lingkungan yang kita hadapi dewasa ini seperti: deforestasi, pemanasan global dan pencemaran laut merupakan masalah multidimensi.</p>

            <p>Data dari Badan Nasional Penanggulangan Bencana, tahun 2018 sebanyak 2.426 kejadian bencana di Indonesia, 96,6% disebabkan oleh bencana Hidrometeorologi.</p>

            <p>Manusia dan seluruh aktifitasnya dari ruang lingkup produksi, distribusi, dan konsumsi memiliki andil besar dalam masalah lingkungan. </p>

            <p>Berdasarkan ruang lingkup tersebut, dapatkah anda menjelaskan masalah lingkungan hidup disekitar anda, serta bagaimana langkah solutif dalam upaya mewujudkan lingkungan hidup yang berkembang secara koheren dengan peradaban manusia?</p>
          `
        case 4:
          return `
            <h3>International Relation</h3>
            <p>Dalam visi ASEAN 2025 terdapat beberapa aspek yang menjadi sorotan utama yakni, aspek Political-Security, aspek Economic dan aspek sosio-cultural. Saat ini negara-negara ASEAN banyak menjalin kerjasama ekonomi dengan negara-negara Asia lainnya, salah satu negara yang aktif menjalin kerjasama dengan negara-negara ASEAN adalah Tiongkok. Berbagai jenis kerjasama yang dilakukan tentunya berimplikasi terhadap perekembangan pergerakan prekonomian kedua belah pihak yang bekerjasama. ASEAN di satu sisi beranggotakan negara-negara yang perekonomiannya belum mampu untuk membangun sendiri infrastrukturnya tanpa ada kerjasama, hal ini tentunya menyebabkan negara-negara ASEAN perlu bersanding dan bekerjasama dengan pihak yang mampu membantu dan menopang perekonomiannya. Kebangkitan Tiongkok, baik secara politik ataupun ekonomi merupakan peluang bagi negara-negara ASEAN untuk memajukan ekonomi dan kepentingan politiknya. Beberapa pihak memandang Tiongkok akan mengancam perekonomian ASEAN, namun sebaliknya justru keberadaan Tiongkok saat ini akan membantu ASEAN dalam mewujudkan mimpi-mimpinya menuju kebangkitan ASEAN. </p>

            <p>Saat ini pertumbuhan ekonomi politik negara-negara ASEAN dapat dikatakan dalam tahap stabil, ketika harga dollar melonjak tajam, perekonomian negara-negara ASEAN cenderung tidak goyah dengan hal tersebut, hal ini dapat dijadikan pertimbangan bahwa perekonomian negara-negara ASEAN sudah dalam tahap perkembangan yang pesat, dilansir dari Detik Finance (Detik Finance, 2018), kejatuhan ekonomi negara-negara ASEAN terhadap kenaikan dollar tidak diatas 1 %, hal ini membuktikan bahwa kemampuan ekonomi negara-negara ASEAN sudah melebihi standar sebelumnya, hal ini tentunya berkaitan dengan kerjasama-kerjasama ekonomi yang dijalin negara-negara ASEAN dengan negara-negara lainnya.</p>

            <p>Melalui situasi yang terjadi di atas, posisikan diri kamu sebagai seorang aktivis hubungan internasional, apa yang akan kamu lakukan dalam menanggapi persoalan yang terjadi di ASEAN saat ini dan berikan pemikiran baru mengenai apa yang akan menjadii tantangan utama negara-negara ASEAN pada saat ini?</p>
          `
        case 5:
          return `
            <h3>Technopreneur</h3>
            <p>Revolusi industri 4.0 telah mendorong kemajuan di berbagai bidang, salah satunya terkait ekonomi digital di ASEAN, dengan berkembangnya pengetahuan seputar Artificial Intellegence (AI), Virtual Reality, dan Big Data Analysis (sc :warta ekonomi, oktober 2018). Dengan adanya kemajuan teknologi di era 4.0, investasi global untuk startup teknologi di ASEAN meningkat hingga bernilai US10,1 miliar dan membuat ekonomi dalam negeri berkembang pesat. (sc: East vc). Investasi tersebut sangat penting bagi permodalan startup agar dapat bertahan ditengah persaingan bisnis yang semakin ketat. Di tengah berbagai fenomena tersebut, modal ventura semakin gencar memberikan suntikan dana untuk startup potensial. Di tengah kemajuan ekonomi digital di era 4.0, modal ventura menjadi semakin menjamur dan menjadi lading bisnis yang cukup menggiurkan. Dengan adanya fenomena tersebut, bagaimanakah pengaruh merajalelanya modal ventura terhadap keberlangsungan ekonomi suatu Negara?</p>
          `
        case 6:
          return `
            <h3>Urban Planning</h3>
            <p>Penduduk perkotaan akan merepresentasikan 45 persen dari populasi ASEAN yang mana jutaan orang, khususnya mereka yang tinggal di tempat yang rentan sepanjang tepi sungai, kanal, dan sisi lembah, akan terkena dampak berbahaya dari kerusakan lingkungan. Porsi rentan dari populasi ASEAN ini diperkirakan akan meningkat 50 persen di wilayah ibukota. Ketika bencana datang, yang akan terkena imbas terbesar adalah penduduk kurang mampu, karena mereka lebih rentan terhadap bahaya lingkungan dan membutuhkan waktu lebih lama untuk bangkit kembali dari krisis. Kota adalah wadah penyimpangan ketidaksetaraan dan resiko iklim hanya akan memperburuk ketidaksetaraan ini.</p>

            <p>Melihat kelamnya kondisi perkotaan sebagaimana tersebut diatas, bagaimana sikap & strategi pendekatan seperti apa yang bisa anda tawarkan pada peradaban untuk pembangunan perkotaan hingga dapat menjadi aspek pendukung 4 pilar Masyarakat Ekonomi ASEAN?</p>
          `
      }
    }
  },
  methods: {
    validate () {
      return new Promise((resolve, reject) => {
        this.$validator.validateAll().then((valid) => {
          let errors = this.errors.collect()
          resolve({ valid: valid, model: this.model, error: errors[Object.keys(errors)[0]]});
        });
      })
    }
  }
}
</script>
