<template>
  <layout-cash>
    <template #header>
      <header-cash> </header-cash>
    </template>
    <template #resume>
      <Resume
        :label="label"
        :total-label="'Monto Total'"
        :total-amount="totalAmount"
        :amount="amount"
      >
        <template #graphic>
          <graphic-cash :amounts="amounts" @select="select" />
        </template>
        <template #action>
          <action-cash @create="create" />
        </template>
      </Resume>
    </template>
    <template #movements>
      <movements-cash :movements="movements" @remove="remove" />
    </template>
  </layout-cash>
</template>

<script>
import HeaderCash from "./HeaderCash.vue";
import LayoutCash from "./LayoutCash.vue";
import Resume from "./Resume/IndexCash.vue";
import GraphicCash from "./Resume/GraphicCash.vue";
import ActionCash from "./ActionCash.vue";
import MovementsCash from "./movements/IndexCash.vue";
export default {
  components: {
    LayoutCash,
    HeaderCash,
    Resume,
    ActionCash,
    MovementsCash,
    GraphicCash,
  },
  data() {
    return {
      label: null,
      amount: null,
      movements: [],
    };
  },
  computed: {
    amounts() {
      const lastDays = this.movements
        .filter((m) => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);
          return m.time > oldDate;
        })
        .map((m) => m.amount);

      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i + 1);

        return lastMovements.reduce((suma, movement) => {
          return suma + movement;
        }, 0);
      });
    },
    totalAmount() {
      return this.movements.reduce((suma, m) => {
        return suma + m.amount;
      }, 0);
    },
  },

  mounted() {
    const movements = JSON.parse(localStorage.getItem("movements"));
    console.log(movements);

    if (Array.isArray(movements)) {
      this.movements = movements?.map((m) => {
        return { ...m, time: new Date(m.time) };
      });
    }
  },

  methods: {
    create(movement) {
      this.movements.push(movement);
      this.save();
    },
    remove(id) {
      const index = this.movements.findIndex((m) => m.id === id);
      this.movements.splice(index, 1);
      this.save();
    },
    save() {
      localStorage.setItem("movements", JSON.stringify(this.movements));
    },
    select(el) {
      console.log(el);
      this.amount = el;
    },
  },
};
</script>
