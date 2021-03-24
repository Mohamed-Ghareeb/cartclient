<template>
    <div class="section">
        <div class="contrainer">
            <div class="columns">
                <div class="column is-half">
                    <img src="http://via.placeholder.com/620x620" alt="product name">
                </div>
                <div class="column is-half">
                    <section class="section">
                        <h1 class="title is-4">
                            {{ product.name }}
                        </h1>
                        <p v-if="product.description">
                            {{ product.description }}
                        </p>

                        <hr>

                        <span class="tag is-rounded is-medium is-dark" v-if="!product.in_stock">
                            Out Of Stock
                        </span>

                        <span class="tag is-rounded is-medium">
                            {{ product.price }}
                        </span>
                    </section>
                    <section class="section">
                        <form action="">
                            <productVariation
                                v-for="(variations, type) in product.variations"
                                :type="type"
                                :variations="variations"
                                :key="type"
                                v-model="form.variation"
                            />

                            <div class="field has-addons" v-if="form.variation">
                                <div class="control">
                                    <div class="select is-fullwidth">
                                        <select name="" id="">
                                        <option value="">1</option>
                                        </select>
                                    </div>
                                </div>
                                <div class="control">
                                <button type="submit" class="button is-info">Add To Cart</button>
                                </div>
                            </div>
                        </form>
                    </section>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Product from '../../assets/styles/components/products/Product.vue'
import ProductVariation from 'assets/styles/components/products/ProductVariation'

export default {
  components: { 
        Product,
        ProductVariation
    },

    data() {
        return {
            product: null,
            form: {
                variation: '',
                quantity: 1
            }
        }
    },

    async asyncData({ params, app }) {
        let response = await app.$axios.$get(`products/${params.slug}`)
    
        return {
            product: response.data
        }
    }
}
</script>