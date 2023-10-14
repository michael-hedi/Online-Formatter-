<template>
     <v-container>
      <v-row>
        <v-col>
          <v-toolbar
          height="40"
          color="#dc5a43"
        class ="rounded-lg rounded-b-0"
  elevation="2"
>
<v-spacer></v-spacer>
<v-btn small class="ma-2" icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
      <v-btn small class="ma-2" icon>
        <v-icon>mdi-content-copy</v-icon>
      </v-btn>
      <v-btn small class="ma-2" icon>
        <v-icon>mdi-reload</v-icon>
      </v-btn>
      <v-btn small class="ma-2" icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
</v-toolbar>
</v-col>
      </v-row>
        <v-row no-gutters>
        <v-col>
        <v-textarea
          :label="format"
          filled
          rows="28"
          row-height="1"
          :value="feed"
          no-resize
          class="code-textarea"
        ></v-textarea>
      </v-col>
   
</v-row>
    </v-container>
</template>
<script>

export default{
    name : "OutputField",
    props:['feed', 'format']

}
</script>
<style scoped>
.code-textarea {
  font-family: 'Courier New', monospace;
}
</style>