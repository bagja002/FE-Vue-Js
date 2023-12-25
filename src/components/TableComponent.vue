<template>
    <div>
      <table>
        <thead>
          <tr>
            <th>ID Permintaan</th>
            <th>ID User</th>
            <th>Nama User</th>
            <th>Departemen</th>
            <th>Lokasi</th>
            <th>Nama Barang</th>
            <th>Kuantitas</th>
            <th>Keterangan</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in data" :key="item.id_permintaan">
            <td>{{ item.id_permintaan }}</td>
            <td>{{ item.id_user }}</td>
            <td>{{ item.nama_user }}</td>
            <td>{{ item.departement }}</td>
            <td>{{ item.lokasi }}</td>
            <td>{{ item.nama_barang }}</td>
            <td>{{ item.kuantitas }}</td>
            <td>{{ item.keterangan }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      data: Array // Properti untuk menerima data dari induk komponen
    }
  };
  </script>
  
  <style scoped>
  /* Gaya CSS khusus untuk komponen ini */
  table {
    width: 100%;
    border-collapse: collapse;
    margin-top: 10px;
  }
  
  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }
  
  th {
    background-color: #f2f2f2;
  }
  </style>
  