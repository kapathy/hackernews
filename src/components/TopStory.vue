<script setup>
import StoryLink from './StoryLink.vue'

defineProps({
  story: {
    type: Object,
    required: true
  }
});

const formatDate = (timestamp) => {
  const date = new Date(timestamp * 1000);
  const options = { day: '2-digit', month: '2-digit', year: '2-digit' };
  return date.toLocaleDateString(undefined, options).split('.').reverse().join('.');
};
</script>

<template>
  <div class="story-content">
    <h2 class="story-title">{{ story.title }}</h2>
    <div class="story-details">
      <span class="story-score">Score:
        <span class="light-font">{{ story.score }}</span>
      </span>
      <span class="story-time">Time:
        <span class="light-font">{{ formatDate(story.time) }}</span>
      </span>
      <div class="author-info">
        <div class="author-id">Author ID:
          <span class="light-font">{{ story.authorId }}</span>
        </div>
        <div class="author-karma">Karma:
          <span class="light-font">{{ story.authorKarma }}</span>
        </div>
      </div>
    </div>
    <StoryLink :url="story.url">Read Story</StoryLink>
  </div>
</template>

<style>
.story-content {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-start;
  height: 100%;
  width: 100%;
}

.story-title {
  color: var(--text-color);
  font-weight: 500;
  font-size: 1.2em;
  margin-bottom: 10px;
  display: block;
}

.story-details {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 15px;
}

.story-score,
.story-time,
.author-id,
.author-karma {
  color: var(--text-color);
  font-size: 0.9em;
  margin-bottom: 5px;
  font-weight: 600;
}

.light-font {
  color: var(--secondary-text-color);
  font-weight: 300;
}
</style>
