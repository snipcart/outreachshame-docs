<template>
<div>
    <div v-for="post in posts">
        <h2>
            <router-link :to="post.path">{{ post.frontmatter.title }}</router-link>
        </h2>
        
        <p>{{ post.frontmatter.description }}</p>

        <p><router-link :to="post.path">Read more</router-link></p>
    </div>
</div>
</template>

<script>
export default {
    computed: {
        posts() {
            return this.$site.pages
                .filter(x => x.path.startsWith('/blog/') && 
                            !x.frontmatter.blog_index)
                .sort((a, b) => {
                    const date1 = new Date(a.frontmatter.date);
                    const date2 = new Date(b.frontmatter.date);

                    return date2 - date1;
                });
        }
    },
    methods: {
        viewPost(path) {
            alert(path);
        }
    },
    mounted() {
        console.log(this.$site);
    }
}
</script>

