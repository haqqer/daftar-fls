<template>
  <v-layout column justify-center align-center class="mt-3">
    <h2 class="display-1">Pendaftaran Delegates FLS 2019</h2>
    <v-flex xs12 sm8 md6 >
      <br class="my-2">
      <v-card>
        <v-chip style="margin-top: -16px;" class="ml-4" label color="primary" text-color="white">
          <div class="subheading">
            Syarat dan Ketentuan
          </div>
        </v-chip>
        <v-card-text>
          <p>
          </p>
          <p>
            <v-icon small>fiber_manual_record</v-icon> Mempunyai ketertarikan dalam isu sosial sesuai room Future Leader Summit 2019
          </p>
          <p>
            <v-icon small>fiber_manual_record</v-icon> Siap berkontribusi dan berjejaring di Future Leader Summit 2019
          </p>
          <p>
            <v-icon small>fiber_manual_record</v-icon> Mengikuti peraturan kebijakan dan alur pendaftaran
          </p>
            <v-icon small>fiber_manual_record</v-icon> Pemuda/pemudi berusia 18-25 tahun
          <p>
            <v-icon small>fiber_manual_record</v-icon> Bersedia membayar commitment fee, jika terpilih menjadi delegates
          </p>
        </v-card-text>
      </v-card>
      <br class="my-4">
      <v-card>
        <v-chip style="margin-top: -16px;" class="ml-4" label color="primary" text-color="white">
          <div class="subheading">
            Tahap Pendaftaran
          </div>
        </v-chip>
        <v-card-text>
          <p>
            <v-icon small>fiber_manual_record</v-icon>
            Follow fanspage dan instagram Future Leader Summit 2019 : Future Leader Summit
            <br>
            <a class="ml-4 info--text" href="https://www.facebook.com/FutureLeaderSummit/" style="text-decoration: none;">
              <v-icon color="info">fa fa-facebook-square</v-icon>
              @FutureLeaderSummit
              </a>
            <br>
            <a class="ml-4 primary--text" href="https://www.instagram.com/flsummit/" style="text-decoration: none;">
              <v-icon color="primary">fa fa-instagram</v-icon>
              @flsummit
            </a>
          </p>
          <p>
            <v-icon small>fiber_manual_record</v-icon>
            Daftar online melalui tombol link di bawah
          </p>
          <p>
            <v-icon small>fiber_manual_record</v-icon>
            Setelah itu akan langsung mendapatkan konfirmasi melalui website dan email
          </p>
          <p class="mb-0">
            <v-icon small>fiber_manual_record</v-icon>
            Download poster yang telah disediakan 
            <a href="https://drive.google.com/file/d/1mNXCaQu-bqj_7yanwYbGeb0j5goQOBK5/view?usp=sharing" 
              target="blank_"
              download>di sini</a>, 
              kemudian upload di instagram kamu dengan caption berikut, lalu tag akun Future Leader Summit @FLSummit dan 5 teman kamu!
          </p>
          <blockquote class="blockquote mt-0">
            &#8220;
            <br> I have dared myself to take the opportunity to become a world change agent by registering Future Leader Summit 2019. How about you? Challenge yourself now!
            <footer>
              <small>
                #ThinkTheUnthinkable
                <br>#FutureLeaderSummit
                <br>#FLS2019
              </small>
            </footer>
            &#8221;
          </blockquote>
          <p>
            <v-icon small>fiber_manual_record</v-icon>
            Pengumuman penerimaan delegates akan diumumkan melalui email dan website resmi Future Leader Summit 2019
          </p>
          <p>
            <v-icon small>fiber_manual_record</v-icon>
            Setelah pengumuman penerimaan delegates via email dan website Future Leader Summit 2019, delegates terpilih wajib melakukan konfrimasi dan pembayaran maksimal 7x24 jam via email Person In Delegates masing-masing room.
          </p>
          <p>
            <v-icon small>fiber_manual_record</v-icon>
            Peserta waiting list akan dihubungi ketika ada calon delegates yang mengundurkan diri
          </p>
        </v-card-text>
      </v-card>
      <br class="mb-1">
      <v-card>
        <v-card-text>
          <h3 class="text-xs-center">Think The Unthinkable</h3>
        </v-card-text>
        <v-card-actions>
          <v-layout justify-center>
            <v-btn color="primary" large round nuxt to="/daftar">Daftar Sekarang</v-btn>
          </v-layout>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  components: {
    Logo,
    VuetifyLogo
  }
}
</script>
<style scoped>
          .container{
            height: 40%;
            width: 40px;
            background-image: url('/images/background.svg')
          }
</style>
