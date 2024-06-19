<script lang="ts">
  import { onMount } from 'svelte'
  import { Input } from '$lib/components/ui/input'
  import { Label } from '$lib/components/ui/label'
  import { Button } from '$lib/components/ui/button'
  import * as DropdownMenu from '$lib/components/ui/dropdown-menu'
  import Image from 'lucide-svelte/icons/image'
  import ImageDown from 'lucide-svelte/icons/image-down'
  import ChevronDown from 'lucide-svelte/icons/chevron-down'
  import Katex from 'svelte-katex'
  import 'katex/dist/katex.min.css'
  import { toPng } from 'dom-to-image'

  let value: string = 'y = ax + b'
  let output: HTMLDivElement
  let dataUrl: string = ''

  const genImg = async (transparent: bool = false) => {
    dataUrl = await toPng(output, {
      width: output.clientWidth * 3,
      height: output.clientHeight * 3,
      style: {
        transform: 'scale(3)',
        transformOrigin: 'top left',
        padding: '1px',
        backgroundColor: transparent ? 'transparent' : 'white',
      },
    })
  }
</script>
 
<h1 class="text-2xl font-bold text-center py-3 bg-sky-100">TeX数式ビューワー</h1>
<div class="p-6 max-w-3xl mx-auto grid gap-6">
  <p><Katex>\TeX</Katex>の数式を表示します.</p>
  <div>
    <Label for="input">数式</Label>
    <Input bind:value id="input" on:keyup={() => { dataUrl = '' }} />
  </div>
  <div bind:this={output}>
    <Katex displayMode>{value}</Katex>
  </div>
  <div class="flex">
    <Button on:click={() => genImg()} class="grow rounded-r-none">
      <Image class="mr-2 h-4 w-4" />
      画像化
    </Button>
    <DropdownMenu.Root>
      <DropdownMenu.Trigger>
        <Button class="rounded-l-none">
          <ChevronDown class="h-4 w-4" />
        </Button>
      </DropdownMenu.Trigger>
      <DropdownMenu.Content>
        <DropdownMenu.Group>
          <DropdownMenu.Item on:click={() => genImg(true)} class="px-4">画像化(背景透過)</DropdownMenu.Item>
          </DropdownMenu.Group>
      </DropdownMenu.Content>
    </DropdownMenu.Root>
  </div>
  {#if dataUrl}
    <div>
      <img src={dataUrl} class="border-t border-x bg-ichimatsu" />
      <a href={dataUrl} download="output.png">
        <Button variant="outline" class="w-full rounded-t-none">
          <ImageDown class="mr-2 h-4 w-4" />
          ダウンロード
        </Button>
      </a>
    </div>
  {/if}
</div>

<style>
  .bg-ichimatsu {
    background-image: linear-gradient(45deg, #f5f5f5 25%, transparent 25%, transparent 75%, #f5f5f5 75%), linear-gradient(45deg, #f5f5f5 25%, transparent 25%, transparent 75%, #f5f5f5 75%);
    background-position: 0 0, 8px 8px;
    background-size: 16px 16px;
    background-color: #FFF; 
  }
</style>
