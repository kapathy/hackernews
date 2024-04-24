<script setup>
import { ref, onMounted } from 'vue';
import TopStory from './TopStory.vue'

const stories = ref([]);

const fetchStories = async () => {
  const topStoriesEndpoint = 'https://hacker-news.firebaseio.com/v0/topstories.json';
  const storyInfoEndpoint = 'https://hacker-news.firebaseio.com/v0/item/[id].json';
  const authorInfoEndpoint = 'https://hacker-news.firebaseio.com/v0/user/[id].json';

  try {
    const response = await fetch(topStoriesEndpoint);
    const data = await response.json();

    const randomIds = getRandomIds(data, 10);

    const storyResponses = await Promise.all(randomIds.map(id => fetch(storyInfoEndpoint.replace('[id]', id))));
    let storyData = await Promise.all(storyResponses.map(response => response.json()));

    const authorResponses = await Promise.all(storyData.map(story => fetch(authorInfoEndpoint.replace('[id]', story.by))));
    const authorData = await Promise.all(authorResponses.map(response => response.json()));

    storyData.forEach((story, index) => {
      story.authorId = authorData[index].id;
      story.authorKarma = authorData[index].karma;
    });

    storyData = storyData.sort((a, b) => a.score - b.score);

    stories.value = storyData;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};

const getRandomIds = (array, n) => {
  const shuffled = array.sort(() => 0.5 - Math.random());
  return shuffled.slice(0, n);
};

onMounted(() => {
  fetchStories();
});
</script>

<template>
  <div class="container">
    <h1 class="title">Hacker News Top Stories</h1>
    <ul class="stories-grid">
      <TopStory 
        v-for="story in stories"
        :key="story.id"
        class="story-item"
        :story=story 
      />
    </ul>
  </div>
</template>

<style scoped>
.container {
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.title {
  text-align: center;
  color: var(--text-color);
  margin-bottom: 20px;
  font-family: var(--font-family);
}

.stories-grid {
  list-style-type: none;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20px;
}

.story-item {
  background-color: #fff;
  border-radius: 8px;
  width: 450px;
  height: 250px;
  padding: 20px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

@media (max-width: 1200px) {
  .story-item {
    flex-basis: calc(50% - 20px);
  }
}

@media (max-width: 768px) {
  .story-item {
    flex-basis: calc(100% - 20px);
  }
}
</style>