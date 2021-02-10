<template>
    <div class="card">
        <div class="card-image">
            <figure class="image is-4by3">
            <nuxt-link :to="link">
                <img src="http://via.placeholder.com/620x620" alt="">            
            </nuxt-link>
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-contetnt">
                    <nuxt-link :to="link" class="title is-5">{{ product.name }}</nuxt-link>
                </div>
            </div>
            <div class="contetnt">
                <p v-if="product.description">{{ product.description }}</p>
                <span class="tag is-rounded is-large">{{ product.price }}</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
        product: {
            required: true,
            type: Object
        }
    },

    computed: {
        link() {
            return { name: 'products-slug', params: {slug: this.product.slug} }
        }
    }
}
</script>