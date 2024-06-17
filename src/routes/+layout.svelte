



<script lang="ts">
    import "./+layout.less";
    import "$lib/TopNav.svelte";
    import TopNav from "$lib/TopNav.svelte";

    let NavLinks: {
        name: string,
        url: string,
    }[] = [
        {
            name: "Github",
            url: "https://github.com/ydfdas1f546g1df",
        },
        {
            name: "Linkedin",
            url: "https://www.linkedin.com/in/niklaus-k-098a71259/",
        },
    ];

</script>


<TopNav links={NavLinks} />


<slot />