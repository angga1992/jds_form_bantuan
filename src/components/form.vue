<template>
  <div>
    <div class="phone">
      <img style="height: 60px; margin: 10px" src="https://digitalservice.jabarprov.go.id/wp-content/uploads/2019/11/logo_jds.png" alt="">
      <div>
        <label for="name">Nama:</label>
        <input id="name" type="text" v-model="dataPendukduk.nama" required />
        <span class="error-message">Required</span>
      </div>
      <div>
        <label for="nik">Nik:</label>
        <input id="nik" type="number" v-model="dataPendukduk.nik" required />
        <span class="error-message">Required</span>
      </div>
      <div>
        <label for="kk">No. Kartu Keluarga:</label>
        <input id="kk" type="number" v-model="dataPendukduk.kk" required />
        <span class="error-message">Required</span>
      </div>
      <div>
        <label for="fktp">Foto KTP:</label>
        <input id="fktp" type="file" :rules="rules" @change="onFileChangeKtp" required accept="image/png, image/jpeg, image/jpg, image/bmp"/>
        <span class="error-message">Required</span>
      </div>
      <div>
        <label for="fkk">Foto Kartu Keluarga:</label>
        <input id="fkk" type="file" :rules="rules" required @change="onFileChangeKk" accept="image/png, image/jpeg, image/jpg, image/bmp"/>
        <span class="error-message">Required</span>
      </div>
      <div>
        <label for="usia">Umur</label>
        <input id="usia" type="number" v-model="dataPendukduk.usia" required />
        <span class="error-message">Required</span>
      </div>
      <div>
        <label for="kelamin">Jenis Kelamin</label>
        <select v-model="dataPendukduk.kelamin" name="kelamin">
          <option value="L">Laki-laki</option>
          <option value="W">Perempuan</option>
        </select>
      </div>
      <div>
        <label for="alamat">Alamat</label>
        <input
          id="alamat"
          type="textarea"
          maxlength="255"
          v-model="dataPendukduk.alamat"
          required
        />
        <span class="error-message">Required</span>
      </div>
      <div>
        <label for="rt">Rt</label>
        <input id="rt" type="text" v-model="dataPendukduk.rt" required />
        <span class="error-message">Required</span>
      </div>
      <div>
        <label for="rw">Rw</label>
        <input id="rw" type="text" v-model="dataPendukduk.rw" required />
        <span class="error-message">Required</span>
      </div>
      <div>
        <label for="bpandemic">Penghasilan sebelum pandemik</label>
        <input
          id="bpandemic"
          type="number"
          v-model="dataPendukduk.bpandemic"
          required
        />
        <span class="error-message">Required</span>
      </div>
      <div>
        <label for="apandemic">Penghasilan sesudah pandemik</label>
        <input
          id="apandemic"
          type="number"
          v-model="dataPendukduk.apandemic"
          required
        />
        <span class="error-message">Required</span>
      </div>
      <div>
        <label for="reason">Alasan membutuhkan bantuan</label>
        <select v-model="dataPendukduk.reason" name="reason">
          <option value="1">Kehilangan pekerjaan</option>
          <option value="2">Kepala keluarga terdampak atau korban Covid</option>
          <option value="3">
            Tergolong fakir/miskin semenjak sebelum Covid
          </option>
          <option value="4">Lainya...</option>
        </select>
      </div>
      <div v-show="dataPendukduk.reason === '4'">
        <input v-model="temp" type="text" />
      </div>
      <div>
        <input v-model="checked" type="checkbox">
        <pre>{{checked}}</pre>
        <span>Saya menyatakan bahwa data yang diisikan adalah benar dan siap mempertanggungjawabkan apabila ditemukan ketidaksesuaian dalam data tersebut.</span>
      </div>
      <button :disabled="disableds()" @click="submitData()">
        <span>Submit</span>
      </button>
    </div>
    <div class="webs">
        <img src="https://digitalservice.jabarprov.go.id/wp-content/uploads/2019/11/logo_jds.png" alt="">
        <h1>Silakan akses via smartphone anda :)</h1>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      errors: false,
      otherReasons: false,
      temp: '',
      checked: false,
      rules: [
        files => !files || !files.some(file => file.size > 2_097_152) || 'image size should be less than 2 MB!'
      ],
      dataPendukduk: {
        nama: "",
        nik: "",
        kk: "",
        fktp: "",
        fkk: "",
        usia: "",
        kelamin: "",
        alamat: "",
        rt: "",
        rw: "",
        bpandemic: "",
        apandemic: "",
        reason: "",
      },
    };
  },
  methods: {
    invalidateForm() {
      this.errors = true;
    },
    submitData() {
      if (this.temp !== '') {
        this.dataPendukduk.reason = this.temp
      }
      setTimeout(() => {
        let sukses = Math.ceil(Math.random() * 2)
        if (sukses === 1) {
          console.log("success", this.dataPendukduk);
        } else {
          console.log("gagal", this.dataPendukduk);
        }
      }, 1500);
    },
    onFileChangeKtp (e) {
        this.dataPendukduk.fktp = e.target.files[0];
    },
    onFileChangeKk (e) {
        this.dataPendukduk.fkk = e.target.files[0];
    },
    disableds() {
      if (this.checked === true && this.dataPendukduk.nama !== '' && this.dataPendukduk.nik !== '' && this.dataPendukduk.kk !== '' && this.dataPendukduk.fktp !== '' && this.dataPendukduk.fkk !== '' && this.dataPendukduk.usia !== '' && this.dataPendukduk.kelamin !== '' && this.dataPendukduk.alamat !== '' && this.dataPendukduk.rt !== '' && this.dataPendukduk.rw !== '' && this.dataPendukduk.bpandemic !== '' && this.dataPendukduk.apandemic !== '' && this.dataPendukduk.reason !== '') {
        return false
      } else {
        return true
      }
    }
  },
};
</script>

<style lang="scss">
button {
  background-color: #008CBA;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
.phone {
  display: none;
}
.webs {
  display: block;
}
@media only screen and (max-width: 600px) {
  body {
    background-color: lightblue;
  }
  .phone {
    display: block;
    padding: 10%;
  }
  label {
    text-align: left;
  }
  .webs {
    display: none;
  }
  label {
    display: block;
  }
  div + div {
    margin-top: 1em;
  }
  .error-message {
    display: none;
    color: red;
  }
  input {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
    border: 3px solid #ccc;
    -webkit-transition: 0.5s;
    transition: 0.5s;
    outline: none;
  }

  input:focus {
    border: 3px solid #555;
  }
  select {
    width: 100%;
    padding: 12px 20px;
    margin: 8px 0;
    box-sizing: border-box;
    border: 3px solid #ccc;
    -webkit-transition: 0.5s;
    transition: 0.5s;
    outline: none;
  }
  form.errors {
    :invalid {
      border-color: red;
    }
    .error-message {
      display: block;
    }
  }
}
</style>