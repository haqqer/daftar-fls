<template>
  <div>
    <div class="title primary__dark--text my-2">Data Diri</div>

    <v-text-field
      v-model="model.fullName"
      label="Nama Lengkap"
      data-vv-as="Nama Lengkap"
      :error-messages="errors.collect('name')"
      v-validate="'required'"
      data-vv-name="name"
    ></v-text-field>

    <v-text-field
      v-model="model.nickName"
      label="Nama Panggilan"
      data-vv-as="Nama Panggilan"
      :error-messages="errors.collect('nickName')"
      v-validate="'required'"
      data-vv-name="nickName"
    ></v-text-field>

    <v-select
      :items="placeOfBirthItems"
      :search-input.sync="searchPlaceOfBirth"
      autocomplete
      v-model="model.placeOfBirth"
      data-vv-as="Tempat Lahir"
      :error-messages="errors.collect('placeOfBirth')"
      v-validate="'required'"
      data-vv-name="placeOfBirth"
      label="Tempat Lahir"
      :loading="loadingPlaceOfBirth"
      item-value="name"
      item-text="name"
      @keyup="placeOfBirthItems.push({ id: 'search', name: 'loading' })"
    >
      <div slot="no-data" @click="applyOtherPlaceOfBirth()">{{ loadingPlaceOfBirth ? 'Loading...' : searchPlaceOfBirth }}</div>
    </v-select>

    <v-menu
      ref="menu"
      lazy
      :close-on-content-click="false"
      v-model="menuDateOfBirth"
      transition="scale-transition"
      full-width
      :nudge-right="40"
      min-width="290px"
    >
      <v-text-field
        slot="activator"
        label="Tanggal Lahir"
        v-model="model.dateOfBirth"
        data-vv-as="Tanggal Lahir"
        :error-messages="errors.collect('dateOfBirth')"
        v-validate="'required'"
        data-vv-name="dateOfBirth"
        readonly
      ></v-text-field>
      <v-date-picker
        ref="picker"
        v-model="model.dateOfBirth"
        @change="saveDateOfBirth"
        min="1993-01-01"
        :max="new Date().toISOString().substr(0, 10)"
      ></v-date-picker>
    </v-menu>

    <v-select
      :items="genderItems"
      v-model="model.gender"
      data-vv-as="Jenis Kelamin"
      :error-messages="errors.collect('gender')"
      v-validate="'required'"
      data-vv-name="gender"
      label="Jenis Kelamin"
      item-value="id"
      item-text="alias"
    ></v-select>

    <div class="title primary__dark--text my-2">Alamat Domisili</div>
    <v-select
      :items="provinceItems"
      :search-input.sync="searchProvince"
      autocomplete
      item-value="id"
      item-text="name"
      :loading="loadingProvince"
      v-model="model.province"
      data-vv-as="Provinsi"
      :error-messages="errors.collect('province')"
      v-validate="'required'"
      data-vv-name="province"
      label="Provinsi"
      @keyup="provinceItems.push({ id: 'search', name: 'loading' })"
    >
      <div slot="no-data" @click="applyOtherProvince()">{{ loadingProvince ? 'Loading...' : searchProvince }}</div>    
    </v-select>
    <v-select
      :items="regencyItems"
      :search-input.sync="searchRegency"
      autocomplete
      item-value="id"
      item-text="name"
      :loading="loadingRegency"
      v-model="model.regency"
      data-vv-as="Kota/Kabupaten"
      :error-messages="errors.collect('regency')"
      v-validate="'required'"
      data-vv-name="regency"
      label="Kota/Kabupaten"
      @keyup="regencyItems.push({ id: 'search', name: 'loading' })"
    >
      <div slot="no-data" @click="applyOtherRegency()">{{ loadingRegency ? 'Loading...' : searchRegency }}</div>
    </v-select>
    <v-text-field
      v-model="model.domicileAddress"
      :error-messages="errors.collect('address')"
      v-validate="'required'"
      data-vv-name="address"
      data-vv-as="Alamat"
      label="Alamat">
    </v-text-field>

    <div class="title primary__dark--text my-2">Institusi</div>
    <v-select
      :items="institutionItems"
      :search-input.sync="searchInstitutions"
      autocomplete
      :no-data-text="loadingUniversity ? 'Loading...' : searchInstitutions"
      v-model="model.institution"
      data-vv-as="Sekolah/Universitas"
      :error-messages="errors.collect('institution')"
      v-validate="'required'"
      data-vv-name="institution"
      label="Sekolah/Universitas"
      :loading="loadingUniversity"
      item-value="nama"
      item-text="nama"
      @keyup="institutionItems.push({ id: 'search', name: 'loading' })"
    >
      <div slot="no-data" @click="applyOtherInstitution()">{{ loadingUniversity ? 'Loading...' : searchInstitutions }}</div>
    </v-select>

    <div class="title primary__dark--text my-2">Kontak</div>
    <v-text-field
      v-model="model.phone"
      label="Nomor Telepon"
      data-vv-as="Nomor Telepon"
      :error-messages="errors.collect('phone')"
      v-validate="'required|numeric'"
      data-vv-name="phone"
    ></v-text-field>
    <v-text-field
      v-model="model.email"
      type="email"
      label="Email"
      data-vv-as="Email"
      :error-messages="errorEmail"
      v-validate="'required|email'"
      data-vv-name="email"
      data-vv-delay="700"
    ></v-text-field>
    <v-text-field
      v-model="model.socmed.instagram"
      label="Akun Instagram"
      data-vv-as="Akun Instagram"
      :error-messages="errors.collect('instagram')"
      v-validate="'required'"
      data-vv-name="instagram"
      prefix="@"
    ></v-text-field>
    <v-text-field
      v-model="model.socmed.facebook"
      label="Akun Facebook"
      data-vv-as="Akun Facebook"
      :error-messages="errors.collect('facebook')"
      v-validate="'required'"
      data-vv-name="facebook"
    ></v-text-field>
    <v-text-field
      v-model="model.socmed.twitter"
      label="Akun Twitter"
      data-vv-as="Akun Twitter"
      :error-messages="errors.collect('twitter')"
      v-validate="'required'"
      data-vv-name="twitter"
    ></v-text-field>        
    <v-text-field
      v-model="model.socmed.line"
      label="Akun Line"
      data-vv-as="Akun Line"
      :error-messages="errors.collect('line')"
      v-validate="'required'"
      data-vv-name="line"
    ></v-text-field>

  </div>
</template>

<script>
import swal from 'sweetalert2'
import _debounce from 'lodash/debounce'
import _orderBy from 'lodash/orderBy'

export default {
  data () {
    return {
      model: {
        fullName: '',
        nickName: '',
        placeOfBirth: '',
        dateOfBirth: '',
        gender: '',
        domicileAddress: '',
        province: '',
        regency: '',
        institution: '',
        phone: '',
        email: '',
        socmed: {
          instagram: '',
          facebook: '',
          line: '',
          twitter: '',
          telegram: ''
        },
      },
      loadingCheckEmail: false,
      loadingPlaceOfBirth: false,
      loadingProvince: false,
      loadingRegency: false,
      loadingUniversity: false,
      searchPlaceOfBirth: '',
      searchRegency: '',
      searchInstitutions: '',
      searchProvince: '',
      placeOfBirthItems: [],
      regencyItems: [],
      provinceItems: [],
      institutionItems: [],
      menuDateOfBirth: false,
      genderItems: [
        { id: 0, name: 'male', alias: 'Laki-Laki' },
        { id: 1, name: 'female', alias: 'Perempuan' }
      ],
      baseURL: 'https://api.futureleadersummit.org/data'
    }
  },
  computed: {
    errorEmail () {
      if(!this.loadingCheckEmail) return this.errors.collect('email')
    }
  },
  watch: {
    menuDateOfBirth (val) {
      val && this.$nextTick(() => (this.$refs.picker.activePicker = 'YEAR'))
    },
    // 'model.province' (val) {
    //   if (val) this.fetchDataRegencies()
    // },
    searchPlaceOfBirth: _debounce(function (e) {
      e && this.fetchDataPlaceOfBirth()
    }, 500),
    searchInstitutions: _debounce(function (e) {
      e && this.fetchDataUniversities()
    }, 500),
    searchRegency: _debounce(function (e) {
      e && this.fetchDataRegencies()
    }, 500),
    searchProvince: _debounce(function (e) {
      e && this.fetchDataProvinces()
    }, 500)
  },
  methods: {
    saveDateOfBirth (date) {
      this.$refs.menu.save(date)
    },
    validate () {
      return new Promise((resolve, reject) => {
        this.$validator.validateAll().then((valid) => {
          let errors = this.errors.collect()
          resolve({ valid: valid, model: this.model, error: errors[Object.keys(errors)[0]]});
        });
      })
    },
    fetchDataPlaceOfBirth () {
      this.loadingPlaceOfBirth = true
      this.$axios.get(this.baseURL+'/regencies', {
        params: {
          limit: 20,
          name: this.searchPlaceOfBirth
        }
      }).then(result => {
        const response = result.data
        console.log('tmpt lahir ', response.data);
        this.placeOfBirthItems = response.data
        if (this.placeOfBirthItems.length < 1 && this.searchPlaceOfBirth) {
          this.placeOfBirthItems.push({ id: 'othePlaceOfBirth', name: this.searchPlaceOfBirth.toUpperCase() })
        }
        this.loadingPlaceOfBirth = false
      }).catch(error => {
        console.log('err tmpt lahir ', error)
        this.loadingPlaceOfBirth = false
      })
    },
    fetchDataUniversities () {
      this.loadingUniversity = true
      this.$axios.get(this.baseURL+'/universities', {
        params: {
          name: this.searchInstitutions
        }
      }).then(result => {
        const response = result.data;
        console.log('universitas ', response.data);
        this.institutionItems = response.data
        console.log(this.institutionItems);
        if (this.institutionItems.length < 1 && this.searchInstitutions) {
          this.institutionItems.push({ id: 'otherInstitution', name: this.searchInstitutions })
        }
        this.loadingUniversity = false
      }).catch(error => {
        console.log('err provinsi ', error)
        this.loadingUniversity = false
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
        this.provinceItems = response.data
        console.log(this.provinceItems);
        if (this.provinceItems.length < 1 &&  this.searchProvince) {
          this.provinceItems.push({ id: 'otherProvince', name: this.searchProvince.toUpperCase() })
        }
        this.loadingProvince = false
      }).catch(error => {
        console.log('err provinsi ', error)
        this.loadingProvince = false
      })
    },
    fetchDataRegencies () {
      this.loadingRegency = true
      console.log(this.model.province);
      this.$axios.get(this.baseURL+'/regencies', {
        params: {
          limit: 20,
          province_id: this.model.province || '100',
          name: this.searchProvince
        }
      }).then(result => {
        const response = result.data
        console.log('regency ', response.data);
        this.regencyItems = response.data
        if (this.regencyItems.length < 1 && this.searchRegency) {
          console.log('trigger if')
          this.regencyItems.push({ id: 'otherRegency', name: this.searchRegency.toUpperCase() })
        }
        this.loadingRegency = false
      }).catch(error => {
        console.log('err regency ', error)
        this.loadingRegency = false
      })
    },
    applyOtherInstitution () {
      this.model.institution = this.searchInstitutions
    },
    applyOtherPlaceOfBirth () {
      this.model.placeOfBirth = this.searchPlaceOfBirth
    },
    applyOtherRegency () {
      this.model.regency = this.regencyItems
    },
    applyOtherProvince () {
      console.log('trigger 2')
      this.model.province = this.provinceItems
    },    
    checkValidEmail () {
      this.loadingCheckEmail = true
      return this.$axios.$get('http://128.199.72.101:3000/api/Registrars/check-email', {
        params: { email: this.model.email }
      }).then(response => {
        this.loadingCheckEmail = false
        return {
          valid: response.valid,
          data: {
            message: response.message
          }
        };
      }).catch(error => {
        this.loadingCheckEmail = false
        if (error.response) {
          return {
            valid: false,
            data: {
              message: error.response.data.error.message
            }
          }
        }
        return {
          valid: false,
          data: {
            message: error.message
          }
        }
      })
    },
  },
  mounted () {
    this.fetchDataProvinces()
    // this.$validator.extend('unique', {
    //   validate: this.checkValidEmail,
    //   getMessage: (field, params, data) => data.message
    // });
  }
}
</script>
