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


/**========= Update URL on typing =========
 * akhane search holo reactive value jeta input theke asce 
 * (value) value holo input box kico change hoyar pore setar update value . or search er update value last input value 
 * route.push diye amra route change korteci .. or input jeta type hobe seta abar route add hobe 
 * ... er mane holo ager joto query ace sob thakbe + search er value add hobe    ... jodi na thake tahole ager filter remove hobe 
 * search:value hocce value add hobe 
 * 
 *  */

// const updateUrl = () => {
//     router.push({
//         query:{
//             search: search.value || undefined,
//             category: categorys.value || undefined,
//         }
//     })
// }


// watch([search,categorys],()=>{
//     updateUrl()
// })

/**========= Fetch Search Result ========= */



/**  find uniques category for category fileter  */
const uniqueCategories = computed(()=>{
    const cats = alldata.value?.products?.map(p => p.category) || [] 
    return [...new Set(cats)]
})


const filteredProducts = computed(() => {
  let products = alldata.value?.products || []

  if (search.value) {
    const q = search.value.toLowerCase()
    products = products.filter(p => p.title.toLowerCase().includes(q))
  }

  if (categorys.value) {
    products = products.filter(p => p.category === categorys.value)
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
            </div>

      <div class="row">
        <!-- product data -->
        <div 
          class="col-12 col-sm-6 col-md-6 col-lg-3 mb-3" 
          v-for="pro in filteredProducts" :key="pro.id" >
          <div class="card" style="width: 18rem;">
            <div class="card-body">
              <h5 class="card-title">{{ pro.title }}</h5>
              <h6 class="card-subtitle mb-2 text-body-secondary">
                BDT {{ pro.price }}
              </h6>
              <p class="card-text">{{ pro.description }}</p>
              <h5>{{ pro.category }}</h5>
              <a href="#" class="card-link">More Details</a>
            </div>
          </div>
        </div>
      </div>

    </div>
  </section>




</template>
