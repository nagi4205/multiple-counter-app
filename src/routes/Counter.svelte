<script lang="ts">
import Button from './CustomButton.svelte';

type CounterType = {
	id: number;
	title: string;
	count: number;
};

let counters: CounterType[] = [{ id: 1, title: 'new', count: 0 }];

const addCounter = (): void => {
	const newId: number = counters.length > 0 ? Math.max(...counters.map(c => c.id)) + 1 : 1;
	counters = [...counters, { id: newId, title: 'new', count: 0 }];
}

const removeCounter = (counterId: number): void => {
	console.log(counterId);
	counters = counters.filter(c => c.id !== counterId);
}

$: total = counters.reduce((sum: number, counter: CounterType) => sum + counter.count, 0);

const increment = (counterId: number): void => {
			const index = counters.findIndex(c => c.id === counterId);
			counters[index].count += 1;
	}

const decrement = (counterId: number): void => {
		const index = counters.findIndex(c => c.id === counterId);
		if (counters[index].count > 0) counters[index].count -= 1;
}

const reset = (counterId: number): void => {
		const index = counters.findIndex(c => c.id === counterId);
		counters[index].count = 0;
}

const changeTitle = (counterId: number, event: Event): void => {
	const inputElement = event.target as HTMLInputElement; // イベントのターゲットを HTMLInputElement としてキャスト
	const index = counters.findIndex(c => c.id === counterId);
	counters[index].title = inputElement.value;
}
</script>

<div class="flex flex-col items-center">
	{#each counters as counter (counter.id)}
	<div class="w-80 xs:w-96 h-12 rounded border-solide bg-gray-100 shadow-xl flex items-center justify-between mb-4">
		<input type="text" class="text-gray-500 mx-2 xs:mx-4 w-32" value={counter.title} on:input={(event) => changeTitle(counter.id, event)}>
		<div class=" font-bold xs:px-2">{counter.count}</div>
			<div class="xs:px-2">
        <Button label="+" onClick={() => increment(counter.id)} className="bg-red-500 rounded-l text-white" />
        <Button label="-" onClick={() => decrement(counter.id)} className="bg-blue-500 text-white"/>
        <Button label="0" onClick={() => reset(counter.id)} className="bg-yellow-500 rounded-r text-white"/>
        <Button label="×" onClick={() => removeCounter(counter.id)} className="xs:pl-2 text-black"/>
			</div>
	</div>
	{/each}
	
	<button class="w-80 xs:w-96 rounded-md bg-green-400 text-white" on:click={addCounter} tabindex="-1">new counter</button>
	
	<div class="w-full text-center">
		<div>title list: {counters.filter(c => c.title !== '').map(c => c.title).join(', ')}</div>
		<div>sum of count: {total}</div>
	</div>
</div>
