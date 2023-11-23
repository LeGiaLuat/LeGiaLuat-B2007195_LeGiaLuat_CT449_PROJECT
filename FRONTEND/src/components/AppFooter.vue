<template>
<footer class="bg-info" id="lkfooter">
    <div class="container link">
                  &#169; Stationery Shop Demo
    </div>
</footer>
</template>
<style scoped>
       @import "@/assets/style.css"; 
       .danhsach {
  background-color:  rgba(10, 143, 215, 0.436); 
  max-width: max-content;
  font-weight: 600;
}

.danhsach :hover{
    margin-right: 4;
    color: black;
    font-weight: bolder;
    font-size: large;
    background-color:  rgba(10, 143, 215, 0.436);
  }
</style>
<script>
import loaihangService from "../services/loaihang.service";
export default {
  props: {
    session_user: { type : Object, default : null} // dữ liệu kiểm tra đăng nhập
  },
  data() {
    return {
      loaihang: []
    };
  },
  computed: {
    loaihangStrings() {
                return this.loaihang.map((loai) => {
                     const {tenloai } = loai;
                    return [tenloai].join("");
                });
            },
    filteredLoaiCho() {
      return this.loaihang.filter((_loai,index) => this.loaihangStrings[index].includes('chó'));
    },
    filteredLoaiMeo() {
      return this.loaihang.filter((_loai,index) => this.loaihangStrings[index].includes('mèo'));
    },
    
  },
  
  methods: {
  setSession_user(){
    this.$store.commit('setSessionUser', null)
  },
  async getALLLoaiHang() {
                try {
                    // lấy danh sách các loại hàng
                  this.loaihang = await loaihangService.getAll();
                } catch (error) {
                    console.log(error);
                }
            },
},
mounted(){
this.getALLLoaiHang(); // gọi khi trang vừa được load
}
}
</script>