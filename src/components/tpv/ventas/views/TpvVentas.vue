<template>
  <h3>Hola</h3>

  <q-form @submit="createSale" ref="form" v-if="showForm">
    <q-input
      v-model="sale.name"
      label="Nombre del producto"
      :rules="nameRules"
      type="text"
      required
    />
    <q-input
      v-model="sale.quantity"
      label="Cantidad"
      :rules="quantityRules"
      type="number"
      required
    />
    <q-input
      v-model="sale.price"
      label="Precio"
      :rules="priceRules"
      type="number"
      required
    />
    <q-btn color="primary" type="submit" label="Crear venta" />
  </q-form>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'TpvVentas',
  props: {
    title: {
      type: String,
      required: true,
    },

    caption: {
      type: String,
      default: '',
    },

    link: {
      type: String,
      default: '#',
    },

    icon: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      showForm: true,
      sale: {
        name: '',
        quantity: 0,
        price: 0,
      },
      nameRules: [
        (v) => !!v || 'Nombre del producto es requerido',
        (v) =>
          (v && v.length <= 20) ||
          'Nombre del producto debe tener 20 caracteres o menos',
      ],
      quantityRules: [
        (v) => !!v || 'Cantidad es requerida',
        (v) => (v && v > 0) || 'La cantidad debe ser mayor a 0',
      ],
      priceRules: [
        (v) => !!v || 'Precio es requerido',
        (v) => (v && v > 0) || 'El precio debe ser mayor a 0',
      ],
    };
  },
  methods: {
    createSale() {
      this.$refs.form.validate().then((valid) => {
        if (valid) {
          // Enviar sale a la API o base de datos
          this.sale = {
            name: '',
            quantity: 0,
            price: 0,
          };
        }
      });
    },
  },
});
</script>
