<template>
  <v-app>
    <AppHeader/>
    <div>
      <center>
    <span style="color: rgb(255, 82, 82);" v-if="input_error_flg">Error in json input</span>
  </center>
  </div>
        <v-container fluid>
            <v-row>
              <v-col>
                <InputField 
                :error="input_error_flg"
                ref="inputfield"
                @getdata="getInputField"/>
              </v-col>
              
              <v-col
              cols="auto"
              >
              <v-btn
              color="primary"
              @click="jsonToYaml"
              elevation="3"
              block
              >
              Yaml
              </v-btn>
              <br>
              <v-btn
              color="primary"
              @click="jsonToXml"
              elevation="3"
              block
              >
              XML
              </v-btn>
              <br>
              <v-btn
              color="primary"
              @click="jsonToCsv"
              elevation="3"
              block
              >
              CSV
              </v-btn>
              <br>
              <v-btn
              color="primary"
              @click="jsonToXml"
              elevation="3"
              block
              >
              Visualuze
              </v-btn>
              <br>
              <v-btn
              color="primary"
              @click="jsonToXml"
              elevation="3"
              block
              >
              XML
              </v-btn>
            </v-col>

              <v-col>
                <OutputField
                :feed="jsonfeed"
                :format="select_fromat"
                />
              </v-col>
            </v-row>
        </v-container>
        
  </v-app>
</template>

<script>
import InputField from '@/components/InputField.vue';
import OutputField from '@/components/OutputField.vue';
import AppHeader from '@/components/AppHeader.vue'
import jsyaml from 'js-yaml';
import jsxml from 'xml-js';

  export default {
    name: 'HomeView',
    data(){
      return {
        jsondata : null,
        jsonfeed : null,
        select_fromat : null,
        input_error_flg : null,
      }
    },
    components:{
      InputField,
      OutputField,
      AppHeader
    },
    methods:{
      getInputField(data){
        this.jsondata = data
      },
      jsonToXml(){
        this.input_error_flg = false
      try{
        this.select_fromat = 'XMl'
      const xmlOutput = jsxml.js2xml(JSON.parse(this.jsondata),
      { compact: true, ignoreComment: true, spaces: 4 });
      this.jsonfeed = xmlOutput
      }catch{
        this.input_error_flg = true
      }
      },
      jsonToYaml() { 
        this.input_error_flg = false
      try {
        this.select_fromat = 'Yaml'
        const yamlString = jsyaml.dump(JSON.parse(this.jsondata));
        this.jsonfeed = yamlString;

      } catch (error) {
        this.input_error_flg = true
      }
    },
    jsonToCsv(){
      this.input_error_flg = false
      try{
          this.select_fromat = 'CSV'
          const jsonData =  eval(this.jsondata)
          const header = Object.keys(jsonData[0]).join(',') + '\n';
          const rows = jsonData.map(obj => Object.values(obj).join(',') + '\n').join('');
          this.jsonfeed =  header + rows
      }catch{
        this.input_error_flg = true
      }
    }
    }
  }
</script>
