<script context="module">

    import lyrics from '../../lyrics/lyrics';

    export async function preload(page, session) {
        const { songName } = page.params;
        return {
            song: lyrics.filter(music => music.title.toLowerCase().replace(/\s(\w+)/g, '-$1').trim() === songName)[0],
            songs: lyrics
        };
    }

</script>

<script>

    import { onMount } from 'svelte';
    import { isFullScreen, songsQueue } from '../../stores/player';

    import SongPlayer from '../../components/SongPlayer.svelte';
    import SongSearcher from '../../components/SongSearcher.svelte';
    import SongCard from '../../components/SongCard.svelte';
    import OpenFullScreenButton from '../../components/OpenFullScreenButton.svelte';

    export let song;
    export let songs;

    let currentLyric = '...';

    $: queue = $songsQueue.map(sQ => songs.filter(s => s.youtubeId === sQ)[0]);

    async function onFullScreenChange() {
        $isFullScreen = (document.fullscreenElement || document.mozFullScreenElement || document.webkitFullscreenElement) !== null;
    }

    onMount(async () => {
        document.addEventListener('fullscreenchange', onFullScreenChange, false);
        document.addEventListener('webkitfullscreenchange', onFullScreenChange, false);
        document.addEventListener('mozfullscreenchange', onFullScreenChange, false);
    })

</script>

<style>
    .fullScreenTitle { color: black; font-size: 75px; }
</style>

<svelte:head>
    <title>Playing {song.title} by {song.artist} - Karaom</title>
</svelte:head>

<div class="section has-text-centered">

    <div class="columns">

        <div class="column" class:isHidden={$isFullScreen}></div>

        <div class="column {$isFullScreen ? '' : 'is-7'}">

            <div class="animated">
                
                <h1 class="title animated" class:isHidden={$isFullScreen}>{song.title} by {song.artist}</h1>
                <div class="section animated" >
                    <SongPlayer {song} bind:currentLyric={currentLyric} />
                </div>
                <h2 class:title={!$isFullScreen} class:fullScreenTitle={$isFullScreen}>{currentLyric}</h2>
                <a href="https://github.com/Karaom/karaom-public/issues/new?title=%5BLyric%20issue%5D%20Music%20{song.title}%20by%20{song.artist}&body=**Explain%20the%20issue%20you%20have%20here:**%20" class:isHidden={$isFullScreen} class="button is-small is-danger animated">Any issue with lyrics? Report it here</a>
            </div>

        </div>

        <div class="column is-5" class:isHidden={$isFullScreen}>
            <div class="dropdown is-hoverable">
                <div class="dropdown-trigger">
                    <button class="button is-dark">
                        <span>Options</span>
                        <span class="icon is-small">
                            <i class="fas fa-angle-down"></i>
                        </span>
                    </button>
                </div>
                <div class="dropdown-menu is-dark">
                    <div class="dropdown-content is-dark">
                        <div class="dropdown-item">
                            <OpenFullScreenButton />
                        </div>
                    </div>
                </div>
            </div>

            <div class="small-section" class:isHidden={$isFullScreen}>
                <h1 class="title">Song queue</h1>
                <div class="small-section" class:isHidden={$isFullScreen}>
                    <SongSearcher isSongsQueue={true} songs={queue} cardSize="small" show={1} />
                </div>
            </div>

        </div>

    </div>

    <div class="small-section" class:isHidden={$isFullScreen}>
        <h1 class="title">Songs List</h1>
        <SongSearcher size="large" {songs} />
    </div>

</div>