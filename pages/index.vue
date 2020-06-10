<template>
  <div class="container">
    <div class="tariffs-container">
      <div v-for="(item, index) in tariffsSortByName" class="tariffs-card">
        <div class="tariffs-card__title">
          <h2>{{ item.name }}</h2>
        </div>
        <div class="tariffs-card__description">
          <p>стоимость:</p>
          <p class="align_end">{{ item.currency | currency }}</p>
          <p>срок действия:</p>
          <p class="align_end">{{ item.validity | dateTime }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const collator = new Intl.Collator()

const numberFormat = new Intl.NumberFormat('kk', {
  style: 'currency',
  currency: 'KZT',
  minimumFractionDigits: 2
})

const dateTimeFormat = new Intl.DateTimeFormat('ru', {
  weekday: 'short',
  year: 'numeric',
  month: 'long',
  day: 'numeric'
})

export default {
  data: () => ({
    tariffs: [
      {
        name: 'Социальный',
        validity: new Date('2025-1-1'),
        currency: 1190
      },
      {
        name: 'Анлим FHD',
        validity: new Date('2020-3-20'),
        currency: 5090
      },
      {
        name: 'Больше за 7490',
        validity: new Date('2020-5-15'),
        currency: 7490
      },
      {
        name: 'Всё за 3990 Архивный',
        validity: new Date('2021-8-20'),
        currency: 3990
      }
    ]
  }),
  computed: {
    tariffsSortByName() {
      return this.tariffs.sort((a, b) => collator.compare(a.name, b.name))
    }
  },
  filters: {
    dateTime(date) {
      return dateTimeFormat.format(date)
    },
    currency(currency) {
      return numberFormat.format(currency)
    }
  }
}
</script>

<style lang="scss">
.tariffs-container {
  width: 100%;
  max-width: 1200px;
  margin: auto;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  .tariffs-card {
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12);
    &__title {
      padding: 0.5rem;
      border-top-left-radius: 8px;
      border-top-right-radius: 8px;
      border-bottom: 1px solid rgba(0, 0, 0, 0.125);
      background: linear-gradient(292.8deg, #ffd400 0.69%, #fcf27e 135.57%);
    }
    &__description {
      padding: 0.5rem;
      display: grid;
      grid-template-columns: auto auto;
      gap: 1rem;
      justify-content: space-between;
    }
  }
}

.align_end {
  justify-self: end;
}
</style>
