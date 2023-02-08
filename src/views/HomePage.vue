<template>
	<header>
		<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
			<h1
				class="text-3xl font-bold leading-tight tracking-tight text-gray-900">
				Cities
			</h1>
		</div>
	</header>
	<main>
		<div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
			<!-- Replace with your content -->
			<div class="px-4 py-8 sm:px-0">
				<div class="flex">
					<div class="drop-zone flex">
						<div
							class="w-full h-full mx-auto bg-gray-100 mr-4 rounded-lg shadow-md">
							<KanbanHeader :title="'Common'" :show-buttons="true"/>
							<LineLayout/>
							<div class="w-96 px-2">
								<drag
									v-for="city in cities"
									:data="city"
									class="item px-2 mb-4"
									:key="city">
									<CityDetails :city="city"/>
								</drag>
							</div>
						</div>
						<!-- india -->
						<div
							class="w-full h-full mx-auto bg-gray-100 mr-4 rounded-lg  shadow-md">
							<KanbanHeader :title="'India'"/>
							<LineLayout/>
							<drop-list
								:items="india"
								class="w-96 h-full"
								@insert="onInsertIndia"
								@reorder="$event.apply(india)">
								<template v-slot:item="{ item }">
									<drag
										class="item px-2 mb-4"
										:key="item.id"
										:data="item">
										<CityDetails :city="item"/>
									</drag>
								</template>
								<template v-slot:feedback="{ data }">
									<DropFeedback :key="data.id" :city="data"/>
								</template>
							</drop-list>
						</div>
						<!-- Philippines -->
						<div
							class="w-full h-full mx-auto bg-gray-100 mr-2 rounded-lg  shadow-md">
							<KanbanHeader :title="'Philippines'"/>
							<LineLayout/>
							<drop-list
								:items="philippines"
								class="w-96 h-full"
								@insert="onInsertPhilippines"
								@reorder="$event.apply(philippines)">
								<template v-slot:item="{ item }">
									<drag
										class="item px-2 mb-2"
										:key="item"
										:data="item">
										<CityDetails :city="item"/>
									</drag>
								</template>
								<template v-slot:feedback="{ data }">
									<DropFeedback :key="data.id" :city="data"/>
								</template>
							</drop-list>
						</div>
					</div>
				</div>
			</div>
			<!-- /End replace -->
		</div>
	</main>

	<Notification
		v-if="notification"
		:show-notification="notification"
		:is-error="isError"
        :title="notificationTitle"
		@close-notification="handleCloseNotification" />
</template>
<script setup>
import { Drag, DropList } from 'vue-easy-dnd';
import { COMMON, INDIA, PHILIPPINES } from '../composables/countries';
import { onMounted, ref } from 'vue';
import { RectangleGroupIcon } from '@heroicons/vue/24/outline';
import { notificationMessage } from '../composables/notifications-message'
import {
	Bars4Icon,
	ChatBubbleLeftEllipsisIcon,
	PlusIcon,
} from '@heroicons/vue/20/solid';
import Notification from '../components/Notification.vue';
import CityDetails from '../components/CityDetails.vue';
import DropFeedback from '../components/DropFeedback.vue';
import LineLayout from '../components/layout/LineLayout.vue'
import KanbanHeader from '../components/Kanban/KanbanHeader.vue';

const cities = ref([
	{
		id: 1,
		country: 'India',
		name: 'Himachal',
		image: 'https://images.livemint.com/img/2021/07/07/600x338/99faa022-de6e-11eb-90a3-059cac49bd75_1625632602822_1625632636240.jpg',
	},
	{
		id: 2,
		country: 'India',
		name: 'Gujrat',
		image: 'https://images.livemint.com/img/2021/07/07/600x338/99faa022-de6e-11eb-90a3-059cac49bd75_1625632602822_1625632636240.jpg',
	},
	{
		id: 3,
		country: 'Philippines',
		name: 'Manila',
		image: 'https://newsinfo.inquirer.net/files/2022/04/284435.jpeg',
	},
	{
		id: 4,
		country: 'Philippines',
		name: 'Cebu',
		image: 'https://newsinfo.inquirer.net/files/2022/04/284435.jpeg',
	},
]);

const notification = ref(false);
const isError = ref(false);
const philippines = ref([]);
const notificationTitle = ref('');

const india = ref([]);
const onInsertIndia = (event) => {
	if (event.data.country != INDIA) {
		showNotification(notificationMessage.drop_error, true)
		return;
	}

	india.value.splice(event.index, 0, event.data);
	cities.value = cities.value.filter((city) => city.id != event.data.id);
	showNotification(`${notificationMessage.drop_success} ${INDIA}`, false)
};

const onInsertPhilippines = (event) => {
	if (event.data.country != PHILIPPINES) {
		showNotification(notificationMessage.drop_error, true)
		return;
	}
	philippines.value.splice(event.index, 0, event.data);
	cities.value = cities.value.filter((city) => city.id != event.data.id);
	showNotification(`${notificationMessage.drop_success} ${PHILIPPINES}`, false)
};

const handleCloseNotification = () => {
	notification.value = false;
};

const showNotification = (message, errorStatus) => {
	errorStatus ? isError.value = true : isError.value = false;
	notification.value = true;
	notificationTitle.value = message
	setTimeout(() => {
		notification.value = false;
		isError.value = false
	}, 2000);
};

onMounted(() => {});
</script>
