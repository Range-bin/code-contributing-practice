<script>
    import { onMount } from 'svelte';

    let users = [];

    onMount(async () => {
        const response = await fetch('http://localhost:8090/api/users', {
            headers: {
                // 如果需要的话，添加Authorization头
                'Authorization': 'Bearer YOUR_POCKETBASE_AUTH_TOKEN',
            }
        });
        if (response.ok) {
            const data = await response.json();
            users = data.items; // 根据PocketBase的响应结构调整
        }
    });
</script>

<main>
    <h1>Registered Users</h1>
    <ul>
        {#each users as user}
            <li>{user.email} - {user.created}</li> <!-- 根据你的数据结构调整 -->
        {/each}
    </ul>
</main>