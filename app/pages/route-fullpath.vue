<script setup lang="ts">

/**========== external link ========= */
useHead({
  link: [
    {
      rel: "stylesheet",
      href: "https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
    }
  ],
  script: [
    { src: "https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js" }
  ]
})


/**=========  Fetch Data From API ========= */

const {data:alldata,refresh} = await useFetch('https://dummyjson.com/products');



/**=========  ROUTE + ROUTER ======== */
const route = useRoute()
const router = useRouter()

/**========= Search Input ========= */
const search = ref(route.query.search || "")
const categorys = ref(route.query.categorys || "")
const priceSort = ref("")
const rating = ref(0)




/**  find uniques category for category fileter  */
const uniqueCategories = computed(()=>{
    const cats = alldata.value?.products?.map(p => p.category) || [] 
    return [...new Set(cats)]
})


const filteredProducts = computed(() => {
  let products = alldata.value?.products || []

  /**----------- search filter --------- */
  if (search.value) {
    const q = search.value.toLowerCase()
    products = products.filter(p => p.title.toLowerCase().includes(q))
  }

  /**--------- category filter ---------- */
  if (categorys.value) {
    products = products.filter(p => p.category === categorys.value)
  }


  /**-----  price filter ------- */
   if (priceSort.value === "low") {
    products = [...products].sort((a, b) => a.price - b.price)
  }

  if (priceSort.value === "high") {
    products = [...products].sort((a, b) => b.price - a.price)
  }

  /**----- Rating filter ----- */
  if(rating.value > 0){
    products = products.filter(p => p.rating >= rating.value)
  }
  return products
})








/**========= Refresh when route changes ========= */





watch(() => route.query.search, () => {
  refresh()
})

</script>




<template>

  <h1>Search Filter Example</h1>
  <hr>
    

  <section>
    <div class="container">
      <!-- search input -->
      <div class="input-group mb-3">
        <input 
          type="text" 
          v-model="search"  
          class="form-control" 
          placeholder="Search products..."
        >
      </div>

            <div class="row">
              <div class="col-lg-3">
              <select class="form-select mb-3 form-control" aria-label="Default select example " v-model="categorys">
                <option value="" disabled  selected>Open this select menu</option>
                <option :value="cate" :key="cate" v-for="cate in uniqueCategories">{{ cate }}</option>
              </select>
              </div>
              <!-- col end  -->
              <div class="col-lg-3">
              <select class="form-select mb-3 form-control" aria-label="Default select example " v-model="priceSort">
                <option value="" disabled  selected>Select Price </option>
                <option value="low" >Low to High</option>
                <option value="high" > High to Low</option>
              </select>
              </div>
              <!-- col end  -->
              <div class="col-lg-3">
                <select v-model="rating" class="border p-2 form-control form-select">
                  <option value="0" selected disabled>All Ratings</option>
                  <option value="1">1★ & Up</option>
                  <option value="2">2★ & Up</option>
                  <option value="3">3★ & Up</option>
                  <option value="4">4★ & Up</option>
                  <option value="5">5★ Only</option>
                </select>
              </div>
              <!-- col end  -->
            </div>

      <div class="row">
        <!-- product data -->
        <div 
          class="col-12 col-sm-6 col-md-6 col-lg-3 mb-3" 
          v-for="pro in filteredProducts" :key="pro.id" >
          <div class="card" style="width: 18rem;">
             <img :src="pro.thumbnail" class="card-img-top" alt="dfdf">
            <div class="card-body">
              <h5 class="card-title">{{ pro.title }}</h5>
              <h6 class="card-subtitle mb-2 text-body-secondary">
                BDT {{ pro.price }}
              </h6>
              <p class="card-text">{{ pro.description }}</p>
              <h5>{{ pro.category }}</h5>
              <p><span class="text-warning"> Rating: {{ pro.rating }}</span></p>
              <a href="#" class="card-link">More Details</a>
            </div>
          </div>
        </div>
      </div>

    </div>
  </section>




</template>
