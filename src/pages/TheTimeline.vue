<script setup>
import TimelineItem from '@/components/TimelineItem.vue';

defineProps({
  timelineItems: {
    required: true,
    type: Array
  }
})
</script>

<template>
	<div class="mt-7">
		<ul>
			<TimelineItem 
				v-for="timelineItem in timelineItems" 
				:key="timelineItem.hour"
				class="relative flex flex-col gap-2 border-t border-gray-200 py-10 px-4"
				:timeline-item="timelineItem"
			/>
		</ul>
	</div>
</template>