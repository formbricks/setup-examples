<script lang="ts">
  import { navigating } from '$app/stores';
  import { env } from '$env/dynamic/public';
  import type fbT from '@formbricks/js';
  import { onMount } from 'svelte';

  let formbricks: typeof fbT;

  onMount(() => {
    import('@formbricks/js').then((fb) => {
      formbricks = fb.default;
      formbricks.init({
        environmentId: env.PUBLIC_FORMBRICKS_ENVIRONMENT_ID || 'not set',
        apiHost: 'https://app.formbricks.com', // Cloud Hosted API
        debug: import.meta.env.DEV, // Enable debug mode on dev
      });

      (window as any).formbricks = formbricks;
    });
  });

  $: if ($navigating) formbricks.registerRouteChange();
</script>
