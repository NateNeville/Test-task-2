<script setup>
import { ref, computed, watchEffect } from 'vue';

/* Входные параметры */
const props = defineProps({
	months: Array,
	weekDays: Array,
	month: Number,
	year: Number,
	darkMode: Boolean,
});

/* События для прослушивания */
const emit = defineEmits([
	'switchToPrevMonth',
	'switchToNextMonth',
	'switchToPrevYear',
	'switchToNextYear',
]);

/* Создаём состояния, в которые будем добавлять массив с датами... */
const prevMonthDates = ref(null); // предыдущего месяца
const currMonthDates = ref(null); // текущего месяца
const nextMonthDates = ref(null); // следующего месяца

/* Описываем функцию для вычисления дат календаря */
function renderDates() {
	// День недели на первое число текущего месяца
	const currMonthFirstDateWeekDay = computed(() => new Date(props.year, props.month, 0).getDay());

	// Последнее число текущего месяца
	const currMonthLastDate = computed(() => new Date(props.year, props.month + 1, 0).getDate());

	// Последнее число предыдущего месяца
	const prevMonthLastDate = computed(() => new Date(props.year, props.month, 0).getDate());

	// День недели на первое число следующего месяца
	const nextMonthFirstDateWeekDay = computed(
		() => 7 - new Date(props.year, props.month + 1, 0).getDay()
	);

	// Сбрасываем и задаем начальное значение для рефов, куда будем добавлять даты
	prevMonthDates.value = [];
	currMonthDates.value = [];
	nextMonthDates.value = [];

	// Добавляем даты предыдущего месяца
	for (let i = currMonthFirstDateWeekDay.value; i > 0; i--) {
		const date = prevMonthLastDate.value - i + 1;
		prevMonthDates.value.push(date);
	}

	// Добавляем даты текущего месяца
	for (let i = 1; i <= currMonthLastDate.value; i++) {
		const date = i;
		currMonthDates.value.push(date);
	}

	// Добавляем даты следующего месяца
	for (let i = 1; i <= nextMonthFirstDateWeekDay.value; i++) {
		const date = i;
		nextMonthDates.value.push(date);
	}
}

/* Вызываем функцию для вычисления дат календаря каждый раз, когда значение текущей даты изменяется */
watchEffect(renderDates);
</script>

<template>
	<!-- Календарь -->
	<div class="calendar" :class="darkMode && 'dark'">
		<!-- Навигация календаря -->
		<nav class="calendar-header">
			<div class="nav-arrow-btn prev-year" @click="$emit('switchToPrevYear')">&lt;&lt;</div>
			<div class="nav-arrow-btn prev-month" @click="$emit('switchToPrevMonth')">&lt;</div>

			<!-- Год и месяц -->
			<div class="month-year">
				{{ `${months[month]} ${year}` }}
			</div>

			<div class="nav-arrow-btn next-month" @click="$emit('switchToNextMonth')">&gt;</div>
			<div class="nav-arrow-btn next-year" @click="$emit('switchToNextYear')">&gt;&gt;</div>
		</nav>

		<!-- Дни недели -->
		<div class="weekdays">
			<div v-for="(day, index) in weekDays" :key="index">
				{{ day }}
			</div>
		</div>

		<!-- Даты -->
		<div class="dates">
			<div class="fade" v-for="(date, index) in prevMonthDates" :key="index">
				{{ date }}
			</div>

			<div v-for="(date, index) in currMonthDates" :key="index">
				{{ date }}
			</div>

			<div class="fade" v-for="(date, index) in nextMonthDates" :key="index">
				{{ date }}
			</div>
		</div>
	</div>
</template>

<style lang="scss" scoped>
// Календарь
.calendar {
	display: flex;
	flex-direction: column;
	gap: 15px;

	width: 300px;
	padding: 15px;

	border: 1px solid rgba(0, 0, 0, 0.1);
	border-radius: 5px;
	box-shadow: 0px 7px 10px rgba(0, 0, 0, 0.15);
	font-size: 14px;

	// Шапка календаря с информацией месяца, года и стрелками навигации
	.calendar-header {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-between;

		.nav-arrow-btn {
			padding: 5px;
			border: 1px solid rgba(0, 0, 0, 0.1);
			border-radius: 3px;
			cursor: pointer;
		}

		.month-year {
			width: 115px;
			text-align: center;
		}
	}

	// Контейнер для дней недели
	.weekdays {
		display: flex;
	}

	// Контейнер для всех видимых дат предыдущего, текущего и следующего месяца
	.dates {
		display: flex;
		flex-wrap: wrap;
		height: 200px;

		.fade {
			color: rgba(0, 0, 0, 0.3);
		}
	}

	// Ячейки непосредственно с днями недели и датами месяца
	.weekdays div,
	.dates div {
		display: flex;
		align-items: center;
		justify-content: center;
		flex: 14.28%;
	}

	&.dark {
		border: 1px solid rgba(255, 255, 255, 0.1);
		box-shadow: 0px 7px 10px rgba(255, 255, 255, 0.15);

		.calendar-header {
			.nav-arrow-btn {
				border: 1px solid rgba(255, 255, 255, 0.1);
			}
		}

		.dates .fade {
			color: rgba(255, 255, 255, 0.3);
		}
	}
}
</style>
