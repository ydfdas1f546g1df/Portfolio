<script lang="ts">
    export let user:string = "";

    async function getProjects():Promise<any> {
        const response = await fetch(`https://api.github.com/users/${user}/repos`);
        const data = await response.json();
        return data;
    }

    let projects = getProjects();


</script>

<style lang="less">

</style>

<div class="GithubProjects">
    <p>{projects}</p>
</div>