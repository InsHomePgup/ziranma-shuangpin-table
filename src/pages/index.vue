<script setup lang="ts">
interface KeyInfo {
  key: string
  initial: string
  final: string
  row: number
}

const keyData: KeyInfo[] = [
  { key: 'Q', initial: 'q', final: 'iu', row: 1 },
  { key: 'W', initial: 'w', final: 'ia / ua', row: 1 },
  { key: 'E', initial: '', final: 'e', row: 1 },
  { key: 'R', initial: 'r', final: 'uan（üan）', row: 1 },
  { key: 'T', initial: 't', final: 'ue（üe）', row: 1 },
  { key: 'Y', initial: 'y', final: 'ing / uai', row: 1 },
  { key: 'U', initial: 'sh', final: 'u', row: 1 },
  { key: 'I', initial: 'ch', final: 'i', row: 1 },
  { key: 'O', initial: '', final: 'o / uo', row: 1 },
  { key: 'P', initial: 'p', final: 'un（ün）', row: 1 },
  { key: 'A', initial: '', final: 'a', row: 2 },
  { key: 'S', initial: 's', final: 'ong / iong', row: 2 },
  { key: 'D', initial: 'd', final: 'iang / uang', row: 2 },
  { key: 'F', initial: 'f', final: 'en', row: 2 },
  { key: 'G', initial: 'g', final: 'eng', row: 2 },
  { key: 'H', initial: 'h', final: 'ang', row: 2 },
  { key: 'J', initial: 'j', final: 'an', row: 2 },
  { key: 'K', initial: 'k', final: 'ao', row: 2 },
  { key: 'L', initial: 'l', final: 'ai', row: 2 },
  { key: 'Z', initial: 'z', final: 'ei', row: 3 },
  { key: 'X', initial: 'x', final: 'ie', row: 3 },
  { key: 'C', initial: 'c', final: 'iao', row: 3 },
  { key: 'V', initial: 'zh', final: 'ui', row: 3 },
  { key: 'B', initial: 'b', final: 'ou', row: 3 },
  { key: 'N', initial: 'n', final: 'in', row: 3 },
  { key: 'M', initial: 'm', final: 'ian', row: 3 },
]

const rowOffsetUnits: Record<number, number> = {
  1: 0,
  2: 0.25,
  3: 0.75,
}

const keyboardRows = computed(() => (
  [1, 2, 3].map(row => keyData.filter(k => k.row === row))
))
</script>

<template>
  <div class="keyboard-page flex min-h-screen w-full items-center justify-center">
    <div class="keyboard flex flex-col items-stretch">
      <div
        v-for="(row, rowIndex) in keyboardRows"
        :key="rowIndex"
        class="key-row flex"
        :style="{ marginLeft: `calc((var(--key) + var(--gap)) * ${rowOffsetUnits[rowIndex + 1]})` }"
      >
        <div
          v-for="item in row"
          :key="item.key"
          class="key-cap flex flex-col items-center justify-between rounded-lg border border-gray-300 bg-white shadow-sm select-none"
        >
          <span class="key-initial font-medium text-gray-600">{{ item.initial }}</span>
          <span class="key-letter font-bold text-gray-800">{{ item.key }}</span>
          <span class="key-final font-medium text-emerald-600">{{ item.final }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.keyboard-page {
  box-sizing: border-box;
  padding: clamp(0.5rem, 3vw, 2rem);
  overflow-x: auto;
}

.keyboard {
  --key: clamp(2.2rem, 9vw, 8rem);
  --gap: clamp(0.2rem, 1vw, 0.85rem);
  gap: var(--gap);
  border: 1px solid #d1d5db;
  border-radius: 0.75rem;
  background: #f9fafb;
  padding: var(--gap);
}

.key-row {
  gap: var(--gap);
}

.key-cap {
  width: var(--key);
  height: var(--key);
  padding: calc(var(--key) * 0.06) 0;
  box-sizing: border-box;
}

.key-initial,
.key-final {
  font-size: clamp(0.7rem, 1.8vw, 1.15rem);
  line-height: 1;
  white-space: nowrap;
}

.key-letter {
  font-size: clamp(1.3rem, 4.6vw, 2.75rem);
  line-height: 1;
}
</style>
