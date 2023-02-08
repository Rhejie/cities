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
							<div class="">
								<div class="flex px-2 pt-4 sm:px-6">
									<div class="flex min-w-0 flex-1">
										<div
											class="min-w-0 flex-1 px-2 md:grid md:grid-cols-2 md:gap-4">
											<p
												class="truncate inline-flex text-sm font-medium text-gray-600">
												<RectangleGroupIcon
													class="h-5 w-5 text-gray-500 mr-2"
													aria-hidden="true" />
												Common
											</p>
										</div>
									</div>
									<div class="bg-white px-1 rounded-lg flex">
										<ChatBubbleLeftEllipsisIcon
											class="h-5 w-5 text-gray-400 mr-2"
											aria-hidden="true" />
										<PlusIcon
											class="h-5 w-5 text-gray-400 mr-2"
											aria-hidden="true" />
										<Bars4Icon
											class="h-5 w-5 text-gray-400"
											aria-hidden="true" />
									</div>
								</div>
							</div>
							<div class="hidden sm:block" aria-hidden="true">
								<div class="py-2">
									<div class="border-t border-gray-200" />
								</div>
							</div>
							<div class="w-96 px-2">
								<drag
									v-for="city in cities"
									:data="city"
									class="item px-2 mb-4"
									:key="city">
									<p class="text-gray-500 mt-4 mb-2 flex">
										<RectangleGroupIcon
											class="h-5 w-5 text-gray-500 mr-2"
											aria-hidden="true" />
										{{ city.name }}
									</p>
									<img :src="city.image" alt="" class="shadow-lg"/>
								</drag>
							</div>
						</div>
						<!-- india -->
						<div
							class="w-full h-full mx-auto bg-gray-100 mr-4 rounded-lg  shadow-md">
							<div class="">
								<div class="flex px-2 pt-4 sm:px-6">
									<div class="flex min-w-0 flex-1">
										<div
											class="min-w-0 flex-1 px-2 md:grid md:grid-cols-2 md:gap-4">
											<p
												class="truncate inline-flex text-sm font-medium text-gray-600">
												<RectangleGroupIcon
													class="h-5 w-5 text-gray-500 mr-2"
													aria-hidden="true" />
												India
											</p>
										</div>
									</div>
								</div>
							</div>
							<div class="hidden sm:block" aria-hidden="true">
								<div class="py-2">
									<div class="border-t border-gray-200" />
								</div>
							</div>
							<drop-list
								:items="india"
								class="w-96 h-full"
								@insert="onInsertIndia"
								@reorder="$event.apply(india)">
								<template v-slot:item="{ item }">
									<drag
										class="item px-2"
										:key="item.id"
										:data="item">
										<p class="text-gray-500 mt-4 mb-2 flex">
											<RectangleGroupIcon
												class="h-5 w-5 text-gray-500 mr-2"
												aria-hidden="true" />
											{{ item.name }}
										</p>
										<img :src="item.image" alt="" />
									</drag>
								</template>
								<template v-slot:feedback="{ data }">
									<div class="px-2" :key="data.id">
										<p class="text-gray-500 mt-4 mb-2 flex">
											<RectangleGroupIcon
												class="h-5 w-5 text-gray-500 mr-2"
												aria-hidden="true" />
											{{ data.name }}
										</p>
										<img :src="data.image" alt="" />
									</div>
								</template>
							</drop-list>
						</div>
						<!-- Philippines -->
						<div
							class="w-full h-full mx-auto bg-gray-100 mr-2 rounded-lg  shadow-md">
							<div class="">
								<div class="flex px-2 pt-4 sm:px-6">
									<div class="flex min-w-0 flex-1">
										<div
											class="min-w-0 flex-1 px-2 md:grid md:grid-cols-2 md:gap-4">
											<p
												class="truncate inline-flex text-sm font-medium text-gray-600">
												<RectangleGroupIcon
													class="h-5 w-5 text-gray-500 mr-2"
													aria-hidden="true" />
												Philippines
											</p>
										</div>
									</div>
								</div>
							</div>
							<div class="hidden sm:block" aria-hidden="true">
								<div class="py-2">
									<div class="border-t border-gray-200" />
								</div>
							</div>
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
										<p class="text-gray-500 mt-4 mb-2 flex">
											<RectangleGroupIcon
												class="h-5 w-5 text-gray-500 mr-2"
												aria-hidden="true" />
											{{ item.name }}
										</p>
										<img :src="item.image" alt="" />
									</drag>
								</template>
								<template v-slot:feedback="{ data }">
									<div class="px-2" :key="data.id">
										<p class="text-gray-500 mt-4 mb-2 flex">
											<RectangleGroupIcon
												class="h-5 w-5 text-gray-500 mr-2"
												aria-hidden="true" />
											{{ data.name }}
										</p>
										<img :src="data.image" alt="" />
									</div>
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
import {
	Bars4Icon,
	ChatBubbleLeftEllipsisIcon,
	PlusIcon,
} from '@heroicons/vue/20/solid';
import Notification from '../components/Notification.vue';

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
		notification.value = true;
		isError.value = true;
        notificationTitle.value = 'This city is not belongs to India';
		closeNotification();
		return;
	}

	india.value.splice(event.index, 0, event.data);
	cities.value = cities.value.filter((city) => city.id != event.data.id);
	notification.value = true;
	isError.value = false;
	notificationTitle.value = 'Successfully moved to India';
	closeNotification();
};

const onInsertPhilippines = (event) => {
	if (event.data.country != PHILIPPINES) {
		notification.value = true;
		isError.value = true;
        notificationTitle.value = 'This city is not belongs to Philippines';
		closeNotification();
		return;
	}
	philippines.value.splice(event.index, 0, event.data);
	cities.value = cities.value.filter((city) => city.id != event.data.id);
	notification.value = true;
	isError.value = false;
	notificationTitle.value = 'Successfully moved to Philippines';
	closeNotification();
};

const handleCloseNotification = () => {
	notification.value = false;
};

const closeNotification = () => {
	setTimeout(() => {
		notification.value = false;
	}, 2000);
};

onMounted(() => {});
</script>
