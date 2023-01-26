<template>
  <div class="App__wrap">
    <div class="App__tabel">
      <div class="App__tabel-col" v-for="col in tabelLabel" :key="col.id" @drop="onDrop($event, col, index)"
        @dragover.prevent @dragenter.prevent>
        <div class="App__tabel-col_hed" draggable="true" @dragstart="startDrag($event, col)">
          <span v-if="typeof col.value[1] === 'boolean'">
            <input type="checkbox" />
          </span>
          <span v-else>
            {{ col.value[1] }}
          </span>
        </div>
        <div class="App__tabel-col_row" v-for="row in tabelRow" :key="row.id" draggable="true"
          @dragstart="startDrag($event, col)">
          <span v-if="col.value[0] === 'isChec'">
            <input type="checkbox" />
          </span>
          <span v-if="col.value[0] === 'ollRevenue'">
            {{ row.prise * row.count }}
          </span>
          <span v-else></span>
          {{ row[col.value[0]] }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>


export default {
  name: 'App',
  computed: {
  },
  data() {
    return {
      tabelLabel: [
        { id: 1, value: ['isChec', false] },
        { id: 2, value: ['name', 'Название'] },
        { id: 3, value: ['id', 'Артикул'] },
        { id: 4, value: ['prise', 'Цена в руб'] },
        { id: 5, value: ['count', 'Продажа, шт'] },
        { id: 6, value: ['ollRevenue', 'Выручка за период'] },
        { id: 7, value: ['revenue', 'Выручка руб'] },
        { id: 8, value: ['bacRevenue', 'Упущеная выручка'] },
        { id: 9, value: ['trader', 'Продавец'] }
      ],
      tabelRow: [
        { id: 123, name: 'Карты таро', prise: 21340.00, count: 105, trader: 'Таро ООО' },
        { id: 234, name: 'Спрей сыворотка', prise: 2755.00, count: 74, trader: 'ООО "Дальба"' },
        { id: 456, name: 'Свечи для торта', prise: 99000.00, count: 0, trader: 'Ангельев Руслан Степанович' },
        { id: 789, name: 'Лента светодиодная', prise: 19900.00, count: 0, trader: 'Пургин Деонисий Вечиславович' }
      ]
    }
  },
  methods: {
    startDrag(evt, item) {
      evt.dataTransfer.dropEffect = 'move';
      evt.dataTransfer.effectAllowed = 'move';
      evt.dataTransfer.setData('itemID', item.id);
    },

    onDrop(evt, list) {
      const itemID = evt.dataTransfer.getData('itemID');
      const item = this.tabelLabel.find((item) => item.id == itemID);
      const val = list.value;
      const index = this.tabelLabel.indexOf(item);
      list.value = item.value;
      this.tabelLabel[index].value = val;
    },
  }
}
</script>

<style lang="scss">
#app {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
}

.App_ {
  &_wrap {
    width: 100%;
    height: 100%;
    display: flex;
    margin-top: 30px;
    justify-content: center;
    align-items: start;
  }

  &_tabel {
    max-width: 90vw;
    min-width: 80%;
    display: flex;

    &-col {
      min-width: 10%;
      display: flex;
      flex-direction: column;

      &_hed {
        min-height: 30px;
        background-color: rgb(218, 218, 218);
        border: 2px solid black;
        cursor: grab;
        display: flex;
        justify-content: center;
        align-items: center;
      }

      &_row {
        min-height: 30px;
        border: 1px solid black;
        display: flex;
        justify-content: center;
        align-items: center;
      }
    }
  }
}
</style>
