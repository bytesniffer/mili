<template>
    <div class="search-view">
        <Pinterest url="/articles" :start="2" :query="{cPath: categoryPathName, sort}" @load="onLoad">
            <template v-slot:loading>
                <div style="padding: 20px; padding-top: 10px;">
                    <ArticleLoading />
                </div>
            </template>
            <template v-slot:content>
                <div>
                    <div class="article-list">
                        <ArticleItem :key="article.id" v-for="article in articles" :article="article" />
                    </div>
                </div>
            </template>
        </Pinterest>
    </div>
</template>

<script>
import ArticleLoading from '~/js/components/article/ArticleLoading.vue';
import ArticleItem from '~/js/components/article/ArticleItem.vue';
import { ErrorCode } from '~/js/constants/error.js';
import Pinterest from '~/js/components/common/Pinterest.vue';

export default {
    data () {
        return {
            articles: [],
            categoryPathName: window.categoryPathName || undefined,
            sort: window.sort,
        };
    },
    mounted() {
        this.$nextTick(() => {
        });
    },
    methods: {
        onLoad(result) {
            this.articles = this.articles.concat(result.data.data.list);
        }
    },
    components: {
        ArticleLoading,
        ArticleItem,
        Pinterest,
    }
}
</script>
