<script>

	import songs from '../lyrics/lyrics';

	import SongSearcher from '../components/SongSearcher.svelte';

</script>

<svelte:head>
	<title>Search a song - Karaom</title>
</svelte:head>

<div class="has-text-centered section">
	<h1 class="title">Karaom</h1>
	<h1 class="subtitle">Have fun with a free Karaoke</h1>
	<a class="button is-info" href="https://github.com/Karaom/karaom-public/issues/new?title=I%20would%20a%20new%20song%20on%20Karaom!&body=**Song%20title:**%20Your%20song%20title%20here">Ask a song!</a>
</div>

<SongSearcher size="large" {songs} />