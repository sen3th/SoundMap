<script>
  let { country = '' } = $props();
</script>

<div class="bg-white rounded-lg shadow-lg p-4 max-w-sm mx-auto mt-4">
  <h3 class="text-xl font-bold mb-2">Country Info</h3>
  <p class="text-lg">{country || '(no data)'}</p>
</div>