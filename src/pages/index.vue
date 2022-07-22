<script setup lang="ts">
import { useUserStore } from '~/stores/user'

import { BaseTree, Draggable, obj, BaseNode, Node } from '@he-tree/vue3'
import '@he-tree/vue3/dist/he-tree-vue3.css'

const flatData = [
  { text: 'node1', selected: false, id: 1 },
  { text: 'node2', selected: false, id: 2 },
  { text: 'node1-1', selected: false, id: 3, pid: 1 },
  { text: 'node1-2', selected: false, id: 4, pid: 1 },
  { text: 'node1-3', selected: false, id: 5, pid: 1 }
]

const user = useUserStore()
const name = $ref(user.savedName)

const selected = $ref(0)

const router = useRouter()
const go = () => {
  if (name) router.push(`/hi/${encodeURIComponent(name)}`)
}

const { t } = useI18n()

const showDrawer = $ref(false)
</script>

<template>
  <div
    class="
      lg:display-none
      fixed
      inset-0
      bg-black/10
      z-990
      transition-all
      duration-200
    "
    :class="{
      'pointer-events-auto': showDrawer,
      'opacity-0 pointer-events-none': !showDrawer
    }"
    @click="showDrawer = false"
  ></div>
  <aside
    class="
      w-full
      max-w-80
      z-990
      fixed
      inset-y-0
      py-4
      pl-4
      transition-transform
      duration-200
      lg:left-0
    "
    :class="{
      'translate-0': showDrawer,
      '-translate-x-full lg:translate-x-0': !showDrawer
    }"
  >
    <div
      class="
        bg-white
        p-4
        w-full
        h-full
        rounded-2xl
        shadow-soft-xl
        overflow-y-auto
      "
    >
      <Draggable :flatData="flatData" idKey="id" parentIdKey="pid">
        <template v-slot="{ node, tree }">
          <div
            @click="selected = node.id"
            :class="{'outline outline-1': selected === node.id}" 
            class="relative flex items-center p-1 bg-slate-100 rounded-2 flex"
          >
            <Icon class="i-tabler-grip-vertical text-sm" />
            <span ml-1>
              {{ node.text }}
            </span>
            <div 
              v-if="node.$children.length > 0"
              @click="tree.toggleFold(node)" 
              class="flex absolute right-0 w-6 h-6 items-center justify-center rounded-2 mr-1 hover:bg-slate-400 hover:text-white"
            >
              <Icon 
                :class="node.$folded ? 'i-tabler-chevron-down' : 'i-tabler-chevron-up'"
                class="text-sm mr-[.5px]"
              />
            </div>
          </div>
        </template>
      </Draggable>
    </div>
  </aside>

  <main
    class="
      pt-4
      flex flex-col
      gap-4
      ease-soft-in-out
      lg:ml-80
      min-h-screen
      max-h-screen
      transition-all
      duration-200
    "
  >
    <ToolBar>
        <button
          @click="showDrawer = true"
          class="lg:display-none p-2 hover:bg-teal-400/10 rounded-lg"
        >
          <Icon i-tabler-menu-2 text-teal-500 />
        </button>
    </ToolBar>

    <section class="bg-gray-100 p-4 mx-4 flex-1 mb-4 rounded-2xl">
      content
    </section>
  </main>
</template>

<route lang="yaml">
meta:
  layout: default
</route>

