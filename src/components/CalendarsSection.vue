<script setup>
import { ref } from 'vue';
import Calendar from './Calendar.vue';
import ThemeChangeButton from './ThemeChangeButton.vue';

/* Состояние для режима цветвой темы */
const isDarkModeOn = ref(false);

/* Состояние для начального месяца */
const month = ref(2);

/* Состояние для начального года */
const year = ref(2021);

/* Массив с названиями месяцев */
const months = [
	'Январь',
	'Февраль',
	'Март',
	'Апрель',
	'Май',
	'Июнь',
	'Июль',
	'Август',
	'Сентябрь',
	'Октябрь',
	'Ноябрь',
	'Декабрь',
];

/* Массив с названиями дней недели */
const weekDays = ['Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб', 'Вс'];

/* Названия месяцев для переключения через ссылки */
const monthsFromLinks = ['Март', 'Апрель', 'Май'];

/* Изменяем значение начального месяца, исходя из названия месяца внутри нажатой ссылки */
const selectMonth = (selectedMonth) =>
	(month.value = months.findIndex((month) => month === selectedMonth));

/* Функция для перехода к предыдущему месяцу */
const switchToPrevMonth = () =>
	month.value >= 1 ? month.value-- : ((month.value = 11), year.value--);

/* Функция для перехода к следующему месяцу */
const switchToNextMonth = () =>
	month.value <= 10 ? month.value++ : ((month.value = 0), year.value++);

/* Функция для перехода к предыдущему году */
const switchToPrevYear = () => year.value--;

/* Функция для перехода к следующему году */
const switchToNextYear = () => year.value++;
</script>

<template>
	<!-- Секция с календарями -->
	<section class="calendars" :class="isDarkModeOn && 'dark'">
		<header class="task-header">
			<h2>Тестовое задание</h2>

			<!-- Кнопка смены цветовой схемы -->
			<ThemeChangeButton
				@toggle-color-theme="() => (isDarkModeOn = !isDarkModeOn)"
				:is-dark-mode-on="isDarkModeOn" />
		</header>

		<!-- Обертка для календарей -->
		<div class="calendars-wrapper">
			<!-- Календари -->
			<Calendar
				@switch-to-prev-month="switchToPrevMonth"
				@switch-to-next-month="switchToNextMonth"
				@switch-to-prev-year="switchToPrevYear"
				@switch-to-next-year="switchToNextYear"
				:months="months"
				:week-days="weekDays"
				:month="month"
				:year="year"
				:dark-mode="isDarkModeOn" />

			<Calendar
				@switch-to-prev-month="switchToPrevMonth"
				@switch-to-next-month="switchToNextMonth"
				@switch-to-prev-year="switchToPrevYear"
				@switch-to-next-year="switchToNextYear"
				:months="months"
				:week-days="weekDays"
				:month="month"
				:year="year"
				:dark-mode="isDarkModeOn" />

			<Calendar
				@switch-to-prev-month="switchToPrevMonth"
				@switch-to-next-month="switchToNextMonth"
				@switch-to-prev-year="switchToPrevYear"
				@switch-to-next-year="switchToNextYear"
				:months="months"
				:week-days="weekDays"
				:month="month"
				:year="year"
				:dark-mode="isDarkModeOn" />
		</div>

		<!-- Ссылки для переключения месяцев календарей -->
		<nav>
			<ul class="month-navigation-links">
				<li v-for="(month, index) in monthsFromLinks" :key="index">
					<a href="#" class="month-nav-link" @click="selectMonth(month)">{{ month }}</a>
				</li>
			</ul>
		</nav>
	</section>
</template>

<style lang="scss" scoped>
// Секция с календарями
.calendars {
	flex: 1;
	display: flex;
	flex-direction: column;
	gap: 2rem;

	padding: 3rem;
	transition: all 0.3s ease-in;

	// Шапка с заголовком задания и кнопкой для смены цветовой схемы
	.task-header {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-between;

		padding-left: 5px;

		h2 {
			font-size: 32px;
		}
	}

	// Обертка для календарей
	.calendars-wrapper {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: space-between;
	}

	// Ссылки для переключения месяцев календарей
	.month-navigation-links {
		display: flex;
		flex-direction: row;
		align-items: center;
		gap: 2rem;

		padding-left: 5px;
		font-size: 18px;
	}

	// Изменения при добавлении для секции 'calendars' класса 'dark' при переключении цветовой схемы
	&.dark {
		background-color: #2c3649;
		color: #fff;
	}

	// Адаптив для различных устройств
	@media screen and (max-width: 480px) {
		padding: 2rem;

		.task-header {
			h2 {
				font-size: 24px;
			}
		}

		.calendars-wrapper {
			flex-direction: column;
			gap: 2rem;
		}

		.month-navigation-links {
			justify-content: center;
		}
	}

	@media screen and (max-width: 786px) {
		.calendars-wrapper {
			flex-wrap: wrap;
			gap: 2rem;
			justify-content: space-evenly;
		}

		.month-navigation-links {
			justify-content: center;
		}
	}

	@media screen and (max-width: 1024px) {
		.calendars-wrapper {
			flex-wrap: wrap;
			gap: 2rem;
			justify-content: space-evenly;
		}

		.month-navigation-links {
			justify-content: center;
		}
	}

	@media screen and (min-width: 1281px) {
		justify-content: space-around;
	}
}
</style>
