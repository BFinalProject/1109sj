<template>
  <div>
    <h2>씹년아</h2>
    <button @click="fetchContacts()">검색</button>
    <button @click="auth">검색2</button>
    <button @click="getMembers">검색3</button>
    <input id="csrfToken" type="hidden" name="${_csrf.subject}" value="${_csrf.content}">
  </div>

</template>

<script>
import Axios from 'axios'
// axios.defaults.xsrfCookieName = 'csrftoken';
// axios.defaults.xsrfHeaderName = 'X-CSRFTOKEN';
// axios.defaults.baseURL = 'http://localgost:8080';
// axios.defaults.headers.post['Content-Type'] = 'application/json;charset=utf-8';
// axios.defaults.headers.post['Access-Control-Allow-Origin']='*';

export default {
  name: 'test',
  data() {
    return {
      listdata : {},
    }
  },
  mounted: function() {
    let vm = this;
    vm.fetchContacts();
  },
  methods: {

      //1
      fetchContacts: function(){
            let vm = this;
            
            let sendData={}

            Axios.get("/question/api/list3", sendData).
            then(function(response) {
                console.log(response.data);              
                vm.listdata = response.data.content;
            }).catch(function(ex) {
                console.log(ex);
            });
        },
        // 틀린코드
      // fetchContacts: function(){
      //       let vm = this;
            
      //       let sendData={}

      //       Axios.post("/api/list3", sendData).
      //       then(function(response) {
      //           console.log(response);              
      //           vm.listdata = response.data;
      //       }).catch(function(ex) {
      //           console.log(ex);
      //       });
      //   },

    //   fnGetStat1List: function() {
    //   let vm = this;
    //   let sendData = {
    //     yyyymm:vm.nowMonth
    //   };
    //   this.$sendAxios("/question/api/list3", sendData, 
    //     function(resp){
    //         vm.listdata = resp.data;
    //     });
    // },
      // 3
    getMembers() {
      Axios({
        url: "/api/list3",
        method: "post"
      })
        .then(res => {
          console.log(res);
        })
        .catch(err => {
          console.log(err);
        })
    },
      //2
    auth: function () {
      const request = Axios.post('api/list3')
        .then(response => response.data);
      return {
        type: paging,
        payload: request
      }
    }
  }
};
</script>
