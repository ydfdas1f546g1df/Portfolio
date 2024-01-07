<script lang="ts">
    import { onMount } from 'svelte';

    interface Project {
        id: number;
        node_id: string;
        name: string;
        full_name: string;
        private: boolean;
        owner: {
            login: string;
            id: number;
            node_id: string;
            avatar_url: string;
            gravatar_id: string;
            url: string;
            html_url: string;
            followers_url: string;
            following_url: string;
            gists_url: string;
            starred_url: string;
            subscriptions_url: string;
            organizations_url: string;
            repos_url: string;
            events_url: string;
            received_events_url: string;
            type: string;
            site_admin: boolean;
        };
        html_url: string;
        description: string;
        fork: boolean;
        url: string;
        forks_url: string;
        keys_url: string;
        collaborators_url: string;
        teams_url: string;
        hooks_url: string;
        issue_events_url: string;
        events_url: string;
        assignees_url: string;
        branches_url: string;
        tags_url: string;
        blobs_url: string;
        git_tags_url: string;
        git_refs_url: string;
        trees_url: string;
        statuses_url: string;
        languages_url: string;
        stargazers_url: string;
        contributors_url: string;
        subscribers_url: string;
        subscription_url: string;
        commits_url: string;
        git_commits_url: string;
        comments_url: string;
        issue_comment_url: string;
        contents_url: string;
        compare_url: string;
        merges_url: string;
        archive_url: string;
        downloads_url: string;
        issues_url: string;
        pulls_url: string;
        milestones_url: string;
        notifications_url: string;
        labels_url: string;
        releases_url: string;
        deployments_url: string;
        created_at: string;
        updated_at: string;
        pushed_at: string;
        git_url: string;
        ssh_url: string;
        clone_url: string;
        svn_url: string;
        homepage: string;
        size: number;
        stargazers_count: number;
        watchers_count: number;
        language: string;
        has_issues: boolean;
        has_projects: boolean;
        has_downloads: boolean;
        has_wiki: boolean;
        has_pages: boolean;
        forks_count: number;
        mirror_url: string;
        archived: boolean;
        disabled: boolean;
        open_issues_count: number;
        license: {
            key: string;
            name: string;
            spdx_id: string;
            url: string;
            node_id: string;
        };
        forks: number;
        open_issues: number;
        watchers: number;
        default_branch: string;
        languages: string[] | undefined;
    }

    export let user: string = '';

    let isFetching: boolean = false;
    let projects: Project[];

    onMount(
        async () => {
            try {
                isFetching = true;
                console.log('fetching projects');
                const response = await fetch(`https://api.github.com/users/${user}/repos`);
                if (!response.ok) {
                    console.log('error loading from GitHub');
                } else {
                    projects = await response.json();
                    console.log(projects);
                }
                console.log('done fetching projects');
                console.log('fetching project languages');
                for (let project of projects) {
                    project.languages = [];
                    const response = await fetch(`https://api.github.com/repos/${project.full_name}/languages`);
                    if (!response.ok) {
                        console.log('error loading from GitHub');
                    } else {
                        let temp = await response.json();
                        let templ: any;
                        project.languages = Object.keys(temp).map((language) => language.toLowerCase());
                        console.log(project.languages);
                    }
                }
                console.log('done fetching project languages');

            } catch (e) {
                console.error(e);
            } finally {
                isFetching = false;
                // force reactivity
            }
        }
    );


</script>

<style lang="less">
  @import "$lib/colors";

  @spinner-size: 40px; // Adjust the size of the spinner

  .spinner-container {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh; // Adjust the height of the container as needed
  }

  .spinner {
    border: 4px solid rgba(0, 0, 0, 0.1);
    border-top: 4px solid #3498db; // Adjust the color of the spinner
    border-radius: 50%;
    width: @spinner-size;
    height: @spinner-size;
    animation: spin 1s linear infinite;
  }

  @keyframes spin {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }

  .GithubProjects {
    max-width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    .project {
      display: flex;
      flex-direction: column;
      text-decoration: none;
      border-radius: 1rem;
      background-color: lighten(@backgroundcolor, 10%);
      padding: 1rem;
      margin: 1rem;
      font-size: 1.6rem;
      height: auto;
      width: auto;



      .languageHolder {
        display: flex;
        flex-direction: row;
        .language-proj {
          font-size: 1rem;
          display: inline-block;
          margin: 0.5rem;
          padding: 0.5rem;
          border-radius: 0.5rem;
          background-color: lighten(@backgroundcolor, 20%);
          color: @fontColor;

        }
      }
    }
  }
</style>

<div class="GithubProjects">
    {#if isFetching}
        <div class="loading">

            <div class="spinner-container">
                <div class="spinner"></div>
            </div>
            <p>Loading</p>
        </div>
    {:else if projects !== undefined}
        {#each projects as project}
            <a class="project" href={project.html_url}>
                {project.name}


                <div class="languageHolder">
                    {#if project.languages !== undefined && project.languages.length > 0}
                        {#each project.languages as language}
                            <p class="language-proj">{language}</p>

                        {/each}
                    {:else}

                        <p class="language-proj">No Lang Available</p>

                    {/if}
                </div>

            </a>
        {/each}
    {/if}
</div>