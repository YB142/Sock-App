<template>
    <div> 
        <span class="tabs"
            :class="{ activeTab: selectedTab === tab}"
            v-for="(tab) in tabs" 
            @click="selectedTab = tab"
            :key="tab">
            {{ tab }}</span>

            <div v-show="selectedTab === 'Reviews'">
            <p v-if="!reviews.length">There are no reviews yet.</p>
            <ul v-else>
                <li v-for="(review, index) in reviews" :key="index">
                <p>{{ review.name }}</p>
                <p>Rating: {{ review.rating }}</p>
                <p>{{ review.review }}</p>
                </li>
            </ul>
            </div>

            <div v-show="selectedTab === 'Make a Review'"> 
            <product-review></product-review>
            </div>
    </div>
</template>

<script>
import ProductReview from './review.vue';
export default {
    props: {
        reviews: {
            type: Array,
            required: false
        }
    }, 
    components: {
        ProductReview
    },
    data() {
        return {
            tabs: ['Reviews', 'Make a Review'],
            selectedTab: 'Reviews'
    
        }
    }
}
</script>
