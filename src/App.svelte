<script lang="ts">
  import { onMount } from 'svelte'
  import { Input } from '$lib/components/ui/input'
  import { Label } from '$lib/components/ui/label'
  import Katex from 'svelte-katex'
  import 'katex/dist/katex.min.css'

  let value: string = 'y = ax + b'
</script>
 
<div class="p-6 max-w-4xl mx-auto grid gap-6">
  <div>
    <Label for="input">数式</Label>
    <Input bind:value id="input" />
  </div>
  <Katex displayMode>{value}</Katex>
</div>
