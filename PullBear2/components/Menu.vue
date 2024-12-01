<template>
  <div>
    <!-- Hamburger Menü Iconu -->
    <div class="menu-icon" @click="toggleSidebar">
      <div class="bar"></div>
      <div class="bar"></div>
      <div class="bar"></div>
    </div>

    <!-- Sidebar -->
    <transition name="sidebar-transition" @before-enter="beforeEnter" @enter="enter" @leave="leave">
      <div v-show="isSidebarVisible" class="sidebar">
        <!-- Kapatma butonu (Çarpı ikonu) -->
        <div class="close-btn" @click="toggleSidebar">
          <div class="close-icon"></div>
          <div class="close-icon"></div>
        </div>

        <ul class="menu-options">
          <li @click="selectCategory('men')">Erkek</li>
          <li @click="selectCategory('women')">Kadın</li>
        </ul>

        <div v-if="selectedCategory === 'men'" class="category-list men-category">
          <ul>
            <li>Gömlek</li>
            <li>Pantolon</li>
            <li>Şort</li>
            <li>Mont</li>
            <li>Ayakkabı</li>
          </ul>
        </div>

        <div v-if="selectedCategory === 'women'" class="category-list women-category">
          <ul>
            <li>Elbise</li>
            <li>Bluz</li>
            <li>Jüp</li>
            <li>Yelek</li>
            <li>Babet</li>
          </ul>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isSidebarVisible: false, // Sidebar başlangıçta gizli
      selectedCategory: null,  // Başlangıçta kategori seçili değil
    };
  },
  methods: {
    toggleSidebar() {
      this.isSidebarVisible = !this.isSidebarVisible; // Sidebar'ı açma/kapama
    },
    selectCategory(category) {
      this.selectedCategory = category;
    },
    beforeEnter(el) {
      el.style.transform = 'translateX(-100%)'; // Başlangıç pozisyonu
    },
    enter(el, done) {
      el.offsetHeight; // Trigger reflow to restart animation
      el.style.transition = 'transform 0.3s ease-in-out';
      el.style.transform = 'translateX(0)';
      done();
    },
    leave(el, done) {
      el.style.transition = 'transform 0.3s ease-in-out';
      el.style.transform = 'translateX(-100%)';
      done();
    }
  },
};
</script>

<style scoped>
/* Hamburger Menu Iconu */
.menu-icon {
  cursor: pointer;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 30px;
  height: 25px;
  margin: 20px;
}

.bar {
  height: 5px;
  background-color: #333;
  border-radius: 5px;
  transition: transform 0.3s ease;
}

/* Sidebar */
.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  width: 250px;
  height: 100%;
  background-color: #333;
  color: white;
  padding-top: 20px;
  transition: transform 0.3s ease-in-out;
}

/* Kapatma butonu (Çarpı ikonu) */
.close-btn {
  position: absolute;
  top: 20px;
  right: 20px;
  cursor: pointer;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 20px;
}

.close-icon {
  width: 25px;
  height: 3px;
  background-color: white;
  border-radius: 5px;
}

.close-icon:first-child {
  transform: rotate(45deg);
}

.close-icon:last-child {
  transform: rotate(-45deg);
}

/* Menü seçenekleri için stil (Erkek ve Kadın aynı satırda) */
.menu-options {
  display: flex;
  justify-content: space-between;
  padding: 0 20px;
}

.menu-options li {
  cursor: pointer;
  padding: 10px;
}

.menu-options li:hover {
  background-color: #444;
}

ul {
  list-style-type: none;
  padding-left: 0;
}

.category-list {
  margin-top: 20px;
  padding-left: 20px;
}

/* Erkek ve Kadın Kategorileri için farklı stiller */
.men-category {
  background-color: #1e3a8a;  /* Erkek kategorisi için mavi arka plan */
}

.women-category {
  background-color: #d946ef;  /* Kadın kategorisi için pembe arka plan */
}

.men-category ul,
.women-category ul {
  padding-left: 20px;
}

.men-category li,
.women-category li {
  font-size: 18px; /* Ürün isimlerinin boyutu */
  padding: 8px 0;
}

.men-category li:hover,
.women-category li:hover {
  background-color: #444;
  font-size: 20px; /* Hover durumunda ürün boyutunu artır */
}

button {
  padding: 10px;
  cursor: pointer;
  margin: 20px;
  background-color: #333;
  color: white;
  border: none;
}

/* Hamburger Menü animasyonu */
.menu-icon.open .bar:nth-child(1) {
  transform: translateY(10px) rotate(45deg);
}

.menu-icon.open .bar:nth-child(2) {
  opacity: 0;
}

.menu-icon.open .bar:nth-child(3) {
  transform: translateY(-10px) rotate(-45deg);
}
</style>
