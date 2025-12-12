<template>
    <div class="property-list">
        <!-- search bar -->
         <input v-model="search"
         type="text"
         placeholder="Search"
         class="search-input"
         />

         <!-- sort Dropdown -->
        <select v-model="sortOrder" class="sort-select">
            <option value="asc">Price: Low to High</option>
            <option value="desc">Price: High to Low</option>
        </select>

          <!-- property cards -->
        <div class="cards">
            <div 
            v-for="property in filteredAndSortedProperties"
            :key="property.id"
            class="card">
            <img :src="property.image ? property.image : 'https://via.placeholder.com/280x160?text=No+Image'" alt="Property" class="card-img" />
            <h3>{{ property.type }}</h3>
            <p>{{ property.location }}</p>
            <p class="price">R{{ property.price.toLocaleString() }}</p>
        </div>
     </div>
    </div>

</template>

<script>
export default {
    name: "PropertyList",
    data(){
        return{
            search:"",
            sortOrder:"asc",
            properties: [
                {
                    id:1,
                    type: "Open Land",
                    location: "belhar",
                    price: 50000,
                    image: "https://image-prod.iol.co.za/16x9/800/LAUNCH-A-total-of-152-units-have-been-completed-in-Belhar-Gardens-Rental-Estate-CREDIT-Brendan-Magaar?source=https://xlibris.public.prod.oc.inl.infomaker.io:8443/opencontent/objects/1653b546-a62d-564b-8fa8-5d948f2c787c&operation=CROP&offset=141x0&resize=2857x1606",
                },
                {
                    id:2,
                    type: "Flat Apartment",
                    location: "Delft",
                    price: 600000,
                    image: "https://tse2.mm.bing.net/th/id/OIP.STmF_IZu9X4cQm2B30RYhwHaFj?rs=1&pid=ImgDetMain&o=7&rm=3",
                },
                {
                    id:3,
                    type: "Apartment",
                    location: "Mitchels Plain",
                    price: 500000,
                    image: "https://tse4.mm.bing.net/th/id/OIP.ZrlLtaAIh3eovyvL2oo7wgHaFj?rs=1&pid=ImgDetMain&o=7&rm=3",
                },
                {
                    id:4,
                    type: "Flat Apartment",
                    location: "Manenburg",
                    price: 720000,
                    image: "https://tse3.mm.bing.net/th/id/OIP.hRGEjgrYCEdVYDD3katfdAHaJ4?rs=1&pid=ImgDetMain&o=7&rm=3",
                },
                {
                    id:5,
                    type: "House",
                    location: "Valahala Park",
                    price: 150000,
                    image: "https://imgza.waa2.com/home/061023/2-bed-house-in-valhalla-park-da89e58eed5824a2d32a195fa85fea32_thumb.jpg",
                },
                {
                    id:6,
                    type: "Flat Apartment",
                    location: "Sea Point",
                    price: 1500000,
                    image: "https://s3.entegral.net/b/f_10f0b2a933274c14b6b07cd50eefbf7e.jpg",
                },
            ]
        };
    }, 
computed:{
    filteredAndSortedProperties(){
        // filter by search
        let filtered = this.properties.filter((p)=>
        p.type.toLowerCase().includes(this.search.toLowerCase()) || p.location.toLowerCase().includes(this.search.toLowerCase())
        )
    
        return filtered.sort((a,b) =>{
            return this.sortOrder === "asc" ? a.price - b.price : b.price - a.price
        })
        },
    }
}
</script>

<style scoped>
.property-list {
  margin: 3vw;
  padding: 20px;
  justify-content: center;
}

.search-input,
.sort-select {
  padding: 8px;
  margin: 10px 5px;
}

.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
}

.card {
  border: 1px solid #ddd;
  border-radius: 6px;
  padding: 10px;
  width: 40vw;
  height:50vh;
  box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

.card-img {
  width: 100%;
  height: 35vh;
  object-fit: cover;
  border-radius: 4px;
}

.price {
  font-weight: bold;
  color: #2c3e50;
}

</style>