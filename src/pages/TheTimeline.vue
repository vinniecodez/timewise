<script setup>
import TimelineItem from '@/components/TimelineItem.vue';
import { isTimelineItemValid } from '@/validators';

defineProps({
  timelineItems: {
    required: true,
    type: Array,
		validator(timelineItems) {
			return timelineItems.every(isTimelineItemValid)
		}
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