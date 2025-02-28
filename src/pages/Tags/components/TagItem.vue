<template>
  <Transition name="default" mode="out-in" appear>
    <RouterLink :to="{name:'search' , query : {tags:[tag.tag_name]}}" class="tagItem">
      <strong style="margin-right: auto ;"> <strong>#</strong> {{ tag.tag_name }}</strong>
      <strong>{{ blogcount }}</strong>
    </RouterLink>
  </Transition>
</template>

<script setup lang="ts">
import { blogCount, loadNetDb } from '@/utils/sqliteUtils';
import { onMounted, ref } from 'vue';

const props = defineProps<{ tag: {
  tag_id: string;
  tag_name: string;
} }>();

const blogcount = ref(0);
onMounted(async () => {
  const data = await loadNetDb();
  blogcount.value = await blogCount({ tags: props.tag.tag_name }, data);
})
</script>

<style scoped>
*{
    padding: 0;
    margin: 0;
}

.tagItem{
  width: 70%;

  background-color: #f7ebd9;
  
  box-shadow: inset 0 0 3px #bebebedc,0 0 3px #aaaaaab7;
  border-radius: 1rem;

  display: flex;
  align-items: center;
  justify-content: space-around;

  margin-bottom: 0.75rem;
  padding: 1em;
  text-decoration: none;
  color: #000000;
}

</style>
