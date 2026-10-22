<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const props = defineProps({
  language: { type: String, default: 'ar' },
})

const emit = defineEmits(['change-language'])

const isArabic = computed(() => props.language === 'ar')
const activeCategory = ref('signature')
const showBackToTop = ref(false)

// ===== ترجمة كاملة =====
const t = computed(() => ({
  langButton: isArabic.value ? 'FR' : 'AR',
  openNow: isArabic.value ? 'مفتوح الآن' : 'Ouvert maintenant',
  closed: isArabic.value ? 'مغلق' : 'Fermé',
  backToTop: isArabic.value ? 'العودة إلى الأعلى' : 'Retour en haut',
  priceNote: isArabic.value ? 'الأسعار بالدينار التونسي' : 'Prix en Dinar Tunisien',
  vegetarian: isArabic.value ? 'نباتي' : 'Végétarien',
  glutenFree: isArabic.value ? 'خالٍ من الغلوتين' : 'Sans gluten',
  new: isArabic.value ? 'جديد' : 'Nouveau',
  chefChoice: isArabic.value ? 'اختيار الباريستا' : 'Choix du Barista',
  mostOrdered: isArabic.value ? 'الأكثر طلباً' : 'Le plus commandé',
  traditional: isArabic.value ? 'حلويات تقليدية' : 'Pâtisseries traditionnelles',
  lastThree: isArabic.value ? 'متبقي 3 فقط' : 'Plus que 3',
  menuTitle: isArabic.value ? 'قائمتنا' : 'Notre Menu',
  contactTitle: isArabic.value ? 'زورونا' : 'Venez nous voir',
  address: isArabic.value ? 'العنوان' : 'Adresse',
  phone: isArabic.value ? 'الهاتف' : 'Téléphone',
  hours: isArabic.value ? 'ساعات العمل' : 'Horaires',
  followUs: isArabic.value ? 'تابعونا' : 'Suivez-nous',
}))

// ===== بيانات المقهى =====
const cafeInfo = computed(() => ({
  name: 'Luna.',
  tagline: isArabic.value ? 'قهوة مختصة · تونس' : 'Café de Spécialité · Tunis',
  established: '2021',
  address: isArabic.value ? '12 شارع الحرية، المرسى، تونس' : '12 Rue de la Liberté, La Marsa, Tunis',
  phone: '+216 71 234 567',
  hours: isArabic.value ? 'كل يوم: 7:00 - 23:00' : 'Tous les jours : 7h00 - 23h00',
  instagram: '@luna.cafe.tn',
  rating: '4.9',
  reviews: '127',
}))

const categories = computed(() => [
  { id: 'signature', name: isArabic.value ? 'توقيع المقهى' : 'Signature' },
  { id: 'coffee', name: isArabic.value ? 'قهوة' : 'Café' },
  { id: 'tea', name: isArabic.value ? 'شاي وأعشاب' : 'Thés & Infusions' },
  { id: 'juice', name: isArabic.value ? 'عصائر طازجة' : 'Jus Frais' },
  { id: 'pastry', name: isArabic.value ? 'حلويات' : 'Pâtisseries' },
  { id: 'sandwich', name: isArabic.value ? 'سندويشات' : 'Sandwichs' },
])

const menuItems = computed(() => [
  // ⭐ توقيع
  { id: 1, category: 'signature', name: isArabic.value ? 'لاتيه الفستق الحلبي' : 'Pistachio Latte', description: isArabic.value ? 'إسبريسو مزدوج، حليب مخملي، كريمة الفستق' : 'Double espresso, lait velouté, crème de pistache', price: 8.9, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1461023058943-07fcbe16d735?w=400', badge: 'chef', dietary: ['V'] },
  { id: 2, category: 'signature', name: isArabic.value ? 'آيس لاتيه كراميل' : 'Iced Caramel Latte', description: isArabic.value ? 'قهوة باردة، حليب، كراميل مملح' : 'Cold brew, lait, caramel salé', price: 9.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1517701604599-bb29b565090c?w=400', badge: 'new', dietary: ['V'] },
  { id: 3, category: 'signature', name: isArabic.value ? 'موكا شوكولاتة' : 'Mocha Chocolat', description: isArabic.value ? 'إسبريسو، شوكولاتة داكنة، حليب مبخر' : 'Espresso, chocolat noir, lait vaporisé', price: 8.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1578374173705-969cbe6f2d6b?w=400', badge: null, dietary: ['V'] },
  { id: 4, category: 'signature', name: isArabic.value ? 'فلات وايت' : 'Flat White', description: isArabic.value ? 'إسبريسو مزدوج، حليب مخملي رقيق' : 'Double espresso, lait micro-mousse', price: 6.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1572442388796-11668a67e53d?w=400', badge: null, dietary: ['V'] },

  // ☕ قهوة
  { id: 5, category: 'coffee', name: isArabic.value ? 'إسبريسو' : 'Espresso', description: isArabic.value ? 'مركز، من محمصتنا المحلية' : 'Serré, de notre torréfacteur local', price: 3.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1510707577719-ae7c14805e3a?w=400', badge: null, dietary: ['V'] },
  { id: 6, category: 'coffee', name: isArabic.value ? 'كابتشينو' : 'Cappuccino', description: isArabic.value ? 'إسبريسو، حليب مبخر، رغوة مخملية' : 'Espresso, lait vaporisé, mousse veloutée', price: 5.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1572442388796-11668a67e53d?w=400', badge: null, dietary: ['V'] },
  { id: 7, category: 'coffee', name: isArabic.value ? 'كورتادو' : 'Cortado', description: isArabic.value ? 'إسبريسو مع كمية مساوية من الحليب' : 'Espresso, quantité égale de lait', price: 4.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1541167760496-1628856ab772?w=400', badge: null, dietary: ['V'] },
  { id: 8, category: 'coffee', name: isArabic.value ? 'في60' : 'V60', description: isArabic.value ? 'قهوة مقطرة، نوتات فاكهية' : 'Pour-over, notes fruitées', price: 7.0, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1544787219-7f47ccb76574?w=400', badge: null, dietary: ['V'] },
  { id: 9, category: 'coffee', name: isArabic.value ? 'أمريكانو' : 'Americano', description: isArabic.value ? 'إسبريسو + ماء ساخن' : 'Espresso + eau chaude', price: 4.0, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1551030173-122aabc4489c?w=400', badge: null, dietary: ['V'] },

  // 🍵 شاي
  { id: 10, category: 'tea', name: isArabic.value ? 'شاي بالصنوبر' : 'Thé aux Pignons', description: isArabic.value ? 'شاي أخضر، نعناع، صنوبر محمص' : 'Thé vert, menthe, pignons torréfiés', price: 4.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1544787219-7f47ccb76574?w=400', badge: 'mostOrdered', dietary: ['V', 'GF'] },
  { id: 11, category: 'tea', name: isArabic.value ? 'شاي أحمر بالفواكه' : 'Thé Fruits Rouges', description: isArabic.value ? 'شاي أسود، فواكه حمراء، عسل' : 'Thé noir, fruits rouges, miel', price: 5.0, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1597481499750-3e6b22637e12?w=400', badge: null, dietary: ['V', 'GF'] },
  { id: 12, category: 'tea', name: isArabic.value ? 'بابونج بالعسل' : 'Camomille au Miel', description: isArabic.value ? 'بابونج طبيعي، عسل، ليمون' : 'Camomille naturelle, miel, citron', price: 4.0, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1576092768241-dec231879fc3?w=400', badge: null, dietary: ['V', 'GF'] },

  // 🧃 عصائر
  { id: 13, category: 'juice', name: isArabic.value ? 'عصير برتقال طازج' : 'Jus d\'Orange Frais', description: isArabic.value ? 'برتقال معصور طازجاً' : 'Orange pressée minute', price: 5.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1600271886742-f049cd451bba?w=400', badge: null, dietary: ['V', 'GF'] },
  { id: 14, category: 'juice', name: isArabic.value ? 'ليموناضة بالنعناع' : 'Limonade Menthe', description: isArabic.value ? 'ليمون طازج، نعناع، سكر خفيف' : 'Citron frais, menthe, sucre léger', price: 4.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1621263764928-df1444c5e859?w=400', badge: null, dietary: ['V', 'GF'] },
  { id: 15, category: 'juice', name: isArabic.value ? 'عصير فراولة' : 'Jus de Fraise', description: isArabic.value ? 'فراولة طازجة، حليب' : 'Fraises fraîches, lait', price: 6.0, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1553530666-ba11a7da3888?w=400', badge: null, dietary: ['V'] },

  // 🍰 حلويات
  { id: 16, category: 'pastry', name: isArabic.value ? 'مقروض' : 'Makroud', description: isArabic.value ? 'سميد محشي بالتمر، عسل' : 'Semoule fourrée aux dattes, miel', price: 3.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1533134242443-d4fd215305ad?w=400', badge: 'traditional', dietary: ['V'] },
  { id: 17, category: 'pastry', name: isArabic.value ? 'بامبالوني' : 'Bambalouni', description: isArabic.value ? 'دونات تونسي، سكر ناعم' : 'Beignet tunisien, sucre glace', price: 2.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1551024506-0bccd828d307?w=400', badge: null, dietary: ['V'] },
  { id: 18, category: 'pastry', name: isArabic.value ? 'كرواسون اللوز' : 'Croissant Amande', description: isArabic.value ? 'كرواسون طازج، كريمة اللوز' : 'Croissant frais, crème d\'amande', price: 4.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1555507036-ab1f4038808a?w=400', badge: 'lastThree', dietary: ['V'] },
  { id: 19, category: 'pastry', name: isArabic.value ? 'تشيز كيك' : 'Cheesecake', description: isArabic.value ? 'جبن كريمي، بسكويت، توت' : 'Cream cheese, biscuit, fruits rouges', price: 7.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1533134242443-d4fd215305ad?w=400', badge: null, dietary: ['V'] },
  { id: 20, category: 'pastry', name: isArabic.value ? 'كيك الشوكولاتة' : 'Gâteau Chocolat', description: isArabic.value ? 'شوكولاتة داكنة، طبقات' : 'Chocolat noir, couches', price: 6.0, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1606313564200-e75d5e30476c?w=400', badge: null, dietary: ['V'] },

  // 🥪 سندويشات
  { id: 21, category: 'sandwich', name: isArabic.value ? 'سندويش تونة' : 'Sandwich Thon', description: isArabic.value ? 'تونة، طماطم، زيتون، خبز طازج' : 'Thon, tomates, olives, pain frais', price: 6.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1528735602780-2552fd46c7af?w=400', badge: null, dietary: [] },
  { id: 22, category: 'sandwich', name: isArabic.value ? 'سندويش دجاج' : 'Sandwich Poulet', description: isArabic.value ? 'دجاج مشوي، خس، مايونيز' : 'Poulet grillé, salade, mayonnaise', price: 7.5, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1521390188846-e2a3a97453a0?w=400', badge: null, dietary: [] },
  { id: 23, category: 'sandwich', name: isArabic.value ? 'سندويش حلوم' : 'Sandwich Halloumi', description: isArabic.value ? 'جبن حلوم مشوي، خيار، نعناع' : 'Halloumi grillé, concombre, menthe', price: 8.0, currency: isArabic.value ? 'د.ت' : 'DT', image: 'https://images.unsplash.com/photo-1539252554453-80ab65ce3586?w=400', badge: 'new', dietary: ['V'] },
])

const filteredItems = computed(() =>
  activeCategory.value === 'signature'
    ? menuItems.value.filter(i => i.category === 'signature')
    : menuItems.value.filter(i => i.category === activeCategory.value)
)

// badge → label
function badgeLabel(badge) {
  return t.value[badge] || ''
}

const badgeClasses = {
  chef: 'text-[#8B6F47] border-[#8B6F47] bg-white/90',
  mostOrdered: 'text-[#2D6A4F] border-[#2D6A4F] bg-white/90',
  new: 'text-[#1E40AF] border-[#1E40AF] bg-white/90',
  traditional: 'text-[#9C6B3C] border-[#9C6B3C] bg-white/90',
  lastThree: 'text-[#9C2C2C] border-[#9C2C2C] bg-white/90',
}

// ===== Scroll handlers =====
let scrollFrame = null
function handleScroll() {
  if (scrollFrame !== null) return
  scrollFrame = window.requestAnimationFrame(() => {
    showBackToTop.value = window.scrollY > 400
    scrollFrame = null
  })
}
function scrollToTop() {
  window.scrollTo({
    top: 0,
    behavior: window.matchMedia('(prefers-reduced-motion: reduce)').matches ? 'auto' : 'smooth',
  })
}

onMounted(() => window.addEventListener('scroll', handleScroll, { passive: true }))
onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  if (scrollFrame) cancelAnimationFrame(scrollFrame)
})
</script>

<template>
  <div :dir="isArabic ? 'rtl' : 'ltr'" class="min-h-screen bg-[#FDFBF7] text-[#2C2C2C] font-sans selection:bg-[#8B6F47] selection:text-white relative">
    
    <!-- Sticky Language Switcher -->
    <div class="fixed top-4 end-4 z-50">
      <button
        @click="emit('change-language')"
        class="flex items-center gap-1.5 px-3 py-1.5 rounded-full bg-[#2C2C2C]/90 backdrop-blur-sm text-white text-xs font-medium border border-white/20 hover:bg-[#8B6F47] transition-colors shadow-lg"
      >
        <svg class="w-3.5 h-3.5" fill="none" stroke="currentColor" stroke-width="1.7" viewBox="0 0 24 24">
          <circle cx="12" cy="12" r="9" /><path d="M3 12h18M12 3a15 15 0 0 1 0 18M12 3a15 15 0 0 0 0 18" />
        </svg>
        {{ t.langButton }}
      </button>
    </div>

    <!-- HERO -->
    <section class="relative h-[55vh] min-h-[420px] overflow-hidden">
      <img src="https://images.unsplash.com/photo-1554118811-1e0d58224f24?w=1600" :alt="cafeInfo.name" class="absolute inset-0 w-full h-full object-cover" />
      <div class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/40 to-transparent"></div>
      <div class="relative h-full flex flex-col justify-end pb-10 px-6 max-w-6xl mx-auto">
        <p class="text-[10px] tracking-[0.4em] text-[#D4AF37] uppercase mb-3">{{ cafeInfo.tagline }}</p>
        <h1 class="text-5xl sm:text-7xl font-serif text-white tracking-tight">{{ cafeInfo.name }}</h1>
        <div class="flex items-center gap-3 mt-4 text-xs text-white/70">
          <span>⭐ {{ cafeInfo.rating }} ({{ cafeInfo.reviews }})</span>
          <span>·</span>
          <span>{{ cafeInfo.hours }}</span>
        </div>
      </div>
    </section>

    <!-- INFO BAR -->
    <div class="bg-[#2C2C2C] text-white py-3 px-6">
      <div class="max-w-6xl mx-auto flex flex-wrap items-center justify-between gap-2 text-[11px] tracking-wide">
        <span>{{ cafeInfo.address }}</span>
        <span class="text-[#D4AF37]">{{ cafeInfo.phone }}</span>
        <span>{{ cafeInfo.instagram }}</span>
      </div>
    </div>

    <!-- TABS -->
    <nav class="sticky top-0 z-20 bg-[#FDFBF7]/95 backdrop-blur-sm border-b border-gray-200">
      <div class="max-w-6xl mx-auto flex gap-6 overflow-x-auto px-6 py-4 scrollbar-hide">
        <button
          v-for="cat in categories" :key="cat.id"
          class="shrink-0 text-sm font-medium transition-all pb-2 border-b-2"
          :class="activeCategory === cat.id ? 'text-[#8B6F47] border-[#8B6F47]' : 'text-gray-400 border-transparent hover:text-gray-600'"
          @click="activeCategory = cat.id"
        >
          {{ cat.name }}
        </button>
      </div>
    </nav>

    <!-- MENU GRID -->
    <main class="max-w-6xl mx-auto px-4 sm:px-6 py-8 pb-24">
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4 sm:gap-5">
        <article v-for="item in filteredItems" :key="item.id" class="group bg-white rounded-lg overflow-hidden shadow-sm hover:shadow-md transition-shadow duration-300 border border-gray-100 flex flex-col">
          <div class="relative aspect-[4/3] overflow-hidden bg-gray-100">
            <img :src="item.image" :alt="item.name" class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105" loading="lazy" />
            <span v-if="item.badge" class="absolute top-2 start-2 text-[10px] font-semibold border px-2 py-0.5 rounded-full backdrop-blur-sm" :class="badgeClasses[item.badge]">
              {{ badgeLabel(item.badge) }}
            </span>
          </div>
          <div class="p-4 flex flex-col flex-1">
            <h3 class="text-sm font-semibold text-[#2C2C2C] leading-tight mb-1">{{ item.name }}</h3>
            <p class="text-xs text-gray-500 leading-relaxed line-clamp-2 mb-2">{{ item.description }}</p>
            <div v-if="item.dietary?.length" class="flex gap-1 mb-2">
              <span v-for="tag in item.dietary" :key="tag" class="text-[9px] font-medium px-1.5 py-0.5 rounded bg-gray-100 text-gray-600">
                {{ tag === 'V' ? t.vegetarian : t.glutenFree }}
              </span>
            </div>
            <div class="mt-auto flex items-baseline justify-between">
              <span class="text-base font-light text-[#8B6F47]">{{ item.price }} <span class="text-xs">{{ item.currency }}</span></span>
            </div>
          </div>
        </article>
      </div>
      <p class="text-center text-[10px] text-gray-400 mt-10 tracking-wide">{{ cafeInfo.name }} · {{ cafeInfo.instagram }} · {{ t.priceNote }}</p>
    </main>

    <!-- Footer info -->
    <footer class="bg-[#2C2C2C] text-white py-8 px-6">
      <div class="max-w-6xl mx-auto grid grid-cols-1 sm:grid-cols-3 gap-6 text-center sm:text-start">
        <div>
          <p class="text-[10px] tracking-[0.3em] text-[#D4AF37] uppercase mb-2">{{ t.address }}</p>
          <p class="text-xs text-white/70">{{ cafeInfo.address }}</p>
        </div>
        <div>
          <p class="text-[10px] tracking-[0.3em] text-[#D4AF37] uppercase mb-2">{{ t.phone }}</p>
          <p class="text-xs text-white/70" dir="ltr">{{ cafeInfo.phone }}</p>
        </div>
        <div>
          <p class="text-[10px] tracking-[0.3em] text-[#D4AF37] uppercase mb-2">{{ t.hours }}</p>
          <p class="text-xs text-white/70">{{ cafeInfo.hours }}</p>
        </div>
      </div>
      <p class="text-center text-[10px] text-white/30 mt-6 tracking-wide">© {{ cafeInfo.established }} {{ cafeInfo.name }} · {{ t.followUs }} {{ cafeInfo.instagram }}</p>
    </footer>

    <!-- Back to Top -->
    <Transition
      enter-active-class="transition duration-300 ease-out"
      enter-from-class="translate-y-3 opacity-0"
      enter-to-class="translate-y-0 opacity-100"
      leave-active-class="transition duration-200 ease-in"
      leave-from-class="translate-y-0 opacity-100"
      leave-to-class="translate-y-3 opacity-0"
    >
      <button
        v-if="showBackToTop"
        @click="scrollToTop"
        class="fixed bottom-6 end-6 z-40 flex h-11 w-11 items-center justify-center rounded-full bg-[#2C2C2C] text-white shadow-lg hover:bg-[#8B6F47] transition-colors duration-300 focus:outline-none focus:ring-2 focus:ring-[#8B6F47] focus:ring-offset-2"
        :aria-label="t.backToTop"
      >
        <svg class="h-5 w-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" d="M12 19V5m0 0-7 7m7-7 7 7" />
        </svg>
      </button>
    </Transition>
  </div>
</template>

<style scoped>
.scrollbar-hide::-webkit-scrollbar {
  display: none;
}
.scrollbar-hide {
  -ms-overflow-style: none;
  scrollbar-width: none;
}
</style>