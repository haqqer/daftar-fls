<template>
  <v-container mt-5 pt-5>
    <v-layout
      wrap=""
      text-center
      justify-center
    >
    <v-flex xs12 md6 pr-1>
        <v-card flat>
          <v-card-text>
            <div class="subheading">
              Silahkan bisa mengecek, apakah kamu sudah terdaftar apa belum dengan masukan email dan Nomor hp kamu, dibawah ini
            </div>
            <v-text-field
              v-model="email"
              v-validate="'required|email'"
              :error-messages="errors.collect('email')"
              data-vv-name="email"
              data-vv-as="Email"
              label="Email"></v-text-field>
            <v-text-field
              v-model="phone"
              :error-messages="errors.collect('phone')"
              v-validate="'required|numeric'"
              data-vv-name="phone"
              data-vv-as="Phone"
              label="No Hp"></v-text-field>              
            <v-btn color="primary" @click="submitDelegate" block round depressed>kirim</v-btn>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
    <v-dialog v-model="dialog" width="75vw">
      <v-layout justify-center>
        <v-flex >
      <v-card v-if="dialog == true">
        <v-card-title primary-title>
          <h3 class="headline">Data Anda!</h3> 
        </v-card-title>
        <v-card-text>
          <div class="body-2"><b>Nama Lengkap</b></div>
          <p>{{ delegate.fullName }}</p>
          <div class="body-2"><b>Nama Panggilan</b></div>
          <p>{{ delegate.nickName }}</p>
          <div class="body-2"><b>Email</b></div>
          <p>{{ delegate.email }}</p>          
          <div class="body-2"><b>Phone</b></div>
          <p>{{ delegate.phone }}</p> 
          <div class="body-2"><b>Tempat Lahir</b></div>
          <p>{{ delegate.placeOfBirth }}</p>
          <div class="body-2"><b>Tanggal Lahir</b></div>
          <p>{{ delegate.dateOfBirth | moment("DD MMMM YYYY") }}</p>
          <div class="body-2"><b>Gender</b></div>
          <p>{{ getGender(delegate.gender) }}</p>
          <div class="body-2"><b>Alamat Domisili</b></div>
          <p>{{ delegate.domicileAddress }}</p>
          <div class="body-2"><b>Provinsi</b></div>
          <p>{{ delegate.province }}</p>
          <div class="body-2"><b>Kota</b></div>
          <p>{{ delegate.city }}</p>
          <div class="body-2"><b>Institusi</b></div>
          <p>{{ delegate.institution }}</p>
          <div class="body-2"><b>Room pilihan</b></div>
          <p>{{ getRoom(delegate.room.firstRoom) }}</p>
          <div class="body-2"><b>Motivasi ikut FLS 2019</b></div>
          <p>{{ delegate.essay.essayMotivationJoin }}</p>
          <div class="body-2"><b>Alasan memilih room</b></div>
          <p>{{ delegate.essay.essayRoomSelected }}</p>
          <div class="body-2"><b>Jawaban Studi Kasus</b></div>
          <p>{{ delegate.essay.essayCaseStudy }}</p>
        </v-card-text>
        <v-card-actions>
          <v-btn round block color="primary" dark @click="resendEmail()">Kirim ulang emailku</v-btn>
        </v-card-actions>
      </v-card>
        </v-flex>
      </v-layout>
    </v-dialog>
  </v-container>
</template>

<script>
import swal from 'sweetalert2'

export default {
  data: () => ({
    dialog: false,
    email: '',
    phone: '',
    delegate: {
        fullName: '',
        nickName: '',
        placeOfBirth: '',
        dateOfBirth: '',
        gender: '',
        domicileAddress: '',
        province: '',
        regency: '',
        city: '',
        institution: '',
        phone: '',
        email: '',
        room: {
          firstRoom: '',
          secondRoom: '',
        },        
        socmed: '',
        essay: {
          essayMotivationJoin: '',
          essayRoomSelected: '',
          essayCaseStudy: ''
        },
        Organizations: '',
        SocialActivities: '',
        Achievements: '',              
    },
    baseURL: 'https://api.futureleadersummit.org/data'     
  }),
  methods: {
    submitDelegate() {
      this.dialog=true
      this.$validator.validateAll().then((result) => {
        if(!result) {
          swal.fire('Error', 'Lengkapi dulu ya', 'error')
        } else {
          this.$axios.post('https://api.futureleadersummit.org/delegates/send', {
            email: this.email,
            phone: this.phone,
          }).then((response) => {
            const result = response.data
            // this.clearDelegate()
            // console.log(result)
            this.delegate = result.data
            this.getProvince(this.delegate.province);
            this.getCity(this.delegate.city);
            console.log('[delegate]',this.delegate)
          }).catch((error) => {
            this.dialog = false;
            swal.fire('Maaf', 'Sepertinya anda belum terdaftar 😟' ,'error')
            console.log(error.response)
          })          
        }
      })
    },
    async resendEmail() {
      this.$axios.post('https://api.futureleadersummit.org/delegates/send', {
        email: this.delegate.email,
        phone: this.delegate.phone,
        send: true
      }).then((response) => {
        const result = response.data
        swal.fire('Success', 'Hore, email mu akan segera dikirim ulang ditunggu ya 😃')
      }).catch((error) => {
        swal.fire('Error', 'Data tidak ditemukan' ,'error')
        console.log(error.response)
      })       
    },
    getDelegate() {
      console.log(this.$route.query == {})
      if(this.$route.query != {}) {
        this.fullName = this.$route.query.fullName
        this.nickName = this.$route.query.nickName
        this.email = this.$route.query.email        
      }
    },
    clearDelegate() {
      this.fullName, this.nickName, this.email, this.message = ''
    },
    getGender(gender) {
      if(gender == 0) {
        return 'Laki-laki'
      }else {
        return 'Perempuan'
      }
      
    },
    fetchDataUniversities (institution) {
      this.loadingUniversity = true
      this.$axios.get(this.baseURL+'/universities', {
        params: {
          name: institution
        }
      }).then(result => {
        const response = result.data;
        console.log('universitas ', response.data);
        return response.data.nama
        // this.institutionItems = response.data
        // console.log(this.institutionItems);
        // if (this.institutionItems.length < 1 && this.searchInstitutions) {
        //   this.institutionItems.push({ id: 'otherInstitution', name: this.searchInstitutions })
        // }
      }).catch(error => {
        console.log('err provinsi ', error)
      })
    },
    fetchDataProvinces () {
      this.loadingProvince = true
      this.$axios.get(this.baseURL+'/provinces', {
        params: {
          name: this.searchProvince
        }
      }).then(result => {
        // console.log(result);
        const response = result.data;
        console.log('provinsi ', response.data);
        return response.data.name;
      }).catch(error => {
        console.log('err provinsi ', error)
      })
    },
    async getProvince(id) {
      const result = await this.$axios.get(this.baseURL+'/provinces/'+id)
      const province = result.data.data.name;
      this.delegate.province = province;
    },
    async getCity(id) {
      const result = await this.$axios.get(this.baseURL+'/regencies/'+id);
      const city = result.data.data.name;
      this.delegate.city = city;
    },
    getRoom(index) {
      const room = ["Digital", "Education", "Enviroment", "International_Relation", "Technopreneur","Urban_Planning"];
      console.log(room[index-1]);
      return room[index-1];
    }      
  },
  mounted() {
    this.getDelegate()
  }
};
</script>
<style>
  td, th {
    font-size: 1.3em
  }
</style>

