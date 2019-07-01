<template>
  <div>
    <div class="body-2 primary__dark--text">
      <v-icon small>help</v-icon>
      Kamu bisa menambahkan maksimal 5 organisasi
    </div>
    <v-card v-for="(organization, index) in model.organizations" :key="index" class="fls-form-group elevation-3 my-2">
      <v-card-title>
        <v-spacer></v-spacer>
        <v-btn color="error" small icon @click="removeFormOrganization(index)"><v-icon small>delete</v-icon></v-btn>
      </v-card-title>
      <v-card-text>
        <v-text-field
          v-model="organization.name"
          label="Nama Organisasi"
          data-vv-as="Nama Organisasi"
          :error-messages="errors.collect('name' + index)"
          v-validate="'required'"
          :data-vv-name="'name' + index"
          required
        ></v-text-field>
        <v-select
          :items="levelItems"
          v-model="organization.level"
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
          v-model="organization.position"
          data-vv-as="Jabatan"
          :error-messages="errors.collect('position' + index)"
          v-validate="'required'"
          :data-vv-name="'position' + index"
          label="Jabatan"
          item-value="name"
          item-text="name"            
        ></v-select>
        <v-text-field
          v-model="organization.period"
          label="Periode"
          data-vv-as="Periode"
          :error-messages="errors.collect('period' + index)"
          v-validate="'required'"
          :data-vv-name="'period' + index"
          required
        ></v-text-field>
      </v-card-text>

    </v-card>
    <v-btn v-if="this.model.organizations.length < 5" block @click="newFormOrganization()" round color="info">Tambah</v-btn>
  </div>
</template>

<script>
export default {
  data () {
    return {
      model: {
        organizations: []
      },
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
      yearItems: [
        2019,
        2018,
        2017,
        2016,
        2015,
        2014,
        2013
      ]      
    }
  },
  methods: {
    newFormOrganization () {
      if (this.model.organizations.length < 5) {
        this.model.organizations.push({
          name: '',
          period: '',
          level: '',
          position: ''
        })
      }
    },
    removeFormOrganization (index) {
      this.model.organizations.splice(index, 1)
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
