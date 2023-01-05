<template>
    <v-card
class="mx-auto"
max-width="434"
tile
>
<v-img
height="100%"
src="https://th.bing.com/th/id/R.ad2ad4ae567c2f1ae5cd1625ab0d5764?rik=4lnrIPYFnZezJQ&pid=ImgRaw&r=0"
>
<v-row
  align="end"
  class="fill-height"
>
  <v-col
    align-self="start"
    class="pa-0"
    cols="12"
  >
    <v-avatar
      class="profile"
      color="grey"
      size="164"
      tile
    >
      <v-img src="https://th.bing.com/th/id/R.981d20408e22ffa06d01bee08527111c?rik=wPj5n6BgXH9ztg&pid=ImgRaw&r=0"></v-img>
    </v-avatar>
  </v-col>
  <v-col class="py-0">
    <v-list-item
      color="rgba(0, 0, 0, .4)"
      dark
    >
      <v-list-item-content>
        <v-list-item-title class="text-h6">
          Juan Carlos
        </v-list-item-title>
        <v-list-item-subtitle>Ingeniero en sistemas</v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>
  </v-col>
</v-row>
</v-img>
</v-card>
</template>

<script>
export default {
name: 'TheProfileCard'
}
</script>