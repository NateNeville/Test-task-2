<script setup></script>

<template>
	<!-- Секция "Геопаспорт" -->
	<section class="geopassport">
		<img src="../assets/geopassport.png" alt="Geopassport" class="geopassport-logo" />

		<article class="geopassport-description">
			<header class="geopassport-header">
				<h1>ЗАГОЛОВОК</h1>
			</header>
			<p>
				Платформа управления геопространственными данными "Геопаспорт" - это инновационный
				продукт, представляющий собой набор программных решений и позволяющий создавать
				современное прикладное программное обесепчение в области управления данными
				территории и региона. Программа включена в единый реестр российских программ для ЭВМ
				и баз данных.
			</p>
		</article>
	</section>
</template>

<style lang="scss" scoped>
// Секция "Геопаспорт"
.geopassport {
	flex: 1;
	display: flex;
	flex-direction: row;
	align-items: stretch;

	background-color: #2c3649;
	color: #fff;

	.geopassport-logo {
		flex: 1;
	}

	.geopassport-description {
		display: flex;
		flex-direction: column;
		align-items: flex-start;
		gap: 2rem;
		flex: 2;

		padding: 25px;

		.geopassport-header {
			position: relative;
			padding: 0 65px 0 60px;
			background-color: #6f45e0;

			font-size: 44px;
			font-weight: 800;
			letter-spacing: 2px;

			&::before {
				content: '';
				position: absolute;
				width: 30px;
				height: 100%;
				top: 0;
				left: 15px;
				background-color: #000;
			}

			&::after {
				content: '';
				position: absolute;
				width: 50px;
				height: 100%;
				top: 0;
				right: 0;
				background-color: #f73373;
			}
		}

		& p {
			font-size: 16px;
			line-height: 24px;
			text-align: justify;
		}
	}

	// Адаптив для различных устройств
	@media screen and (max-width: 480px) {
		flex-direction: column;

		.geopassport-description {
			align-items: center;

			.geopassport-header {
				font-size: 32px;
				font-weight: 700;
				letter-spacing: 1px;

				padding: 0 55px 0 45px;

				&::before {
					width: 20px;
					height: 100%;
					top: 0;
					left: 10px;
				}

				&::after {
					width: 35px;
				}
			}

			p {
				font-size: 14px;
				text-align: center;
			}
		}
	}

	@media screen and (max-width: 786px) {
		flex-direction: column;
	}

	@media screen and (max-width: 1024px) {
		flex-direction: column;
	}

	@media screen and (max-width: 1280px) {
		flex-direction: column;
	}

	@media screen and (min-width: 1281px) {
		.geopassport-logo {
			width: 50vw;
		}
	}
}
</style>
