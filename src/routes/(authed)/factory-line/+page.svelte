<script lang="ts">
	import Deliveries from '$lib/components/factory-line/Deliveries.svelte';
	import FactoryLines from '$lib/components/factory-line/FactoryLines.svelte';
	import ItemList from '$lib/components/factory-line/ItemList.svelte';

	let { data } = $props();

	let chosenFactory = $state('');
	let factoryLines = $derived.by(() => {
		if (chosenFactory === '') {
			return data.factoryLines.flatMap((factory) => factory.lines);
		} else {
			const factory = data.factoryLines.find((factory) => factory.FACTORYNAME === chosenFactory);
			return factory ? factory.lines : [];
		}
	});
	let deliveries = $derived.by(() => {
		if (chosenFactory === '') {
			return data.deliveries;
		} else {
			return data.deliveries
				.filter(
					(delivery) =>
						delivery.SOURCENAME === chosenFactory || delivery.DESTINATIONNAME === chosenFactory
				)
				.map((delivery) => {
					if (delivery.SOURCENAME === chosenFactory) {
						return {
							...delivery,
							SOURCENAME: delivery.DESTINATIONNAME,
							DESTINATIONNAME: delivery.SOURCENAME,
							AMOUNT: -delivery.AMOUNT
						};
					}
					return delivery;
				});
		}
	});
</script>

<div class="container">
	<div class="factories-container">
		<div class="factories-container-text">Factories:</div>
		<button
			class="factory-button"
			onclick={() => {
				chosenFactory = '';
			}}>전체</button
		>
		{#each data.factoryLines as factories}
			<button
				class="factory-button"
				onclick={() => {
					chosenFactory = factories.FACTORYNAME;
				}}>{factories.FACTORYNAME}</button
			>
		{/each}
	</div>
	<div class="item-list">
		<ItemList />
	</div>
	<div class="content">
		<div class="factory-lines">
			<FactoryLines lines={factoryLines} />
		</div>
		<div class="deliveries">
			<Deliveries {deliveries} />
		</div>
	</div>
</div>

<style>
	.factories-container {
		display: flex;
		flex-direction: row;
		align-items: center;
		margin: 20px;
	}

	.factories-container-text {
		margin-right: 10px;
		font-weight: bold;
	}

	.factory-button {
		background-color: rgba(250, 149, 73, 255);
		color: white;
		border: none;
		padding: 10px 15px;
		margin-right: 10px;
		border-radius: 5px;
		cursor: pointer;
		transition:
			background-color 0.3s ease,
			transform 0.3s ease;
	}

	.factory-button:hover {
		background-color: rgba(250, 149, 73, 0.8);
		transform: translateY(-2px);
	}

	.factory-button:active {
		transform: scale(0.98);
	}

	/* 전체 컨테이너 설정 */
	.container {
		display: flex;
		flex-direction: column;
		width: 100vw; /* 브라우저 전체 너비 */
		max-width: 100%;
	}

	/* ItemList 스타일 */
	.item-list {
		overflow-x: auto; /* 가로 스크롤 활성화 */
		white-space: nowrap; /* 자식 요소들이 한 줄로 정렬 */
		padding: 10px;
	}

	/* Content 영역 스타일 */
	.content {
		display: flex;
		flex: 1; /* 남은 공간을 차지 */
		overflow: hidden; /* 불필요한 스크롤 제거 */
	}

	/* FactoryLines 스타일 */
	.factory-lines {
		flex: 2; /* 왼쪽 영역이 차지할 비율 */
		overflow-y: auto; /* 세로 스크롤 활성화 */
		padding: 10px;
	}

	/* Deliveries 스타일 */
	.deliveries {
		flex: 1; /* 오른쪽 영역이 차지할 비율 */
		overflow-y: auto; /* 세로 스크롤 활성화 */
		padding: 10px;
	}
</style>
