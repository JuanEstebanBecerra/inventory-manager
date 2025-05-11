<template>
  <div class="flex flex-col gap-4 h-full">
    <div class="flex justify-between items-center">
      <span>Productos</span>
      <UButton
        label="Añadir producto"
        @click="addProduct" />
    </div>

    <div class="flex-1 w-full">
      <table class="w-full">
        <thead>
          <tr class="*:px-4 *:py-2 *:bg-gray-50">
            <th class="rounded-s-lg">Producto</th>
            <th>Cantidad</th>
            <th class="rounded-e-lg">Acciones</th>
          </tr>
        </thead>

        <tbody>
          <tr
            v-for="(item, index) in selectedProducts"
            class="*:py-2 *:px-3">
            <td>
              <USelectMenu
                placeholder="Seleccione"
                class="w-full"
                variant="ghost"
                :items="products"
                @update:modelValue="
                  (e) => {
                    item.product = { name: e.label, price: e.price };
                  }
                " />
            </td>
            <td class="text-center">
              <UInput v-model="item.amount" />
            </td>
            <td class="text-center">
              <UButton
                icon="i-material-symbols-close-rounded"
                color="error"
                variant="ghost"
                @click="selectedProducts.splice(index, 1)" />
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="flex justify-end items-center gap-4 mt-4">
      <UButton
        size="lg"
        color="neutral"
        label="Cancelar"
        variant="outline"
        @click="emit('close')" />
      <UButton
        size="lg"
        label="Guardar"
        @click="emit('close')" />
    </div>
  </div>
</template>

<script setup lang="ts">
type Emits = (e: 'close') => void;

const emit = defineEmits<Emits>();

type SelectedProduct = {
  product: { name: string; price: number };
  amount: number;
};

const selectedProducts = ref<SelectedProduct[]>([]);

const addProduct = () => {
  selectedProducts.value.push({
    product: {
      name: '',
      price: 0,
    },
    amount: 0,
  });
};

const products = [
  { id: 1, label: 'Arroz', provider: 'Bebidas del Valle', code: '751462', active: true, amount: 409, price: 3295 },
  { id: 2, label: 'Frijoles', provider: 'Bebidas del Valle', code: '737810', active: false, amount: 166, price: 2842 },
  { id: 3, label: 'Azúcar', provider: 'Aseo Hogar', code: '767997', active: false, amount: 22, price: 13438 },
  { id: 4, label: 'Aceite', provider: 'Comestibles Andinos', code: '139661', active: true, amount: 111, price: 8709 },
  { id: 5, label: 'Sal', provider: 'Alimentos del Sur', code: '960861', active: true, amount: 309, price: 10241 },
  {
    id: 6,
    label: 'Harina de Trigo',
    provider: 'Panadería San Juan',
    code: '946558',
    active: false,
    amount: 272,
    price: 7914,
  },
  { id: 7, label: 'Café', provider: 'Higiene Total', code: '902119', active: true, amount: 76, price: 1351 },
  {
    id: 8,
    label: 'Leche en Polvo',
    provider: 'Distribuciones Gourmet',
    code: '376770',
    active: false,
    amount: 107,
    price: 1455,
  },
  {
    id: 9,
    label: 'Pasta',
    provider: 'Distribuciones Gourmet',
    code: '105192',
    active: false,
    amount: 330,
    price: 14593,
  },
  { id: 10, label: 'Lentejas', provider: 'Granos del Norte', code: '897539', active: false, amount: 169, price: 10718 },
  { id: 11, label: 'Galletas', provider: 'Granos del Norte', code: '888957', active: true, amount: 93, price: 7929 },
  { id: 12, label: 'Atún', provider: 'Lácteos Nacionales', code: '846042', active: false, amount: 264, price: 6322 },
  {
    id: 13,
    label: 'Sardinas',
    provider: 'Lácteos Nacionales',
    code: '898527',
    active: true,
    amount: 289,
    price: 10518,
  },
  { id: 14, label: 'Maíz', provider: 'Productos del Campo', code: '121726', active: false, amount: 134, price: 7433 },
  { id: 15, label: 'Avena', provider: 'Productos del Campo', code: '345982', active: true, amount: 142, price: 11781 },
  {
    id: 16,
    label: 'Chocolate',
    provider: 'Distribuciones Gourmet',
    code: '324740',
    active: false,
    amount: 63,
    price: 14466,
  },
  { id: 17, label: 'Jabón', provider: 'Aseo Hogar', code: '641871', active: true, amount: 160, price: 9546 },
  {
    id: 18,
    label: 'Detergente',
    provider: 'Comestibles Andinos',
    code: '384251',
    active: false,
    amount: 166,
    price: 11290,
  },
  { id: 19, label: 'Shampoo', provider: 'Alimentos del Sur', code: '264203', active: false, amount: 349, price: 13236 },
  {
    id: 20,
    label: 'Cepillo de dientes',
    provider: 'Higiene Total',
    code: '109087',
    active: true,
    amount: 166,
    price: 6011,
  },
  {
    id: 21,
    label: 'Papel higiénico',
    provider: 'Lácteos Nacionales',
    code: '973703',
    active: false,
    amount: 41,
    price: 6806,
  },
  { id: 22, label: 'Toallas', provider: 'Aseo Hogar', code: '144875', active: true, amount: 64, price: 12577 },
  { id: 23, label: 'Desodorante', provider: 'Higiene Total', code: '770899', active: true, amount: 448, price: 5373 },
  {
    id: 24,
    label: 'Agua embotellada',
    provider: 'Comestibles Andinos',
    code: '645045',
    active: false,
    amount: 497,
    price: 6430,
  },
  { id: 25, label: 'Jugo', provider: 'Distribuciones Gourmet', code: '240537', active: true, amount: 27, price: 7639 },
  { id: 26, label: 'Refresco', provider: 'Granos del Norte', code: '327787', active: true, amount: 265, price: 6790 },
  {
    id: 27,
    label: 'Cerveza',
    provider: 'Productos del Campo',
    code: '935191',
    active: false,
    amount: 22,
    price: 13215,
  },
  { id: 28, label: 'Vino', provider: 'Distribuciones Gourmet', code: '802099', active: true, amount: 304, price: 6043 },
  { id: 29, label: 'Ron', provider: 'Aseo Hogar', code: '300313', active: true, amount: 85, price: 9111 },
  { id: 30, label: 'Whisky', provider: 'Panadería San Juan', code: '347808', active: true, amount: 78, price: 10265 },
  { id: 31, label: 'Pollo', provider: 'Higiene Total', code: '858598', active: true, amount: 408, price: 13716 },
  {
    id: 32,
    label: 'Carne',
    provider: 'Distribuciones Gourmet',
    code: '471247',
    active: false,
    amount: 202,
    price: 7310,
  },
  {
    id: 33,
    label: 'Pescado',
    provider: 'Distribuciones Gourmet',
    code: '133229',
    active: true,
    amount: 302,
    price: 11911,
  },
  { id: 34, label: 'Huevos', provider: 'Comestibles Andinos', code: '163230', active: false, amount: 85, price: 7771 },
  {
    id: 35,
    label: 'Mantequilla',
    provider: 'Granos del Norte',
    code: '256969',
    active: false,
    amount: 209,
    price: 6255,
  },
  {
    id: 36,
    label: 'Queso',
    provider: 'Distribuciones Gourmet',
    code: '586207',
    active: false,
    amount: 275,
    price: 9474,
  },
  {
    id: 37,
    label: 'Yogur',
    provider: 'Distribuciones Gourmet',
    code: '718146',
    active: false,
    amount: 483,
    price: 13297,
  },
  { id: 38, label: 'Pan', provider: 'Alimentos del Sur', code: '973746', active: true, amount: 130, price: 1422 },
  {
    id: 39,
    label: 'Gaseosa',
    provider: 'Productos del Campo',
    code: '236781',
    active: true,
    amount: 381,
    price: 11895,
  },
  { id: 40, label: 'Helado', provider: 'Comestibles Andinos', code: '231120', active: true, amount: 462, price: 7404 },
  {
    id: 41,
    label: 'Cereal',
    provider: 'Distribuciones Gourmet',
    code: '582541',
    active: false,
    amount: 448,
    price: 11131,
  },
  {
    id: 42,
    label: 'Sopa instantánea',
    provider: 'Panadería San Juan',
    code: '247052',
    active: false,
    amount: 317,
    price: 12348,
  },
  { id: 43, label: 'Salsa de tomate', provider: 'Aseo Hogar', code: '887514', active: true, amount: 199, price: 7980 },
  {
    id: 44,
    label: 'Mayonesa',
    provider: 'Alimentos del Sur',
    code: '828758',
    active: false,
    amount: 341,
    price: 13583,
  },
  { id: 45, label: 'Mostaza', provider: 'Panadería San Juan', code: '728452', active: true, amount: 316, price: 5815 },
  { id: 46, label: 'Vinagre', provider: 'Granos del Norte', code: '443999', active: false, amount: 238, price: 5941 },
  {
    id: 47,
    label: 'Mermelada',
    provider: 'Panadería San Juan',
    code: '976456',
    active: true,
    amount: 292,
    price: 10041,
  },
  { id: 48, label: 'Miel', provider: 'Distribuciones Gourmet', code: '213912', active: true, amount: 267, price: 6959 },
  { id: 49, label: 'Té', provider: 'Productos del Campo', code: '511061', active: true, amount: 55, price: 5922 },
  { id: 50, label: 'Yerba Mate', provider: 'Aseo Hogar', code: '178375', active: false, amount: 354, price: 8756 },
];
</script>
