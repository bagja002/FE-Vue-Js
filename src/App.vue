<template>
  <div>
    <button type="button" class="btn btn-primary float-end" data-bs-toggle="modal" data-bs-target="#exampleModal">
      Tambah Permintaan
    </button>

    <!-- Modal -->
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Tambah Permintaan</h5>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <!-- Konten modal di sini -->
            <form @submit.prevent="tambahPermintaan">
              <label for="id_barang" class="form-label">ID Barang:</label>
              <input type="text" class="form-control" v-model="newPermintaan.id_barang" required />

              <!-- Tambahkan input untuk properti lainnya sesuai kebutuhan -->

              <button type="submit" class="btn btn-primary">Simpan</button>
              <button type="button" class="btn btn-danger" data-bs-dismiss="modal">Batal</button>

              <!-- Pesan sukses -->
              <div v-if="showSuccess" class="alert alert-success mt-3" role="alert">
                Permintaan berhasil disimpan!
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>

    <TableComponent :data="tableData" />
  </div>
</template>

<script>
import { ref, watchEffect } from 'vue';
import axios from 'axios';
import TableComponent from './components/TableComponent.vue';
import bootstrap from 'bootstrap/dist/js/bootstrap.js';

export default {
  name: 'App',
  components: {
    TableComponent,
  },
  data() {
    return {
      nama: "Bagja Lazwardi",
      total: 0,
      showSuccess: false,
      newPermintaan: {
        id_barang: '',
        // Add other properties as needed
      },
      // Use ref to define daftarBarang as a reactive reference
      daftarBarang: ref([]),
    };
  },
  methods: {
    async tambahPermintaan() {
      console.log('Tambahkan permintaan:', this.newPermintaan);

      try {
        // Send a POST request to your API endpoint using Axios
        await axios.post('your-api-endpoint', this.newPermintaan);

        // Reset properties
        this.newPermintaan = {
          id_barang: '',
          // Reset other properties as needed
        };

        // Show success message
        this.showSuccess = true;

        // Close success message after 3 seconds (adjust as needed)
        setTimeout(() => {
          this.showSuccess = false;
        }, 3000);

        // Close the Bootstrap modal
        const modalElement = document.getElementById('exampleModal');
        const modal = new bootstrap.Modal(modalElement);
        modal.hide();
      } catch (error) {
        console.error('Error adding request:', error);
      }
    },
  },
  setup() {
    
    // Use watchEffect to fetch data when the component is created
    watchEffect(() => {
      const fetchData = async () => {
        try {
          const response = await axios.get('http://127.0.0.1:8000/api/barang');
          // Update reactive data
          // Use .value to access the value of a ref
          // Note: context is the first parameter in setup
          this.daftarBarang.value = response.data;
        } catch (error) {
          console.error('Error fetching data:', error);
        }
      };

      fetchData();
    });
  },
};
</script>



<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
