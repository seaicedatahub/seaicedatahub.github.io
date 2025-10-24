---
layout: default
title: Products
---

<div class="home">
  <h1 class="page-heading">{{ page.title }}</h1>

  <!-- Barre de recherche stylée -->
  <input type="text" id="search" placeholder="Search by name or category" class="search-input">

  <!-- Tableau rempli par Liquid/Minima -->
  <table id="products-table" class="products-table">
    <thead>
      <tr>
        <th>Name</th>
        <th>Instrument</th>
        <th>Hemisphere</th>
        <th>Variable</th>
      </tr>
    </thead>
    <tbody>
      {% for product in site.data.products %}
      <tr>
        <td>{{ product.Name }}</td>
        <td>{{ product.Instrument }}</td>
        <td>{{ product.Hemisphere }}</td>
        <td>{{ product.Variable }}</td>
      </tr>
      {% endfor %}
    </tbody>
  </table>
</div>

<script>
const tableBody = document.querySelector('#products-table tbody');
const searchInput = document.querySelector('#search');

searchInput.addEventListener('input', () => {
  const query = searchInput.value.toLowerCase();
  Array.from(tableBody.rows).forEach(row => {
    const name = row.cells[0].textContent.toLowerCase();
    const category = row.cells[1].textContent.toLowerCase();
    row.style.display = (name.includes(query) || category.includes(query)) ? '' : 'none';
  });
});
</script>

<style>
.products-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}
.products-table th, .products-table td {
  border: 1px solid #ddd;
  padding: 10px;
}
.products-table th {
  background-color: #f7f7f7;
  text-align: left;
}
.products-table tr:nth-child(even) {
  background-color: #f2f2f2;
}
.products-table tr:hover {
  background-color: #e0f7fa;
}
.search-input {
  margin-bottom: 20px;
  padding: 8px;
  width: 100%;
  max-width: 400px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
</style>
