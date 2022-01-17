<template>
<div class="container">
<div class="row">
<div class="col">
  <div class="card text-center card-form" @keypress.enter="addProduct">
  <div class="card-body">
    <h5 class="card-title">Товар</h5>
              <div class="mb-3">
            <label for="name" class="form-label">Название</label>
            <input type="text" class="form-control" id="name" :class="{'is-invalid': !name}" v-model="name">
                <div class="invalid-feedback">Заполните название</div>
            </div>
              <div class="mb-3">
            <label for="date" class="form-label">Дата приема товара</label>
            <input type="date" class="form-control" id="date" :class="{'is-invalid': !date}" v-model="date">
            <div class="invalid-feedback">Заполните дату приема товара</div>
            </div>
              <div class="mb-3">
            <label for="count" class="form-label">Количество</label>
            <input type="number" class="form-control" id="count" :class="{'is-invalid': !count}" v-model="count">
            <div class="invalid-feedback">Заполните количество</div>
            </div>
              <div class="mb-3">
            <label for="price" class="form-label">Цена</label>
            <input type="text" class="form-control" id="price" :class="{'is-invalid': !price}" v-model="price">
            <div class="invalid-feedback">Введите цену</div>
            </div>
    <button class="btn btn-primary" @click="addProduct">Добавить</button>
  </div>
</div>
</div>
<div class="row">
  <div class="col">
    <table class="table table-hover table-product">
<thead>
  <tr>
    <th>#</th>
    <th>Название</th>
    <th>Дата приема товара</th>
    <th>Количество</th>
    <th>Цена</th>
    <th>Удаление</th>
  </tr>
</thead>
<tbody>
  <tr v-for="(product, index) in products" :key="product.id">
    <td>{{ index + 1 }}</td>
    <td>{{ product.name }}</td>
    <td>{{ product.date }}</td>
    <td>{{ product.count }}</td>
    <td>{{ product.price }}</td>
    <td><button type="button" class="btn btn-danger" @click="deleteProduct(product.id)">Удалить</button></td>
  </tr>
</tbody>
<tfoot>
  <tr>
    <td colspan="6" class="text-right text-bold">{{ totalPrice }}</td>
  </tr>
</tfoot>
</table>
  </div>
</div>
</div>

</div>
</template>

<script>
export default {
  name: 'accounting',
  data () {
    return {
        products: [
          {id:1, name: 'Ручка шариковая', date: '29.12.2021', price: 500, count: 5},
          {id:2, name: 'Карандаш', date: '30.12.2021', price: 700, count: 10},
          {id:3, name: 'Бумага', date: '31.12.2021', price: 800, count: 50},
        ],
        name: '',
        date: '',
        count: 1,
        price: '',
    }
  },
  computed: {
    totalPrice() {
      let total = 0;
for (const product of this.products) {
  total += product.price * product.count;
}

      return total;
    }
  },
  methods: {
    addProduct() {
if (this.name && this.date && this.price && this.count) {
  this.products.push({
    id: Date.now(),
    name: this.name,
    date: this.date,
    price: this.price,
    count: this.count

  });
} else {
  alert('Заполните все поля!')
      }
    },
deleteProduct(id) {
this.products = this.products.filter(product => product.id != id)
}
}
}
</script>
