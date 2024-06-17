
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-D7D7N8ZJD2"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-D7D7N8ZJD2');
</script>


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