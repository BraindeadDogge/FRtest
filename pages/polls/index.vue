<template>
  <div>
  <v-breadcrumbs :items="breaditems">
    <template v-slot:divider>
      <v-icon>mdi-forward</v-icon>
    </template>
  </v-breadcrumbs>
  <v-btn to="/polls/add">
    Добавить опрос
  </v-btn>
  </div>
</template>

<script>
export default {
  name: 'Polls',
  data: () => ({
      breaditems: [
        {
          text: 'Home',
          disabled: false,
          href: '/',
        },
        {
          text: 'Опросы',
          disabled: true,
          href: '/polls',
        }
      ],
    }),
}
</script>
