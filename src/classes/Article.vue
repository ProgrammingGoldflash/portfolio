<script lang="ts">
export default class Article {
    constructor(
        public title: string,
        public url: string,
        public description: string,
        public cover_image?: string,
    ) { }
}
</script>
