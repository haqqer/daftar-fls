<template>
  <v-container mt-5 pt-5>
    <v-layout
      wrap=""
      text-center
      justify-center
    >
    <v-flex xs10 md6 pr-5>
        <v-card flat>
          <v-card-text>
            <div class="headline">
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
    <v-dialog v-model="dialog" max-width="50vw">
      <v-tabs background-color="deep-purple accent-4" class="elevation-2" grow :icons-and-text="true" vertical centered>
        <v-tab>
          Biodata <v-icon>contact</v-icon> 
        </v-tab>
        <v-tab>
          Biodata <v-icon>people</v-icon> 
        </v-tab>
        <v-tab>
          Biodata <v-icon>people</v-icon> 
        </v-tab>
      </v-tabs>
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
        city: '',
        institution: '',
        phone: '',
        email: '',
        Room: {
          firstRoom: '',
          secondRoom: '',
        },        
        Socmed: '',
        Essay: {
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
            console.log('[delegate]',this.delegate)
          }).catch((error) => {
            swal.fire('Error', 'Sistem Error' ,'error')
            console.log(error.response)
          })          
        }
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
      if(gender == '') {
        return ''
      }
      if(gender == 0) {
        return 'Laki-laki'
      }
      return 'Perempuan'
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

