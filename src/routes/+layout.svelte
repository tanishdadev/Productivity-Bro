<script>
	import '../app.css';
	
	let { children } = $props();
</script>

<svelte:head>
	<title>Productivity Bro</title>
	<meta name="description" content="Productivity Bro is a web application designed to help you manage your tasks and boost your productivity.">
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
</svelte:head>

<div class="min-h-screen w-full bg-blue-300 m-0 p-0 absolute inset-0">
	{@render children()}
</div>