<script setup>
import { onMounted, onUnmounted, reactive, ref } from "vue";

const isScrolled = ref(false);
const isNavOpen = ref(false);
const formStatus = ref("");

const reservation = reactive({
  name: "",
  phone: "",
  date: "",
  time: "",
  party: 2,
  note: "",
});

const navItems = [
  { label: "菜单", href: "#menu" },
  { label: "空间", href: "#space" },
  { label: "营业", href: "#hours" },
  { label: "预订", href: "#reserve" },
];

const menuItems = [
  {
    title: "迷迭香炭烤小羊排",
    description: "配暖暖鹰嘴豆泥、烤甜椒和一勺薄荷酸奶",
    price: "¥168",
    image: "https://images.unsplash.com/photo-1555939594-58d7cb561ad1?auto=format&fit=crop&w=900&q=82",
    alt: "烤肉和蔬菜主菜",
  },
  {
    title: "松露菌菇手作意面",
    description: "奶香帕玛森、现磨黑胡椒和慢熬蘑菇汁",
    price: "¥118",
    image: "https://images.unsplash.com/photo-1551218808-94e220e084d2?auto=format&fit=crop&w=900&q=82",
    alt: "厨师正在摆盘",
  },
  {
    title: "柑橘布拉塔小沙拉",
    description: "芝麻叶、开心果与蜂蜜油醋汁，清爽又温柔",
    price: "¥86",
    image: "https://images.unsplash.com/photo-1543353071-10c8ba85a904?auto=format&fit=crop&w=900&q=82",
    alt: "餐盘中的新鲜沙拉",
  },
];

const stats = [
  { value: "36", label: "餐位" },
  { value: "4", label: "包间" },
  { value: "21:30", label: "最后点餐" },
];

const hours = [
  { label: "周一至周五", value: "11:30 - 14:00 / 17:30 - 22:00" },
  { label: "周六至周日", value: "11:30 - 22:30" },
  { label: "电话", value: "021-6188-0927" },
];

const timeOptions = ["17:30", "18:00", "18:30", "19:00", "19:30", "20:00"];

const syncHeader = () => {
  isScrolled.value = window.scrollY > 16;
};

const closeNav = () => {
  isNavOpen.value = false;
};

const submitReservation = () => {
  formStatus.value = `${reservation.name}，已收到您 ${reservation.date} ${reservation.time} 的预订请求，我们会尽快电话确认。`;

  Object.assign(reservation, {
    name: "",
    phone: "",
    date: "",
    time: "",
    party: 2,
    note: "",
  });
};

onMounted(() => {
  syncHeader();
  window.addEventListener("scroll", syncHeader, { passive: true });
});

onUnmounted(() => {
  window.removeEventListener("scroll", syncHeader);
});
</script>

<template>
  <header class="site-header" :class="{ 'is-scrolled': isScrolled, 'is-open': isNavOpen }">
    <a class="brand" href="#top" aria-label="栖味餐厅首页" @click="closeNav">
      <span class="brand-mark">QW</span>
      <span>
        <strong>栖味</strong>
        <small>Bistro & Table</small>
      </span>
    </a>

    <button
      class="nav-toggle"
      type="button"
      :aria-label="isNavOpen ? '关闭导航' : '打开导航'"
      :aria-expanded="String(isNavOpen)"
      @click="isNavOpen = !isNavOpen"
    >
      <span></span>
      <span></span>
      <span></span>
    </button>

    <nav class="site-nav" :class="{ 'is-open': isNavOpen }" aria-label="主导航">
      <a v-for="item in navItems" :key="item.href" :href="item.href" @click="closeNav">
        {{ item.label }}
      </a>
    </nav>
  </header>

  <main id="top">
    <section class="hero" aria-label="栖味餐厅介绍">
      <img
        class="hero-image"
        src="https://images.unsplash.com/photo-1504674900247-0877df9cc836?auto=format&fit=crop&w=2200&q=85"
        alt="摆满当季料理的餐桌"
      />
      <div class="hero-shade"></div>
      <div class="hero-content">
        <p class="eyebrow">当季餐桌 | 手作酱汁 | 城市小聚</p>
        <h1>栖味餐厅</h1>
        <p class="hero-copy">
          用炭火、香草和慢熬高汤做一桌有温度的晚餐。适合两个人的安静约会，也适合一群朋友的轻松小聚。
        </p>
        <div class="hero-actions">
          <a class="button primary" href="#reserve">预约座位</a>
          <a class="button secondary" href="#menu">查看菜单</a>
        </div>
      </div>
      <aside class="hero-note" aria-label="今日推荐">
        <span>今日推荐</span>
        <strong>香草烤鸡配柠檬黄油汁</strong>
        <small>18:00 后供应</small>
      </aside>
    </section>

    <section class="intro section-band">
      <div class="section-inner intro-grid">
        <div>
          <p class="eyebrow">Fresh every day</p>
          <h2>从市场到餐桌，保留食材本来的香气。</h2>
        </div>
        <p>
          我们每天根据海鲜、蔬菜和香草的状态调整菜单。厨房保留开放式动线，让烘烤、煎烤和调汁的过程成为用餐的一部分。
        </p>
      </div>
    </section>

    <section class="menu-section" id="menu">
      <div class="section-inner">
        <div class="section-heading">
          <p class="eyebrow">Warm signatures</p>
          <h2>想和你分享的几道菜</h2>
          <p>热腾腾上桌，慢慢吃，适合把一天里的好心情留在餐桌边。</p>
        </div>

        <div class="menu-grid">
          <article v-for="item in menuItems" :key="item.title" class="menu-card">
            <img :src="item.image" :alt="item.alt" />
            <div class="menu-card-body">
              <div>
                <h3>{{ item.title }}</h3>
                <p>{{ item.description }}</p>
              </div>
              <strong>{{ item.price }}</strong>
            </div>
          </article>
        </div>
      </div>
    </section>

    <section class="space-section" id="space">
      <div class="section-inner space-grid">
        <div class="space-copy">
          <p class="eyebrow">Dining room</p>
          <h2>有火光，也有安静角落。</h2>
          <p>
            靠窗区适合午后简餐，吧台能看到厨房出餐，长桌区为生日、团队晚餐和朋友聚会预留了更从容的距离。
          </p>
          <dl class="stats">
            <div v-for="item in stats" :key="item.label">
              <dt>{{ item.value }}</dt>
              <dd>{{ item.label }}</dd>
            </div>
          </dl>
        </div>
        <div class="space-photo-wrap">
          <img
            class="space-photo"
            src="https://images.unsplash.com/photo-1517248135467-4c7edcad34c4?auto=format&fit=crop&w=1400&q=84"
            alt="温暖灯光下的餐厅室内空间"
          />
        </div>
      </div>
    </section>

    <section class="visit-section section-band" id="hours">
      <div class="section-inner visit-grid">
        <div class="visit-block">
          <p class="eyebrow">Visit</p>
          <h2>今晚来吃点好的。</h2>
          <p>上海市静安区梧桐路 118 号 1F</p>
        </div>
        <div class="hours-list" aria-label="营业时间">
          <div v-for="item in hours" :key="item.label">
            <span>{{ item.label }}</span>
            <strong>{{ item.value }}</strong>
          </div>
        </div>
      </div>
    </section>

    <section class="reserve-section" id="reserve">
      <div class="section-inner reserve-grid">
        <div>
          <p class="eyebrow">Reservation</p>
          <h2>预订座位</h2>
          <p>
            告诉我们人数和到店时间。提交后前台会尽快确认，如需包间或生日布置，可以在备注里说明。
          </p>
        </div>

        <form class="reserve-form" @submit.prevent="submitReservation">
          <label>
            姓名
            <input v-model.trim="reservation.name" type="text" name="name" placeholder="您的称呼" required />
          </label>
          <label>
            电话
            <input v-model.trim="reservation.phone" type="tel" name="phone" placeholder="联系电话" required />
          </label>
          <label>
            日期
            <input v-model="reservation.date" type="date" name="date" required />
          </label>
          <label>
            时间
            <select v-model="reservation.time" name="time" required>
              <option value="">选择时间</option>
              <option v-for="time in timeOptions" :key="time">{{ time }}</option>
            </select>
          </label>
          <label>
            人数
            <input v-model.number="reservation.party" type="number" name="party" min="1" max="12" required />
          </label>
          <label class="form-wide">
            备注
            <textarea
              v-model.trim="reservation.note"
              name="note"
              rows="3"
              placeholder="忌口、儿童椅、包间需求"
            ></textarea>
          </label>
          <button class="button primary form-wide" type="submit">提交预订</button>
          <p class="form-status form-wide" aria-live="polite">{{ formStatus }}</p>
        </form>
      </div>
    </section>
  </main>

  <footer class="site-footer">
    <div class="section-inner footer-grid">
      <div>
        <strong>栖味 Bistro & Table</strong>
        <p>市场鲜味、炭火料理、自然酒。</p>
      </div>
      <a href="#top">回到顶部</a>
    </div>
  </footer>
</template>
