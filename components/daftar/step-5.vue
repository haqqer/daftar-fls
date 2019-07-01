<template>
  <div>
    <div class="body-2 primary__dark--text">
      <v-icon small>help</v-icon>
      Kamu bisa menambahkan maksimal 5
    </div>
    <v-card v-for="(socialActivity, index) in model.socialActivities" :key="index" class="fls-form-group my-2">
      <v-card-title>
        <v-spacer></v-spacer>
        <v-btn color="error" small icon @click="removeFormSocialActivity(index)"><v-icon small>delete</v-icon></v-btn>
      </v-card-title>
      <v-card-text>
        <v-text-field
          v-model="socialActivity.name"
          label="Kegiatan"
          data-vv-as="Kegiatan"
          :error-messages="errors.collect('name' + index)"
          v-validate="'required'"
          :data-vv-name="'name' + index"
          required
        ></v-text-field>
        <v-select
          :items="levelItems"
          v-model="socialActivity.level"
          data-vv-as="Tingkat"
          :error-messages="errors.collect('level' + index)"
          v-validate="'required'"
          :data-vv-name="'level' + index"
          label="Tingkat"
          item-value="id"
          item-text="name"          
        ></v-select>
        <v-select
          :items="positionItems"
          v-model="socialActivity.level"
          data-vv-as="Jabatan"
          :error-messages="errors.collect('position' + index)"
          v-validate="'required'"
          :data-vv-name="'position' + index"
          label="Jabatan"
          item-value="name"
          item-text="name"            
        ></v-select>        
        <v-select
          :items="yearItems"
          v-model="socialActivity.period"
          label="Tahun"
          data-vv-as="Tahun"
          :error-messages="errors.collect('year' + index)"
          v-validate="'required'"
          :data-vv-name="'year' + index"
          required
        ></v-select>
      </v-card-text>

    </v-card>
    <v-btn v-if="this.model.socialActivities.length < 5" block @click="newFormSocialActivity()" color="info" round>Tambah</v-btn>
  </div>
</template>

<script>
export default {
  data () {
    return {
      model: {
        socialActivities: []
      },
      levelItems: [
        {
          id: 1,
          name: 'Internasional'
        },
        {
          id: 2,
          name: 'Nasional'
        },
        {
          id: 3,
          name: 'Daerah'
        },
        {
          id: 4,
          name: 'Universitas'
        },
        {
          id: 5,
          name: 'Sekolah'
        }
      ],    
      positionItems: [
        {
          id: 1,
          name: 'Ketua'
        },
        { id: 2,
          name: 'Wakil Ketua'
        },
        {
          id: 3,
          name: 'Sekretaris'
        },
        { id: 4,
          name: 'Bendahara'
        },
        { id: 5,
          name: 'Menteri'
        },
        { id: 6,
          name: 'Kabid'
        },
        { id: 7,
          name: 'Wakil Menteri'
        },
        { id: 8,
          name: 'Wakil Bidang'
        },
        { id: 9,
          name: 'Kadiv'
        },
        { id: 10,
          name: 'Staff Ahli'
        },
        { id: 11,
          name: 'Anggota/Staff'
        }
      ],      
      yearItems: [
        2019,
        2018,
        2017,
        2016,
        2015,
        2014,
        2013,
        2012,
        2011,
        2010
      ]
    }
  },
  methods: {
    newFormSocialActivity () {
      if (this.model.socialActivities.length < 5) {
        this.model.socialActivities.push({
          name: '',
          year: '',
          level: ''
        })
      }
    },
    removeFormSocialActivity (index) {
      this.model.socialActivities.splice(index, 1)
    },
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
