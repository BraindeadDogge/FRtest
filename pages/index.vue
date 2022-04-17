<template>
  <div>
  <v-breadcrumbs :items="breaditems">
    <template v-slot:divider>
      <v-icon>mdi-forward</v-icon>
    </template>
  </v-breadcrumbs>
  </div>
</template>

<script>
export default {
  name: 'Polls',
  data: () => ({
      breaditems: [
        {
          text: 'Home',
          disabled: true,
          href: '/',
        },
      ],
    }),
}
</script>
