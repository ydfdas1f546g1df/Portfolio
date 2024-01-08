<script lang="ts">
    import '$lib/GithubProjects.svelte';
    import GithubProjects from '$lib/GithubProjects.svelte';
    import './+page.less';
</script>

<main>
    <div class="aboutMe">
        <h1>N.K.</h1>
        <div class="nextother">
            <img src="/images/picture.png" />
            <p>
                I'm a X-year-old student currently apprenticing at Bruetsch Elektroniks AG, where my daily focus
                revolves around managing network infrastructure. Additionally, I possess skills in
                backend, frontend development and PowerShell scripting.
            </p>
        </div>
    </div>
    <GithubProjects user="ydfdas1f546g1df" />
</main>
