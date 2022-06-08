<template>
  <layout-cash>
    <template #header>
      <header-cash> </header-cash>
    </template>
    <template #resume>
      <Resume :label="'Monto Total'" :totalAmount="90000" :amount="amount">
        <template #graphic> graphic </template>
        <template #action>
          <action-cash />
        </template>
      </Resume>
    </template>
    <template #movements>
      <movements-cash :movements="movements" />
    </template>
  </layout-cash>
</template>

<script>
import HeaderCash from "./HeaderCash.vue";
import LayoutCash from "./LayoutCash.vue";
import Resume from "./Resume/IndexCash.vue";
import ActionCash from "./ActionCash.vue";
import MovementsCash from "./movements/IndexCash.vue";
export default {
  components: {
    LayoutCash,
    HeaderCash,
    Resume,
    ActionCash,
    MovementsCash,
  },
  data() {
    return {
      amount: null,
      movements: [
        {
          id: 0,
          title: "Movimiento",
          description: "Miguel Angel Castillo Colmenares",
          amount: 1000,
        },
        {
          id: 1,
          title: "Movimiento 1",
          description: "Miguel Angel Castillo Colmenares",
          amount: -1000,
        },
        {
          id: 2,
          title: "Movimiento 2",
          description: "Miguel Angel Castillo Colmenares",
          amount: -1000,
        },
        {
          id: 3,
          title: "Movimiento 3",
          description: "Miguel Angel Castillo Colmenares",
          amount: 1000,
        },
        {
          id: 4,
          title: "Movimiento 4",
          description: "Miguel Angel Castillo Colmenares",
          amount: -1000,
        },
        {
          id: 5,
          title: "Movimiento 5",
          description: "Miguel Angel Castillo Colmenares",
          amount: 1000,
        },
        {
          id: 6,
          title: "Movimiento 6",
          description: "Miguel Angel Castillo Colmenares",
          amount: 1000,
        },
      ],
    };
  },
};
</script>
