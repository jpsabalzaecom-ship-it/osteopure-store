 <template>
  <div class="min-h-screen bg-white font-sans">
    <!-- Top Promo Bar -->
    <div class="bg-red-600 text-white text-center py-4 text-2xl font-bold">
      50% OFF
    </div>

    <!-- Total Section -->
    <div class="bg-teal-600 text-white py-6 px-6 text-center">
      <p class="text-lg">TOTAL AMOUNT</p>
      <p class="text-4xl font-bold mt-1">₱2450.00</p>
      <p class="text-sm opacity-75 line-through mt-1">₱4900.00</p>
      <p class="mt-3 text-yellow-300 font-medium">DISCOUNT COUPON APPLIED</p>
      <p class="bg-white/20 inline-block px-4 py-2 rounded-lg mt-2 text-sm font-semibold">
        CODE: SPARK2026
      </p>
    </div>

    <!-- Packages -->
    <div class="px-4 py-6 space-y-4 max-w-2xl mx-auto">
      <!-- Package 1 -->
      <div 
        @click="selectedPkg = 0"
        class="border-2 rounded-xl p-4 cursor-pointer transition"
        :class="selectedPkg === 0 ? 'border-teal-500 bg-teal-50' : 'border-gray-200'"
      >
        <div class="flex justify-between items-center">
          <div>
            <p class="font-bold text-lg">BUY 1</p>
            <p class="text-sm text-gray-500">(Good for 1 mos)</p>
          </div>
          <div class="text-right">
            <p class="font-bold text-teal-700">₱11.25</p>
            <p class="text-xs text-gray-500">per day</p>
          </div>
        </div>
      </div>

      <!-- Package 2 - Most Popular -->
      <div 
        @click="selectedPkg = 1"
        class="border-2 rounded-xl p-4 cursor-pointer relative transition"
        :class="selectedPkg === 1 ? 'border-yellow-500 bg-yellow-50' : 'border-yellow-400 bg-yellow-50/50'"
      >
        <div class="absolute -top-3 left-1/2 -translate-x-1/2 bg-yellow-500 text-white px-4 py-1 rounded-full text-sm font-bold">
          MOST POPULAR
        </div>
        <div class="flex justify-between items-center mt-2">
          <div>
            <p class="font-bold text-lg">BUY 1 TAKE 1</p>
            <p class="text-sm text-gray-500">(Good for 2 mos)</p>
          </div>
          <div class="text-right">
            <p class="font-bold text-teal-700">₱8.70</p>
            <p class="text-xs text-gray-500">per day</p>
          </div>
        </div>
      </div>

      <!-- Package 3 -->
      <div 
        @click="selectedPkg = 2"
        class="border-2 rounded-xl p-4 cursor-pointer transition"
        :class="selectedPkg === 2 ? 'border-teal-500 bg-teal-50' : 'border-gray-200'"
      >
        <div class="flex justify-between items-center">
          <div>
            <p class="font-bold text-lg">BUY 1 TAKE 2</p>
            <p class="text-sm text-gray-500">(Good for 3 mos)</p>
          </div>
          <div class="text-right">
            <p class="font-bold text-teal-700">₱7.20</p>
            <p class="text-xs text-gray-500">per day</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Delivery Form -->
    <div class="px-4 pb-8 max-w-2xl mx-auto">
      <h3 class="text-center font-bold text-lg mb-5 text-gray-800">
        COMPLETE THE DETAILS TO ENSURE PROPER DELIVERY
      </h3>

      <form @submit.prevent="submitOrder" class="space-y-3">
        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">MOBILE#</label>
          <input 
            v-model="form.mobile"
            type="text" 
            placeholder="09"
            class="w-full border border-gray-300 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-teal-500"
          />
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-3">
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">FIRSTNAME</label>
            <input 
              v-model="form.firstName"
              type="text" 
              placeholder="FIRST NAME"
              class="w-full border border-gray-300 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-teal-500"
            />
          </div>
          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">LASTNAME</label>
            <input 
              v-model="form.lastName"
              type="text" 
              placeholder="LAST NAME"
              class="w-full border border-gray-300 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-teal-500"
            />
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">ADDRESS</label>
          <input 
            v-model="form.address"
            type="text" 
            placeholder="BLK/LOT/STREET/SUBDIVISION"
            class="w-full border border-gray-300 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-teal-500"
          />
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">PROVINCE</label>
          <select 
            v-model="form.province"
            class="w-full border border-gray-300 rounded-lg px-4 py-3 bg-white focus:outline-none focus:ring-2 focus:ring-teal-500"
          >
            <option value="">SELECT PROVINCE</option>
            <option v-for="p in provinces" :key="p" :value="p">{{ p }}</option>
          </select>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">CITY / MUNICIPALITY</label>
          <select 
            v-model="form.city"
            class="w-full border border-gray-300 rounded-lg px-4 py-3 bg-white focus:outline-none focus:ring-2 focus:ring-teal-500"
          >
            <option value="">SELECT CITY</option>
            <option v-for="c in cities" :key="c" :value="c">{{ c }}</option>
          </select>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">BARANGAY</label>
          <select 
            v-model="form.barangay"
            class="w-full border border-gray-300 rounded-lg px-4 py-3 bg-white focus:outline-none focus:ring-2 focus:ring-teal-500"
          >
            <option value="">SELECT BARANGAY</option>
            <option v-for="b in barangays" :key="b" :value="b">{{ b }}</option>
          </select>
        </div>

        <div>
          <label class="block text-sm font-medium text-gray-700 mb-1">LANDMARK</label>
          <input 
            v-model="form.landmark"
            type="text" 
            placeholder="NOTE: ISULAT ANG TAMA..."
            class="w-full border border-gray-300 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-teal-500"
          />
        </div>

        <button 
          type="submit"
          class="w-full bg-green-600 hover:bg-green-700 text-white text-xl font-bold py-4 rounded-lg transition mt-4"
          :disabled="isSubmitting"
        >
          <span v-if="isSubmitting">SENDING...</span>
          <span v-else>SUBMIT ORDER</span>
        </button>
      </form>
    </div>

    <!-- Footer Badges -->
    <div class="border-t py-6 text-center">
      <div class="flex justify-center items-center gap-4 flex-wrap mb-3 font-bold">
        <span class="text-red-600">LBC EXPRESS</span>
        <span class="text-orange-500">J&T EXPRESS</span>
        <span class="text-red-600">COD Cash on Delivery</span>
      </div>
      <p class="text-gray-600 font-medium">100% Legit — Real Parcels Delivered</p>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const selectedPkg = ref(null)
const isSubmitting = ref(false)
const form = ref({
  mobile: '',
  firstName: '',
  lastName: '',
  address: '',
  province: '',
  city: '',
  barangay: '',
  landmark: ''
})

const provinces = ref(['Metro Manila', 'Cavite', 'Laguna', 'Batangas', 'Pampanga'])
const cityMap = {
  'Metro Manila': ['Manila', 'Quezon City', 'Makati', 'Pasay', 'Taguig'],
  'Cavite': ['Dasmariñas', 'Bacoor', 'Imus', 'Cavite City', 'Trece Martires'],
  'Laguna': ['Calamba', 'Santa Rosa', 'San Pablo', 'Biñan', 'San Pedro'],
  'Batangas': ['Batangas City', 'Lipa', 'Tanauan', 'Taal', 'Balayan'],
  'Pampanga': ['San Fernando', 'Angeles', 'Mabalacat', 'Guagua', 'Mexico']
}
const brgyMap = {
  'Manila': ['Binondo', 'Intramuros', 'Malate', 'Ermita', 'Tondo'],
  'Quezon City': ['Diliman', 'Bagong Silang', 'Pag-asa', 'Batasan Hills', 'Novaliches'],
  'Makati': ['Poblacion', 'Bel-Air', 'San Lorenzo', 'Urdaneta', 'Guadalupe']
}

const cities = computed(() => cityMap[form.value.province] || [])
const barangays = computed(() => brgyMap[form.value.city] || [])

const packages = [
  { id: 'buy1', name: 'BUY 1', price: 2450, desc: 'Good for 1 month', perDay: '₱11.25' },
  { id: 'buy1take1', name: 'BUY 1 TAKE 1', price: 2450, desc: 'Good for 2 months', perDay: '₱8.70' },
  { id: 'buy1take2', name: 'BUY 1 TAKE 2', price: 2450, desc: 'Good for 3 months', perDay: '₱7.20' }
]

// ==============================================
// 🔑 PANCAKE POS CREDENTIALS
// ==============================================
const SHOP_ID = '408130136'
const PANCAKE_API_KEY = '8ed4ddab5ba8b08eeb789989974ac63f'
const PANCAKE_CREATE_ORDER_URL = 'https://pos.pancake.biz/api/orders'

async function submitOrder() {
  // Validation
  if (selectedPkg.value === null) return alert('Pumili muna ng package!')
  const { mobile, firstName, lastName, address, province, city, barangay } = form.value
  if (!mobile || !firstName || !lastName || !address || !province || !city || !barangay) {
    return alert('Punan lahat ng required fields!')
  }
  if (!PANCAKE_WEBHOOK_URL) {
    return alert('⚠️ Kulang ang Webhook URL!\nPumunta sa Pancake POS → Webhook URL tab → kopyahin → ilagay sa code.')
  }

  isSubmitting.value = true
  const pkg = packages[selectedPkg.value]

  const orderData = {
    order_id: `ORD${Date.now()}`,
    package_name: pkg.name,
    package_description: pkg.desc,
    total_amount: 2450,
    original_price: 4900,
    discount_code: 'SPARK2026',
    discount_percent: 50,
    customer: {
      first_name: firstName,
      last_name: lastName,
      phone: mobile,
      address: `${address}, ${barangay}, ${city}, ${province}`,
      landmark: form.value.landmark || ''
    },
    payment_method: 'COD',
    delivery_carrier: ['LBC', 'J&T'],
    currency: 'PHP',
    created_at: new Date().toISOString()
  }

  console.log('📤 Sending to Pancake POS:', orderData)

  try {
    const res = await fetch(PANCAKE_WEBHOOK_URL, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'API-Key': PANCAKE_API_KEY
      },
      body: JSON.stringify(orderData)
    })

    const result = await res.json()
    console.log('📥 Response from Pancake POS:', result)

    if (res.ok) {
      alert('✅ Order Submitted!\nNapasok na sa Pancake POS.')
      selectedPkg.value = null
      form.value = { mobile: '', firstName: '', lastName: '', address: '', province: '', city: '', barangay: '', landmark: '' }
    } else {
      alert(`❌ Error: ${result.message || 'Hindi nakapasok sa system'}`)
    }
  } catch (err) {
    console.error('Pancake POS Error:', err)
    alert('⚠️ Hindi makakonekta — tignan ang Webhook URL at API Key.')
  } finally {
    isSubmitting.value = false
  }
}
</script>
