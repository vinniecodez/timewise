<script setup>
import { 
	isActivityValid, 
	isHourValid, 
	isNumber, 
	isTimelineItemValid, 
	validateActivities, 
	validateSelectOptions 
} from '@/validators'
import BaseSelect from './BaseSelect.vue'
import TimelineStopwatch from './TimelineStopwatch.vue'
import TimelineHour from './TimelineHour.vue'

const props = defineProps({
  timelineItem: {
    required: true,
    type: Object,
		validator: isTimelineItemValid
  },
	activities: {
		required: true,
		type: Array,
		validator: validateActivities
	},
	activitySelectOptions: {
		required: true,
		type: Array,
		validator: validateSelectOptions
	}
})

const emit = defineEmits({
	updateActivitySeconds: isNumber,
	selectActivity: isActivityValid,
	scrollToHour: isHourValid
})

function selectActivity(id) {
	emit(
		'selectActivity', 
		findActivityById(id)
	)
}

function findActivityById(id) {
	return props.activities.find((activity) => activity.id === id) || NULLABE_ACTIVITY
}
</script>

<template>
	<li class="relative flex flex-col gap-2 border-t border-gray-200 py-10 px-4">
		<TimelineHour 
			:hour="timelineItem.hour" 
			@click.prevent="emit('scrollToHour', timelineItem.hour)" 
		/>
		<BaseSelect 
			:selected="timelineItem.activityId" 
			:options="activitySelectOptions" 
			placeholder="Rest" 
			@select="selectActivity"
		/>
		<TimelineStopwatch 
			:seconds="timelineItem.activitySeconds" 
			:hour="timelineItem.hour" 
			@update-seconds="emit('updateActivitySeconds', $event)"
		/>
	</li>
</template>