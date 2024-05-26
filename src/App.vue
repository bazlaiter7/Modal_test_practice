<script >
  export default {
  data() {
    return {
      show_modal_flag: false,
      form_data: {
        export_name: 'my_vol2',
        volume_name: ['iscsi', 'bbc'],
        protocol: ['tcp', 'udp'],
      },
      selected_form_data: {
        export_name: "",
        volume_name: "",
        protocol: "",
      }
    };
  },
  methods: {
    toggle_modal_flag() {
      this.show_modal_flag = !this.show_modal_flag;
    },
    off_modal_flag(){
      this.show_modal_flag = false;
    },
    submit_form(e){
      e.preventDefault();
      this.off_modal_flag();
      this.selected_form_data.export_name = this.$refs.export_name.value;
      this.selected_form_data.volume_name = this.$refs.volume_name.value;
      this.selected_form_data.protocol = this.$refs.protocol.value;
      console.log(this.selected_form_data);
    }
  },
  components:{

  },
};

</script>


<template>
  
  <section v-if="show_modal_flag" class="modal_external_wrapper">
    <div class="modal_window">
      <div class="modal_header">
        <p class="modal_header-title">Create Export</p>
        <button class="modal_header-close" @click="off_modal_flag"><img src="./assets/close.png"/></button>
      </div>
      <form class="modal_form" @submit="submit_form">
          <div class="modal_form-elem export-name">
              <label>Export name</label>
              <input ref="export_name" placeholder="my_vol2" type="text" />
          </div>
          <div class="modal_form-elem volume-name">
              <label>Volume name</label>
              <select ref="volume_name">
                <option v-for="elem in form_data.volume_name" >{{elem}}</option>
              </select>
          </div>
          <div class="modal_form-elem protocol">
              <label>Protocol</label>
              <select ref="protocol">
                <option v-for="elem in form_data.protocol">{{elem}}</option>
              </select>
          </div>
          <div class="modal_form-sumbit">
              <button>Cancel</button>
              <input type="submit" value="Create"/>
          </div>
      </form>
    </div>
    <div @click="off_modal_flag" class="black_overlay"></div>
  </section>
  <section class="content">
    
    <button @click="toggle_modal_flag" class="modal_show">
        Открыть модальное окно
    </button>
    <p>Отправленные данные</p>
    <div>
      <p>Export name - {{ selected_form_data.export_name }}</p>
      <p>Volume name - {{ selected_form_data.volume_name }}</p>
      <p>Protocol - {{ selected_form_data.protocol }}</p>
    </div>
  </section>
</template>


<style scoped>
  .content{
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 200px;
    flex-direction: column;
  }
  .modal_show{
    background: none;
    padding: 10px 15px;
    border: 1px solid black;
    border-radius: 5px;
    cursor: pointer;
  }
  .modal_show:hover{
    opacity: 0.5;
    transition: 0.5s;
  }
  .modal_external_wrapper{

  }
  .modal_window{
        background-color: white;
        position: absolute;
        top:50%;
        left:50%;
        width: 400px;
        border-radius: 10px;
        transform:translate(-50%, -50%); 
        z-index: 4;
        padding: 10px 30px;
    }
    .black_overlay{
        background-color: black;
        opacity: 0.7;
        position: absolute;
        z-index: 3;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        cursor: pointer
    }
    .modal_header{
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .modal_header-title{
      font-size: 22px;
      font-weight: bold;
    }
    .modal_header-close{
      background: none;
      border: none;
      width: 30px;
      cursor: pointer;
    }
    .modal_header-close img{
      position: relative;
      width: 100%;
      height: 100%;
    }
    .modal_form-elem input{
      outline: none;
      border: 1px solid #e5e7eb;
      border-radius: 5px;
      cursor: pointer;
      padding: 10px;
    }
    .modal_form-elem select{
      background: none;
      border: 1px solid #e5e7eb;
      border-radius: 5px;
      cursor: pointer;
      padding: 10px;
    }
    .modal_form-elem{
      display: flex;
      flex-direction: column;
      margin-bottom: 20px;
    }
    .modal_form-elem label{
      margin-bottom: 10px;
    }
    .modal_form-sumbit{
      display: flex;
      align-items: flex-end;
      justify-content: flex-end;
      margin-bottom: 35px;
      margin-top: 35px;
    }
    .modal_form-sumbit button{
      background: none;
      border: 1px solid #2a3447;
      padding: 10px 15px;
      margin-right: 10px;
      border-radius: 5px;
      cursor: pointer;
    }
    .modal_form-sumbit input{
      background: #2a3447;
      color: white;
      cursor: pointer;
      border: 1px solid #2a3447;
      padding: 10px 15px;
      border-radius: 5px;
    }
</style>
