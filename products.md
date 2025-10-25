---
layout: defaults
title: Products
---

<div class="home">
  <h1 class="page-heading">{{ page.title }}</h1>

  <!-- search bar -->
  <input type="text" id="search" placeholder="Search by name or instrument" class="search-input">

  <!-- filters -->
  <div class="filters">
    <select id="filter-hemisphere" class="filter-select">
      <option value="">All hemispheres</option>
      {% assign hemispheres = site.data.products | map: "Hemisphere" | uniq %}
      {% for hemisphere in hemispheres %}
        <option value="{{ hemisphere }}">{{ hemisphere }}</option>
      {% endfor %}
    </select>

    <select id="filter-variable" class="filter-select">
      <option value="">All variables</option>
      {% assign variables = site.data.products | map: "Variable" | uniq %}
      {% for variable in variables %}
        <option value="{{ variable }}">{{ variable }}</option>
      {% endfor %}
    </select>
  </div>

  <!-- Table -->
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
const filterHemisphere = document.querySelector('#filter-hemisphere');
const filterVariable = document.querySelector('#filter-variable');

function applyFilters() {
  const query = searchInput.value.toLowerCase();
  const selectedHemisphere = filterHemisphere.value.toLowerCase();
  const selectedVariable = filterVariable.value.toLowerCase();

  Array.from(tableBody.rows).forEach(row => {
    const name = row.cells[0].textContent.toLowerCase();
    const instrument = row.cells[1].textContent.toLowerCase();
    const hemisphere = row.cells[2].textContent.toLowerCase();
    const variable = row.cells[3].textContent.toLowerCase();

    const matchesSearch =
      name.includes(query) || instrument.includes(query);

    const matchesHemisphere =
      !selectedHemisphere || hemisphere === selectedHemisphere;

    const matchesVariable =
      !selectedVariable || variable === selectedVariable;

    row.style.display = matchesSearch && matchesHemisphere && matchesVariable ? '' : 'none';
  });
}

searchInput.addEventListener('input', applyFilters);
filterHemisphere.addEventListener('change', applyFilters);
filterVariable.addEventListener('change', applyFilters);
</script>

<style>
.home {
  max-width: 900px;
  margin: auto;
}
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
  margin-bottom: 15px;
  padding: 8px;
  width: 100%;
  max-width: 400px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.filters {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}
.filter-select {
  flex: 1;
  max-width: 200px;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}
</style>
