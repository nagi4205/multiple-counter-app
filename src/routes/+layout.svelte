<script>
	import Header from './Header.svelte';
	import cute_dog from '$lib/images/img_1194.png';
	import '../app.css';
</script>

<div class="flex justify-center w-full">
	<div class="flex flex-col">
		<Header />
		<main>
			<slot />
		</main>
		<img src={cute_dog} alt="cutedog" class="w-200 h-400"/>
	</div>
</div>