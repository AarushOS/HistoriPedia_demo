<script lang="ts">
	import Searchbar from './searchbar.svelte';
import SearchBar from './searchbar.svelte'
</script>
<main>
    <section>
        <h1 class="title">HistoriPedia</h1>
        <Searchbar />
    </section>
</main>
<style>
@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@700&display=swap');

.title{
    font-family: 'Josefin Sans', sans-serif;
}
h1{
    font-size: 5.5rem;
    position: absolute;
	transform: translate(-50%, 50%);
	left: 50%;
    top: 10%;
    color: #f4f3ef;
    user-select: none;
    margin-bottom: 10px;
	z-index: 9;
}

@keyframes gradient {
    0% {background-position: 0%}
    100% {background-position: 100%}
}
</style>