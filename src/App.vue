<template>
  <div>
    <!-- สร้าง inputText เพื่อรับข้อมูลส่วนตัวจากผู้ใช้-->
    <h2>แบบฟอร์มเก็บข้อมูลส่วนตัว</h2>
    <form @submit.prevent="submitForm">
      <div>
        <label>คำนำหน้าชื่อ:</label>
        <input type="text" v-model="prefix" />
      </div>
      <div>
        <label>ชื่อ:</label>
        <input type="text" v-model="firstName" />
      </div>
      <div>
        <label>นามสกุล:</label>
        <input type="text" v-model="lastName" />
      </div>
      <div>
        <label>เพศ:</label>
        <select v-model="gender">
          <option value="ชาย">ชาย</option>
          <option value="หญิง">หญิง</option>
        </select>
      </div>
      <div>
        <label>วันเกิด:</label>
        <input type="number" v-model="birthDay" placeholder="วัน" />
        <input type="number" v-model="birthMonth" placeholder="เดือน" />
        <input type="number" v-model="birthYear" placeholder="ปี" />
      </div>
      <div>
        <label>อายุ:</label>
        {{ age }}
      </div>
      <div>
        <label>ที่อยู่:</label>
        <textarea v-model="address"></textarea>
      </div>
      <div>
        <label>อำเภอ:</label>
        <input type="text" v-model="district" />
      </div>
      <div>
        <label>ตำบล:</label>
        <input type="text" v-model="subdistrict" />
      </div>
      <div>
        <label>งานอดิเรก:</label>
        <input type="text" v-model="hobby" />
      </div>
      <div>
        <label>ภาษาโปรเเกรมที่ชอบ:</label>
        <input type="text" v-model="favoriteLanguage" />
      </div>
      <button type="submit">Submit</button>
    </form>
    <div v-if="isSubmitted">
      <h2>ข้อมูลที่เพิ่มล่าสุด:</h2>
      <p>คำนำหน้าชื่อ: {{ prefix }}</p>
      <p>ชื่อ: {{ firstName }}</p>
      <p>นามสกุล: {{ lastName }}</p>
      <p>เพศ: {{ gender }}</p>
      <p>วันเกิด: {{ birthDay }}/{{ birthMonth }}/{{ birthYear }}</p>
      <p>อายุ: {{ age }}</p>
      <p>ที่อยู่: {{ address }}</p>
      <p>อำเภอ: {{ district  }}</p>
      <p>ตำบล: {{ subdistrict }}</p>
      <p>งานอดิเรก: {{ hobby }}</p>
      <p>ภาษาโปรเเกรมที่ชอบ: {{ favoriteLanguage }}</p>
      </div>
        </div>
</template>
<script>
export default {
  data() {
    return {
      prefix: '',
      firstName: '',
      lastName: '',
      gender: '',
      birthDay: '',
      birthMonth: '',
      birthYear: '',
      address: '',
      district: '',
      subdistrict: '',
      hobby: '',
      favoriteLanguage: '',
      isSubmitted: false,
    };
  },
  // ใช้ computed รับข้อมูลวันเกิดของผู้ใข้เเล้วคำนวณอายุออกมา โดยการคำนวณจะถูกทำเมื่อมีการเปลี่ยนแปลงข้อมูลในฟอร์ม
  computed: {
    age() {
      if (this.birthDay && this.birthMonth && this.birthYear) {
        const birthDate = new Date(this.birthYear, this.birthMonth - 1, this.birthDay);
        const today = new Date();
        const ageDiff = today.getTime() - birthDate.getTime();
        const ageDate = new Date(ageDiff);
        return Math.abs(ageDate.getUTCFullYear() - 1970);
      }
      return '';
    },
  },
  //เมื่อผู้ใช้กดปุ่ม Submit เพื่อเปลี่ยนค่า isSubmitted เป็น true เพื่อแสดงผลข้อมูลที่กรอกในฟอร์ม
  methods: {
    submitForm() {
      this.isSubmitted = true;
    },
  },
};
</script>

