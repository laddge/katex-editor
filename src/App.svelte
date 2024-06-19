<script lang="ts">
  import { onMount } from 'svelte'
  import { Input } from '$lib/components/ui/input'
  import { Label } from '$lib/components/ui/label'
  import Katex from 'svelte-katex'
  import 'katex/dist/katex.min.css'

  let value: string = 'y = ax + b'
</script>
 
<h1 class="text-2xl font-bold text-center py-3 bg-sky-100">TeX数式ビューワー</h1>
<div class="p-6 max-w-4xl mx-auto grid gap-6">
  <p><Katex>\TeX</Katex>の数式を表示します.</p>
  <div>
    <Label for="input">数式</Label>
    <Input bind:value id="input" />
  </div>
  <Katex displayMode>{value}</Katex>
</div>
